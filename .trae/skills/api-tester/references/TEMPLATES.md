# 技术交付物模板

## 交付物模板 1：API 测试用例

```markdown
# API 测试用例：[接口名称]

## 接口信息
- **路径**：`[METHOD] /api/v1/[path]`
- **功能**：[一句话描述]
- **作者**：[姓名]
- **日期**：[日期]

## 测试用例

### TC-001：正常流程
| 步骤 | 操作 | 预期结果 |
|------|------|---------|
| 1 | 发送请求：`[请求示例]` | 状态码：200 |
| 2 | - | 响应包含字段：[字段列表] |
| 3 | - | 响应数据：[预期值] |

### TC-002：缺少必填参数
| 步骤 | 操作 | 预期结果 |
|------|------|---------|
| 1 | 发送请求，省略 `[必填字段]` | 状态码：400 |
| 2 | - | 错误信息包含 `[字段名] is required` |

### TC-003：非法参数值
| 步骤 | 操作 | 预期结果 |
|------|------|---------|
| 1 | 发送请求，`[字段]` = `[非法值]` | 状态码：400/422 |
| 2 | - | 错误信息说明参数非法原因 |
```

## 交付物模板 2：API 测试脚本（REST Assured）

```java
// UserApiTest.java
public class UserApiTest {
    
    @BeforeAll
    public static void setup() {
        RestAssured.baseURI = System.getProperty("api.base.url", "https://api.example.com");
        RestAssured.authentication = oauth2("access_token");
    }
    
    @Test
    @DisplayName("获取用户详情 - 正常流程")
    public void testGetUser_Success() {
        given()
            .pathParam("userId", 123)
        .when()
            .get("/api/v1/users/{userId}")
        .then()
            .statusCode(200)
            .body("id", equalTo(123))
            .body("name", notNullValue())
            .body("email", matchesPattern(".*@.*\\..*"))
            .body("createdAt", matchesPattern("\\d{4}-\\d{2}-\\d{2}T.*"));
    }
    
    @Test
    @DisplayName("获取用户详情 - 用户不存在")
    public void testGetUser_NotFound() {
        given()
            .pathParam("userId", 999999)
        .when()
            .get("/api/v1/users/{userId}")
        .then()
            .statusCode(404)
            .body("code", equalTo("USER_NOT_FOUND"))
            .body("message", containsString("999999"));
    }
    
    @Test
    @DisplayName("创建用户 - 参数校验")
    public void testCreateUser_Validation() {
        given()
            .contentType(ContentType.JSON)
            .body("{\"name\": \"\", \"email\": \"invalid-email\"}")
        .when()
            .post("/api/v1/users")
        .then()
            .statusCode(400)
            .body("errors", hasSize(greaterThanOrEqualTo(2)))
            .body("errors.field", hasItems("name", "email"));
    }
}
```

## 交付物模板 3：API 性能测试脚本（k6）

```javascript
// api-load-test.js
import http from 'k6/http';
import { check, sleep } from 'k6';
import { Rate } from 'k6/metrics';

const errorRate = new Rate('errors');

export const options = {
  stages: [
    { duration: '2m', target: 100 },   // 渐进到 100 用户
    { duration: '5m', target: 100 },   // 稳定 100 用户
    { duration: '2m', target: 200 },   // 渐进到 200 用户
    { duration: '5m', target: 200 },   // 稳定 200 用户
    { duration: '2m', target: 0 },     // 降载
  ],
  thresholds: {
    http_req_duration: ['p(95)<200'],   // 95% 请求 < 200ms
    errors: ['rate<0.1'],                // 错误率 < 10%
  },
};

export default function () {
  const payload = JSON.stringify({
    name: `User_${__VU}_${__ITER}`,
    email: `user_${__VU}_${__ITER}@test.com`,
  });
  
  const headers = { 'Content-Type': 'application/json' };
  const res = http.post('https://api.example.com/v1/users', payload, { headers });
  
  const success = check(res, {
    'status is 201': (r) => r.status === 201,
    'response time < 200ms': (r) => r.timings.duration < 200,
  });
  
  errorRate.add(!success);
  sleep(1);
}
```

## 交付物模板 4：API 测试报告

```markdown
# API 测试报告：[版本号]

## 执行概况
- **接口总数**：[N]
- **用例总数**：[N]
- **通过率**：[N]% ([通过]/[总数])
- **执行时间**：[时长]

## 接口覆盖
| 接口 | 方法 | 用例数 | 通过 | 失败 |
|------|------|--------|------|------|
| /api/v1/users | GET | 5 | 5 | 0 |
| /api/v1/users | POST | 8 | 7 | 1 |

## 性能指标
| 接口 | P50 | P95 | P99 | 吞吐量 |
|------|-----|-----|-----|--------|
| GET /users/{id} | 45ms | 120ms | 200ms | 500/s |
| POST /users | 80ms | 250ms | 400ms | 200/s |

## 问题清单
| 优先级 | 接口 | 问题 | 状态 |
|--------|------|------|------|
| 🔴 高 | POST /users | 并发创建重复用户 | 待修复 |

## 附件
- [详细测试日志]
- [性能测试图表]
```
