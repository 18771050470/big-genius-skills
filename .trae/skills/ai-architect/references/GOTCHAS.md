# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：训练-服务偏差（Training-Serving Skew）

**问题**：训练时和推理时的特征计算逻辑不一致，导致模型在生产环境表现远低于预期，且难以排查。

❌ **Before（错误做法）**
```python
# 训练代码
features = df.groupby('user_id')['amount'].mean()  # Pandas 计算

# 推理代码（API 中）
user_amounts = get_user_orders(user_id)
feature = sum(user_amounts) / len(user_amounts)  # 纯 Python 计算，舍入方式不同
```

✅ **After（正确做法）**
```python
# 统一定义在特征存储中
@feature_view(
    entities=["user_id"],
    ttl=timedelta(hours=24),
    online=True,
)
def user_avg_amount_feature():
    return Feature(
        name="user_avg_amount",
        dtype=ValueType.FLOAT,
        transformation=Aggregation(
            column="amount",
            function="AVG",
            window="30d"
        )
    )

# 训练和推理都通过 Feast 获取同一特征
features = store.get_online_features(
    features=["user_avg_amount"],
    entity_rows=[{"user_id": uid}]
)
```

**原因**：即使计算逻辑看起来相同，不同的执行环境（Pandas vs 纯 Python）、浮点精度、空值处理方式都会导致细微差异。必须通过特征存储（Feast/Tecton）确保训练和推理使用完全相同的特征定义。

## Gotcha 2：模型版本未锁定导致推理结果漂移

**问题**：模型文件或依赖库版本未固定，重新部署后推理结果发生变化，影响业务一致性。

❌ **Before（错误做法）**
```yaml
# 未指定模型版本
model:
  path: s3://models/latest/model.pkl  # "latest" 随时可能变
  framework: sklearn  # 未指定版本
```

✅ **After（正确做法）**
```yaml
model:
  name: fraud-detection-v3.2.1
  artifact_path: s3://models/fraud-detection/v3.2.1/model.pkl
  framework: sklearn==1.3.2
  python_version: "3.10.12"
  requirements_hash: "sha256:abc123..."
  signature:
    inputs: [{name: "feature_vector", type: "tensor", shape: [-1, 128]}]
    outputs: [{name: "probability", type: "tensor", shape: [-1, 1]}]
```

**原因**：ML 模型对依赖版本极其敏感。scikit-learn 1.2 和 1.3 的随机森林实现可能有细微差异，导致预测结果不同。必须通过模型注册中心（MLflow）锁定模型版本、依赖版本和输入输出签名。

## Gotcha 3：未区分在线特征和离线特征导致延迟超标

**问题**：将离线批处理特征直接用于在线推理，导致 P99 延迟从 10ms 飙升到 500ms+。

❌ **Before（错误做法）**
```python
# 推理时实时计算聚合特征
def predict(user_id):
    orders = query_all_user_orders(user_id)  # 查询全量订单！
    avg_amount = sum(o.amount for o in orders) / len(orders)  # 实时计算
    return model.predict([avg_amount, ...])
```

✅ **After（正确做法）**
```python
# 离线预计算 + 在线查表
# 离线作业（每小时更新）
@batch_feature_view(...)
def user_avg_amount_24h():
    return query("""
        SELECT user_id, AVG(amount) as avg_amount
        FROM orders
        WHERE created_at > now() - INTERVAL 24 HOURS
        GROUP BY user_id
    """)

# 在线推理（仅查表，O(1)）
def predict(user_id):
    features = online_store.get("user_avg_amount_24h", user_id)
    return model.predict([features.avg_amount, ...])
```

**原因**：在线推理必须在毫秒级完成，任何实时计算（尤其是涉及全量数据扫描的操作）都会导致延迟不可控。必须通过特征存储的在线/离线双路径设计，将计算移到离线，在线只做 O(1) 查表。

## Gotcha 4：监控只关注基础设施忽略模型性能

**问题**：只监控 CPU/内存/磁盘，未监控模型本身的性能衰减（数据漂移、概念漂移），导致模型 silently fail。

❌ **Before（错误做法）**
```yaml
# 只监控基础设施
alerts:
  - metric: cpu_usage > 80%
  - metric: memory_usage > 85%
  - metric: disk_usage > 90%
# 没有模型性能监控！
```

✅ **After（正确做法）**
```yaml
alerts:
  # 基础设施监控
  - metric: cpu_usage > 80%
  - metric: memory_usage > 85%
  
  # 模型性能监控（关键！）
  - metric: model_accuracy < 0.85  # 准确率下降
  - metric: prediction_drift > 0.1  # 分布漂移
  - metric: feature_drift[age] > 0.05  # 特征漂移
  - metric: null_prediction_rate > 0.01  # 空值率异常
  - metric: latency_p99 > 100ms  # 延迟超标
```

**原因**：ML 模型会随时间退化（数据分布变化、概念漂移），但基础设施指标可能完全正常。必须建立模型层面的监控体系，包括预测分布漂移、特征漂移、准确率衰减等。
