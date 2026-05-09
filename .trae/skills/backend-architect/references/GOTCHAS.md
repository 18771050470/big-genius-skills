# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：N+1 查询陷阱

**问题**：在循环中逐条查询关联数据，导致数据库查询次数随数据量线性增长，性能急剧恶化。

❌ **Before（错误做法）**
```python
# 先查询用户列表，再逐个查询订单
users = db.query("SELECT * FROM users")
for user in users:
    # 每条用户触发一次查询！1000 用户 = 1001 次查询
    orders = db.query(f"SELECT * FROM orders WHERE user_id = {user.id}")
    user.orders = orders
```

✅ **After（正确做法）**
```python
# 使用 JOIN 或 IN 查询一次性获取所有数据
users = db.query("SELECT * FROM users")
user_ids = [u.id for u in users]
# 一次性查询所有订单
orders = db.query("SELECT * FROM orders WHERE user_id IN %s", (user_ids,))
# 在内存中关联
orders_map = defaultdict(list)
for order in orders:
    orders_map[order.user_id].append(order)
for user in users:
    user.orders = orders_map[user.id]
```

**原因**：N+1 查询是性能杀手，1000 条数据会变成 1001 次数据库往返。使用 JOIN、IN 查询或 ORM 的 eager loading（如 SQLAlchemy 的 `joinedload`）可以一次性获取数据。

## Gotcha 2：分布式锁实现不当导致死锁

**问题**：使用 Redis setnx 实现分布式锁，但忘记设置过期时间或续期机制，导致服务崩溃后锁永久不释放。

❌ **Before（错误做法）**
```python
# 只设置锁，没有过期时间
redis.setnx("lock:order:123", "true")
# 处理业务逻辑...
# 如果服务在这里崩溃，锁永远不会释放！
redis.delete("lock:order:123")
```

✅ **After（正确做法）**
```python
# 使用 Redlock 或带看门狗的锁实现
import redis
from redis_lock import Lock

with Lock(redis_client, "lock:order:123", expire=30, auto_renewal=True):
    # 业务逻辑
    process_order(123)
# 自动释放，即使异常也会过期
```

**原因**：分布式锁必须满足：互斥性、防死锁（过期时间）、可重入性、看门狗续期。只用 `setnx` 是不够的，应该使用成熟的分布式锁库（Redisson、redis-py-lock）。

## Gotcha 3：缓存穿透 + 雪崩双重打击

**问题**：缓存 key 设置不合理，高并发下缓存同时失效，所有请求直接打到数据库，导致数据库崩溃。

❌ **Before（错误做法）**
```python
# 所有 key 同时过期
redis.setex("user:1", 3600, user_data)  # 1小时过期
redis.setex("user:2", 3600, user_data)  # 同时设置，同时过期

# 查询不存在的数据，每次都穿透到数据库
user = redis.get(f"user:{user_id}")
if not user:
    user = db.query(f"SELECT * FROM users WHERE id = {user_id}")  # 缓存穿透！
    redis.setex(f"user:{user_id}", 3600, user)
```

✅ **After（正确做法）**
```python
# 随机过期时间，避免同时失效
import random
expire_time = 3600 + random.randint(0, 300)  # 3600-3900 秒
redis.setex(f"user:{user_id}", expire_time, user_data)

# 缓存空值，防止穿透
user = redis.get(f"user:{user_id}")
if user == "__NULL__":
    return None  # 数据库确认不存在
if not user:
    user = db.query("SELECT * FROM users WHERE id = %s", (user_id,))
    if not user:
        redis.setex(f"user:{user_id}", 60, "__NULL__")  # 短期缓存空值
    else:
        redis.setex(f"user:{user_id}", expire_time, user)
```

**原因**：缓存雪崩（同时失效）和缓存穿透（查询不存在数据）是高并发系统的经典问题。通过随机过期时间、缓存空值、布隆过滤器可以有效防御。

## Gotcha 4：异步任务丢失——只发不确认

**问题**：消息发送到队列就认为成功，不等待消费者确认，导致消息丢失而不自知。

❌ **Before（错误做法）**
```python
# 发送消息后立即返回，不管是否成功
rabbitmq.publish("order_queue", order_data)
return {"status": "success"}  # 可能消息根本没发出去！
```

✅ **After（正确做法）**
```python
# 使用发布确认（Publisher Confirm）机制
channel.confirm_delivery()
try:
    channel.basic_publish(
        exchange='',
        routing_key='order_queue',
        body=json.dumps(order_data),
        properties=pika.BasicProperties(delivery_mode=2)  # 持久化
    )
    # 等待确认
    if channel.wait_for_confirms(timeout=5):
        return {"status": "success"}
except Exception as e:
    # 记录失败，进入重试或死信队列
    logger.error(f"Message publish failed: {e}")
    return {"status": "failed", "retry": True}
```

**原因**：消息队列的"发后即忘"模式在网络抖动或 Broker 故障时会丢失消息。必须使用发布确认（Publisher Confirm）和消费者确认（Consumer Ack）机制保证消息可靠传递。

## Gotcha 5：连接池耗尽导致级联故障

**问题**：连接池配置不当，慢查询或长事务占用连接不释放，导致新请求无法获取连接，服务全面瘫痪。

❌ **Before（错误做法）**
```python
# 连接池配置过小，且没有超时设置
pool = redis.ConnectionPool(max_connections=10)  # 只有 10 个连接！

# 长事务占用连接
def process():
    conn = db.get_connection()
    result = conn.query("SELECT * FROM huge_table")  # 慢查询，占用连接 30 秒
    time.sleep(10)  # 业务处理
    conn.commit()  # 连接一直不释放
```

✅ **After（正确做法）**
```python
# 合理配置连接池大小（通常 = 核心数 * 2 + 有效磁盘数）
pool = redis.ConnectionPool(
    max_connections=50,
    timeout=5,  # 获取连接超时 5 秒
    retry_on_timeout=True
)

# 使用上下文管理器确保连接释放
def process():
    with db.get_connection() as conn:
        conn.execute("SET statement_timeout = '5s'")  # 查询超时 5 秒
        result = conn.query("SELECT * FROM huge_table LIMIT 100")
        # 连接自动释放
```

**原因**：连接池是稀缺资源，配置不当会引发级联故障。正确配置：连接池大小 = (核心数 * 2) + 有效磁盘数，必须设置获取超时和查询超时，使用上下文管理器确保释放。
