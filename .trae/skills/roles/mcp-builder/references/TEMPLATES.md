# 技术交付物模板

## MCP服务器代码模板

```python
# server.py - MCP服务器示例
from mcp.server import Server
from mcp.types import TextContent, Tool
import json

# 创建服务器实例
server = Server("my-mcp-server")

# 定义工具列表
@server.list_tools()
async def list_tools():
    return [
        Tool(
            name="query_data",
            description="""
            Query data from the database.
            Use this when the user asks for data queries, reports, or analytics.
            Returns JSON formatted results.
            Requires: table_name (str), filters (dict, optional).
            """,
            inputSchema={
                "type": "object",
                "properties": {
                    "table_name": {
                        "type": "string",
                        "description": "Name of the table to query",
                        "enum": ["users", "orders", "products"]
                    },
                    "filters": {
                        "type": "object",
                        "description": "Optional filters to apply",
                        "properties": {
                            "limit": {"type": "integer", "default": 100}
                        }
                    }
                },
                "required": ["table_name"]
            }
        )
    ]

# 实现工具调用
@server.call_tool()
async def call_tool(name: str, arguments: dict):
    if name == "query_data":
        # 参数验证
        table_name = arguments.get("table_name")
        if table_name not in ["users", "orders", "products"]:
            return [TextContent(
                type="text",
                text=json.dumps({
                    "error": {
                        "type": "validation_error",
                        "message": f"Invalid table: {table_name}",
                        "suggestion": "Use one of: users, orders, products",
                        "retryable": True
                    }
                })
            )]
        
        # 执行查询
        try:
            result = await query_database(table_name, arguments.get("filters", {}))
            return [TextContent(
                type="text",
                text=json.dumps({"data": result})
            )]
        except Exception as e:
            return [TextContent(
                type="text",
                text=json.dumps({
                    "error": {
                        "type": "execution_error",
                        "message": str(e),
                        "suggestion": "Please check your parameters and retry",
                        "retryable": True
                    }
                })
            )]

if __name__ == "__main__":
    server.run()
```

---

## 工具定义模板

```json
{
  "name": "[tool_name]",
  "description": "[清晰的功能说明。使用此工具当用户需要XX时。返回YY格式的结果。需要ZZ参数。]",
  "inputSchema": {
    "type": "object",
    "properties": {
      "[param1]": {
        "type": "[string/integer/boolean/object]",
        "description": "[参数说明，包含格式要求和示例]",
        "[enum]": ["[可选值1]", "[可选值2]"],
        "[default]": "[默认值]"
      },
      "[param2]": {
        "type": "[type]",
        "description": "[说明]"
      }
    },
    "required": ["[param1]"]
  }
}
```

---

## MCP集成测试模板

```markdown
# MCP服务器测试方案

## 功能测试

### 测试 1：工具列表获取
**输入**：请求 tools/list
**预期输出**：返回所有已注册工具的完整定义
**验证点**：
- [ ] 工具名称正确
- [ ] 描述完整清晰
- [ ] 参数Schema完整

### 测试 2：正常工具调用
**输入**：调用 [tool_name]，参数 [valid_params]
**预期输出**：返回正确结果
**验证点**：
- [ ] 返回格式符合预期
- [ ] 数据正确
- [ ] 无错误信息

### 测试 3：参数验证
**输入**：调用 [tool_name]，参数 [invalid_params]
**预期输出**：返回验证错误
**验证点**：
- [ ] 错误类型正确
- [ ] 错误信息清晰
- [ ] 包含修复建议
- [ ] retryable标记正确

## 协议测试

### 测试 4：生命周期
**步骤**：
1. 发送 initialize
2. 发送 ping
3. 发送 tools/list
4. 发送 tools/call
5. 发送 shutdown

**验证点**：
- [ ] 每个步骤响应正确
- [ ] 无协议错误

## 安全测试

### 测试 5：输入验证
**输入**：包含特殊字符、超长字符串、SQL注入尝试的参数
**验证点**：
- [ ] 恶意输入被拒绝
- [ ] 服务端无异常
- [ ] 返回友好错误信息

### 测试 6：权限控制
**输入**：未授权用户调用受限工具
**验证点**：
- [ ] 返回权限错误
- [ ] 不执行受限操作
```
