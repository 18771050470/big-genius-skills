# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：工具调用循环导致无限递归

**问题**：Agent 设计不当导致工具调用陷入无限循环（如反复查询同一 API、自我调用），消耗大量资源且无法自行终止。

❌ **Before（错误做法）**
```python
# 无循环检测的 Agent
class Agent:
    def run(self, query):
        while True:  # 危险！可能无限循环
            thought = self.think(query)
            action = self.decide_action(thought)
            result = self.execute(action)
            query = result  # 直接进入下一轮，无终止条件
```

✅ **After（正确做法）**
```python
class Agent:
    def run(self, query, max_steps=10):
        steps = 0
        visited_actions = set()  # 记录已执行的动作
        
        while steps < max_steps:
            thought = self.think(query)
            action = self.decide_action(thought)
            
            # 循环检测
            action_key = f"{action.tool}:{action.params}"
            if action_key in visited_actions:
                return {"status": "loop_detected", "answer": "检测到循环，请换一种方式提问"}
            visited_actions.add(action_key)
            
            result = self.execute(action)
            
            # 终止条件
            if result.is_final:
                return {"status": "success", "answer": result.content}
            
            query = result
            steps += 1
        
        return {"status": "max_steps_reached", "answer": "思考步数超限，建议简化问题"}
```

**原因**：Agent 的自主性是一把双刃剑。必须通过最大步数限制、动作去重、终止条件检测等机制防止无限循环，确保 Agent 能在合理时间内返回结果。

## Gotcha 2：记忆未做摘要导致上下文溢出

**问题**：Agent 将完整对话历史直接传入 LLM，随着轮次增加，上下文窗口被占满，导致早期关键信息丢失。

❌ **Before（错误做法）**
```python
# 直接传递全部历史
messages = system_prompt + conversation_history  # 可能超过 128K！
response = llm.chat(messages)
```

✅ **After（正确做法）**
```python
class MemoryManager:
    def __init__(self, max_tokens=8000):
        self.max_tokens = max_tokens
        self.short_term = []  # 近期对话
        self.long_term = []   # 摘要记忆
    
    def add_interaction(self, user_msg, assistant_msg):
        self.short_term.append({"user": user_msg, "assistant": assistant_msg})
        
        # 当短期记忆过长时，生成摘要
        if self.token_count(self.short_term) > self.max_tokens * 0.7:
            summary = self.summarize(self.short_term)
            self.long_term.append(summary)
            self.short_term = self.short_term[-3:]  # 保留最近3轮
    
    def get_context(self):
        """构建上下文：系统提示 + 长期摘要 + 近期对话"""
        context = [system_prompt]
        
        if self.long_term:
            context.append({
                "role": "system",
                "content": f"历史摘要：{'\n'.join(self.long_term)}"
            })
        
        # 添加近期对话
        for interaction in self.short_term:
            context.append({"role": "user", "content": interaction["user"]})
            context.append({"role": "assistant", "content": interaction["assistant"]})
        
        return context
```

**原因**：LLM 上下文窗口有限（即使 128K 也会被长对话占满）。必须通过分层记忆（短期+长期摘要）机制，确保关键信息不丢失，同时控制上下文长度。

## Gotcha 3：工具权限未隔离导致安全风险

**问题**：Agent 的所有工具共享同一权限级别，导致低权限任务意外调用高权限工具（如删除数据、修改配置）。

❌ **Before（错误做法）**
```python
# 所有工具平级，无权限控制
tools = [
    search_tool,      # 只读
    read_file_tool,   # 只读
    write_file_tool,  # 写操作
    delete_tool,      # 危险操作
    execute_shell_tool # 极危险
]
# Agent 可能在不适当的场景调用 delete_tool 或 execute_shell_tool
```

✅ **After（正确做法）**
```python
class ToolRegistry:
    def __init__(self):
        self.tools = {
            "search": {"tool": search_tool, "level": "read", "scope": "public"},
            "read_file": {"tool": read_file_tool, "level": "read", "scope": "public"},
            "write_file": {"tool": write_file_tool, "level": "write", "scope": "authorized"},
            "delete": {"tool": delete_tool, "level": "dangerous", "scope": "admin"},
            "execute_shell": {"tool": execute_shell_tool, "level": "dangerous", "scope": "admin"},
        }
    
    def get_available_tools(self, user_level):
        """根据用户级别返回可用工具"""
        permission_map = {
            "guest": ["read"],
            "user": ["read", "write"],
            "admin": ["read", "write", "dangerous"]
        }
        allowed = permission_map.get(user_level, ["read"])
        return [t for t in self.tools.values() if t["level"] in allowed]
    
    def execute(self, tool_name, params, user_level):
        """执行前检查权限"""
        tool_info = self.tools.get(tool_name)
        if not tool_info:
            raise ValueError(f"未知工具: {tool_name}")
        
        available = self.get_available_tools(user_level)
        if tool_info not in available:
            raise PermissionError(f"用户级别 {user_level} 无权使用 {tool_name}")
        
        # 危险操作二次确认
        if tool_info["level"] == "dangerous":
            if not self.confirm_dangerous_operation(tool_name, params):
                return {"status": "cancelled", "reason": "用户取消"}
        
        return tool_info["tool"].execute(params)
```

**原因**：Agent 的工具调用能力必须遵循最小权限原则。不同工具应有不同的权限级别，执行前必须检查权限，危险操作需要二次确认。

## Gotcha 4：未处理工具调用失败导致 Agent 崩溃

**问题**：Agent 假设所有工具调用都会成功，未处理网络超时、API 错误、参数无效等情况，导致整个任务失败。

❌ **Before（错误做法）**
```python
# 直接调用，无错误处理
result = tool.execute(params)  # 可能抛出异常
# 如果失败，整个 Agent 崩溃
```

✅ **After（正确做法）**
```python
from tenacity import retry, stop_after_attempt, wait_exponential

class RobustToolExecutor:
    @retry(
        stop=stop_after_attempt(3),
        wait=wait_exponential(multiplier=1, min=2, max=10),
        retry=lambda e: isinstance(e, (TimeoutError, ConnectionError))
    )
    def execute_with_retry(self, tool, params):
        """带重试的工具调用"""
        return tool.execute(params)
    
    def execute(self, tool, params):
        try:
            result = self.execute_with_retry(tool, params)
            return {
                "status": "success",
                "data": result,
                "tool": tool.name
            }
        except TimeoutError:
            return {
                "status": "timeout",
                "error": f"工具 {tool.name} 调用超时",
                "suggestion": "请稍后重试或检查网络连接"
            }
        except ValueError as e:
            return {
                "status": "invalid_params",
                "error": str(e),
                "suggestion": "请检查参数格式是否正确"
            }
        except Exception as e:
            return {
                "status": "error",
                "error": str(e),
                "suggestion": "请联系管理员"
            }
```

**原因**：工具调用（尤其是外部 API）不可避免地会失败。Agent 必须具备健壮的错误处理能力，包括重试、降级、友好错误提示，而不是直接崩溃。
