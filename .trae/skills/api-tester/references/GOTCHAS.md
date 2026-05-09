# Gotchas

> 只写 API 测试容易犯错的**非显而易见的事实**。通用知识不要写。

## Gotcha 1：只验证状态码不验证响应体

**问题**：API 测试只检查 HTTP 200，不验证响应数据结构，导致接口返回空数据或错误结构时测试通过。

❌ **Before（错误做法）**
```python
# 只验证状态码，响应体完全不管
response = requests.get("/api/users/123")
assert response.status_code == 200  # 即使返回 {"error": "not found"} 也通过
```

✅ **After（正确做法）**
```python
# 验证状态码 + 响应结构 + 业务数据
response = requests.get("/api/users/123")
assert response.status_code == 200

# 验证 JSON Schema
data = response.json()
assert "id" in data and data["id"] == 123
assert "name" in data and isinstance(data["name"], str)
assert "email" in data and "@" in data["email"]

# 或使用 jsonschema 验证
from jsonschema import validate
validate(instance=data, schema=USER_SCHEMA)
```

**原因**：状态码只表示 HTTP 层成功，不表示业务逻辑正确。接口可能返回 200 但数据为空或格式错误。必须验证响应结构、字段类型和业务值。

## Gotcha 2：测试数据污染导致用例间依赖

**问题**：测试用例共享数据或执行顺序依赖，导致单独运行失败或随机失败。

❌ **Before（错误做法）**
```python
# 用例 A 创建数据，用例 B 依赖该数据
def test_create_user():
    response = requests.post("/api/users", json={"name": "Alice"})
    assert response.status_code == 201
    # 不清理数据

def test_get_user():
    # 假设用例 A 已创建 Alice
    response = requests.get("/api/users/Alice")
    assert response.status_code == 200  # 单独运行会失败
```

✅ **After（正确做法）**
```python
import pytest

@pytest.fixture
def test_user():
    # 每个用例独立准备数据
    user = {"name": f"test_{uuid.uuid4().hex[:8]}", "email": f"{uuid.uuid4()}@test.com"}
    response = requests.post("/api/users", json=user)
    user_id = response.json()["id"]
    yield user_id
    # 用例结束后清理
    requests.delete(f"/api/users/{user_id}")

def test_get_user(test_user):
    response = requests.get(f"/api/users/{test_user}")
    assert response.status_code == 200
```

**原因**：用例间依赖是 flaky test 的主要原因。每个用例应独立准备和清理数据，确保任意顺序单独运行都能通过。

## Gotcha 3：忽略 API 版本兼容性测试

**问题**：只测试当前版本 API，不验证版本间兼容性，导致客户端升级后崩溃。

❌ **Before（错误做法）**
```python
# 只测试最新版本
response = requests.get("/api/v2/users/123")
assert response.json()["phone_number"]  # v2 新增字段
```

✅ **After（正确做法）**
```python
# 测试版本兼容性
def test_api_v1_compatibility():
    """验证 v1 客户端能正常解析 v2 响应（忽略未知字段）"""
    response = requests.get("/api/v2/users/123")
    data = response.json()
    
    # v1 必需的字段必须存在
    assert "id" in data
    assert "name" in data
    assert "email" in data
    
    # v2 新增字段不应影响 v1 解析（客户端应忽略未知字段）
    # 验证响应包含 Content-Type 和版本信息
    assert response.headers.get("API-Version") == "2.0"

def test_deprecated_fields_still_work():
    """验证已废弃字段仍可用（给客户端迁移时间）"""
    response = requests.get("/api/v2/users/123")
    data = response.json()
    
    # 即使 phone 已废弃为 phone_number，旧字段仍应可用
    if "phone" in data:
        assert data["phone"] == data.get("phone_number", "")
```

**原因**：API 变更是最常见的破坏性变更之一。必须测试向后兼容性，确保旧客户端在新版本下仍能工作，或至少优雅降级。

## Gotcha 4：未测试超时和降级场景

**问题**：API 测试只在理想网络环境下执行，未测试超时、服务降级、依赖故障等异常场景。

❌ **Before（错误做法）**
```python
# 只在正常环境下测试
response = requests.get("/api/orders/123")
assert response.status_code == 200
```

✅ **After（正确做法）**
```python
# 测试超时场景
response = requests.get("/api/orders/123", timeout=0.001)  # 强制超时
assert response.status_code == 504  # 网关超时

# 测试依赖服务故障（使用 mock 或故障注入）
def test_when_payment_service_down():
    with mock.patch('services.payment_client.charge', side_effect=ConnectionError):
        response = requests.post("/api/orders", json={"items": [1, 2, 3]})
        # 应返回友好错误，而非 500 崩溃
        assert response.status_code == 503
        assert "payment" in response.json()["message"].lower()

# 测试降级场景
def test_circuit_breaker_open():
    # 连续失败触发熔断
    for _ in range(10):
        requests.get("/api/unstable-service")
    
    # 熔断后应快速失败，而非长时间等待
    start = time.time()
    response = requests.get("/api/unstable-service")
    assert time.time() - start < 1  # 快速失败
    assert response.status_code == 503
```

**原因**：生产环境网络不稳定、依赖服务故障是常态。API 必须优雅处理超时和降级，测试应覆盖这些场景以确保系统韧性。
