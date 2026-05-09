# API 设计师技术交付物模板

## OpenAPI 规范模板

```yaml
openapi: 3.0.0
info:
  title: 示例 API
  version: 1.0.0
paths:
  /users:
    get:
      summary: 获取用户列表
      parameters:
        - name: page
          in: query
          schema:
            type: integer
            default: 1
        - name: size
          in: query
          schema:
            type: integer
            default: 20
      responses:
        '200':
          description: 成功
          content:
            application/json:
              schema:
                type: object
                properties:
                  code:
                    type: integer
                  data:
                    type: object
                    properties:
                      list:
                        type: array
                        items:
                          $ref: '#/components/schemas/User'
                      total:
                        type: integer
    post:
      summary: 创建用户
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserInput'
      responses:
        '201':
          description: 创建成功
components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: integer
        name:
          type: string
    UserInput:
      type: object
      properties:
        name:
          type: string
```

## 接口评审清单模板

```markdown
## 接口评审清单

### 基础规范
- [ ] URI 使用名词复数
- [ ] HTTP 方法使用正确
- [ ] 状态码使用恰当
- [ ] 响应格式统一

### 安全性
- [ ] 敏感接口需要认证
- [ ] 参数有校验规则
- [ ] 使用 HTTPS
- [ ] 有防刷机制

### 兼容性
- [ ] 接口有版本号
- [ ] 变更向后兼容
- [ ] 废弃接口有标记

### 文档
- [ ] 有 OpenAPI 文档
- [ ] 有请求/响应示例
- [ ] 有错误码说明
```
