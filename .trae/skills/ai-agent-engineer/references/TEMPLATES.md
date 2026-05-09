# 技术交付物模板

> 提供可直接使用的 Markdown/代码模板。

## 交付物模板 1：Agent 系统设计文档

```markdown
# Agent 系统设计: [Agent 名称]

## 系统架构

```
[用户输入]
    ↓
[输入处理器] → 意图识别 → 实体提取 → 参数校验
    ↓
[规划器] → 任务分解 → 工具选择 → 执行计划
    ↓
[执行器] → 工具调用 → 结果处理 → 状态更新
    ↓
[输出生成器] → 结果整合 → 响应格式化
    ↓
[用户输出]
```

## 组件说明

| 组件 | 职责 | 输入 | 输出 |
|------|------|------|------|
| 输入处理器 | 解析用户输入 | 原始文本 | 结构化意图 |
| 规划器 | 制定执行计划 | 结构化意图 | 执行计划 |
| 执行器 | 调用工具 | 执行计划 | 工具结果 |
| 输出生成器 | 生成响应 | 工具结果 | 最终回复 |

## 状态机设计

```
[Idle] --用户输入--> [Planning]
[Planning] --计划完成--> [Executing]
[Executing] --需要更多信息--> [Clarifying]
[Clarifying] --获得信息--> [Planning]
[Executing] --执行完成--> [Generating]
[Generating] --响应生成--> [Idle]
[Executing] --执行失败--> [ErrorHandling]
[ErrorHandling] --可恢复--> [Planning]
[ErrorHandling] --不可恢复--> [Idle]
```

## 工具清单

| 工具名 | 类型 | 权限 | 描述 |
|--------|------|------|------|
| search | 查询 | read | 搜索引擎 |
| read_file | 查询 | read | 读取文件 |
| write_file | 操作 | write | 写入文件 |
| execute_code | 执行 | dangerous | 执行代码 |
```

## 交付物模板 2：ReAct 循环实现模板

```python
# react_agent.py
from typing import List, Dict, Any, Optional
from dataclasses import dataclass
from enum import Enum

class ActionType(Enum):
    THOUGHT = "thought"
    ACTION = "action"
    OBSERVATION = "observation"
    FINAL = "final"

@dataclass
class Step:
    type: ActionType
    content: str
    tool: Optional[str] = None
    params: Optional[Dict] = None

class ReActAgent:
    """ReAct (Reasoning + Acting) Agent 实现"""
    
    def __init__(self, llm_client, tools, max_steps=10):
        self.llm = llm_client
        self.tools = {t.name: t for t in tools}
        self.max_steps = max_steps
        self.memory = []
    
    def run(self, query: str) -> str:
        """执行 ReAct 循环"""
        self.memory = [Step(ActionType.THOUGHT, f"用户问题: {query}")]
        
        for step in range(self.max_steps):
            # 1. 思考
            thought = self.think()
            self.memory.append(Step(ActionType.THOUGHT, thought))
            
            # 2. 决定行动
            action = self.decide_action(thought)
            
            if action.type == ActionType.FINAL:
                return action.content
            
            self.memory.append(action)
            
            # 3. 执行行动
            observation = self.execute(action)
            self.memory.append(Step(ActionType.OBSERVATION, observation))
        
        return "思考步数超限，未能找到答案"
    
    def think(self) -> str:
        """基于记忆生成思考"""
        prompt = self._build_prompt()
        return self.llm.generate(prompt)
    
    def decide_action(self, thought: str) -> Step:
        """根据思考决定下一步行动"""
        # 解析 LLM 输出，提取行动
        if "最终答案" in thought:
            answer = thought.split("最终答案:")[1].strip()
            return Step(ActionType.FINAL, answer)
        
        # 提取工具调用
        tool_name = self._extract_tool(thought)
        params = self._extract_params(thought)
        
        return Step(ActionType.ACTION, thought, tool_name, params)
    
    def execute(self, action: Step) -> str:
        """执行工具调用"""
        if action.tool not in self.tools:
            return f"错误: 未知工具 {action.tool}"
        
        tool = self.tools[action.tool]
        try:
            result = tool.run(action.params)
            return str(result)
        except Exception as e:
            return f"错误: {str(e)}"
    
    def _build_prompt(self) -> str:
        """构建 ReAct Prompt"""
        history = "\n".join([
            f"{step.type.value}: {step.content}"
            for step in self.memory
        ])
        
        return f"""基于以下思考历史，决定下一步行动：

{history}

可用工具: {', '.join(self.tools.keys())}

请按以下格式输出：
思考: [你的思考过程]
行动: [工具名] [参数]
或者
最终答案: [直接回答用户]
"""
```

## 交付物模板 3：Agent 评估报告

```markdown
# Agent 评估报告: [Agent 名称]

## 评估环境
- **模型**: [GPT-4/Claude-3/...]
- **工具数量**: [N]
- **测试时间**: YYYY-MM-DD

## 功能测试

| 测试场景 | 测试数 | 通过数 | 通过率 | 备注 |
|----------|--------|--------|--------|------|
| 单工具调用 | 50 | 48 | 96% | ... |
| 多工具组合 | 30 | 25 | 83% | ... |
| 错误处理 | 20 | 18 | 90% | ... |
| 边界输入 | 20 | 15 | 75% | ... |

## 性能测试

| 指标 | 目标 | 实测 | 状态 |
|------|------|------|------|
| 平均响应时间 | < 3s | 2.5s | ✅ |
| P99 响应时间 | < 10s | 8s | ✅ |
| 工具调用成功率 | > 95% | 92% | ⚠️ |
| 任务完成率 | > 90% | 88% | ⚠️ |

## 问题分析
1. ...
2. ...

## 优化建议
1. ...
2. ...
```
