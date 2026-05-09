# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：工具描述不清导致LLM误调用

**问题**：工具描述过于简单或模糊，LLM无法准确判断何时调用，导致错误调用或遗漏调用。

❌ **Before（错误做法）**
```json
{
  "name": "query",
  "description": "Query the database",
  "parameters": {...}
}
```

✅ **After（正确做法）**
```json
{
  "name": "query_user_orders",
  "description": "Query a user's order history from the e-commerce database. Use this when the user asks about their past orders, order status, or purchase history. Returns a list of orders with items, prices, and status. Requires user_id parameter.",
  "parameters": {...}
}
```

**原因**：LLM仅通过工具描述决定是否调用。描述必须包含：功能说明、使用场景、返回值、必要参数。模糊描述会导致LLM在不该调用时调用，或该调用时未调用。

---

## Gotcha 2：参数验证缺失导致安全问题

**问题**：服务端未严格验证LLM传入的参数，导致SQL注入、路径遍历等安全漏洞。

❌ **Before（错误做法）**
```python
# 直接将用户输入拼接到SQL中
def query_data(table_name):
    sql = f"SELECT * FROM {table_name}"
    return db.execute(sql)
```

✅ **After（正确做法）**
```python
# 严格验证参数，使用参数化查询
ALLOWED_TABLES = ["users", "orders", "products"]

def query_data(table_name: str):
    if table_name not in ALLOWED_TABLES:
        raise ValueError(f"Invalid table: {table_name}")
    sql = "SELECT * FROM {}".format(table_name)  # 仍需谨慎，最好使用ORM
    return db.execute(sql)
```

**原因**：LLM可能生成意外参数（如用户提示注入导致LLM生成恶意参数）。服务端必须像对待普通用户输入一样严格验证所有参数。

---

## Gotcha 3：错误信息不友好导致LLM无法处理

**问题**：工具返回的错误信息过于技术化或模糊，LLM无法理解失败原因，无法决定下一步行动。

❌ **Before（错误做法）**
```json
{
  "error": "500 Internal Server Error"
}
```

✅ **After（正确做法）**
```json
{
  "error": {
    "type": "validation_error",
    "message": "The 'start_date' parameter must be in YYYY-MM-DD format. Received: '2024/01/01'",
    "suggestion": "Please provide the date in format '2024-01-01' and retry.",
    "parameter": "start_date",
    "retryable": true
  }
}
```

**原因**：LLM需要根据错误信息决定是重试、修改参数还是告知用户。友好的错误信息应包含：错误类型、具体信息、修复建议、是否可重试。

---

## Gotcha 4：忽视MCP协议生命周期

**问题**：未正确实现MCP协议的initialize、ping、shutdown等生命周期方法，导致客户端连接失败或异常断开。

❌ **Before（错误做法）**
只实现了tools/list和tools/call，忽略了initialize握手和ping心跳。

✅ **After（正确做法）**
完整实现MCP协议要求的所有方法：initialize（握手协商）、ping（心跳检测）、tools/list（工具列表）、tools/call（工具调用）、resources/list（资源列表）、prompts/list（提示词列表），以及对应的shutdown清理逻辑。

**原因**：MCP协议定义了完整的客户端-服务器交互生命周期。跳过关键步骤会导致连接不稳定、客户端无法发现能力、资源泄漏等问题。
