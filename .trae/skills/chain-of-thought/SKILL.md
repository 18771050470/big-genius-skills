---
name: chain-of-thought
description: |
  触发：当面对多步推理任务、数学问题、逻辑谜题或需要逐步推导的复杂问题时；常见信号包括"一步步思考"、"详细推导"、"解释过程"、"为什么这样"、"中间步骤"。
  不触发：当问题只需单步回答（如事实查询）、当答案显而易见无需推导、当时间紧迫且近似答案可接受时。
  Invoke when facing multi-step reasoning tasks, math problems, logic puzzles, or complex problems requiring step-by-step derivation.
  Do NOT invoke when the problem requires only single-step answers, when the answer is obvious, or when time is critical and approximate answers are acceptable.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["tree-of-thought", "self-reflection", "react", "probabilistic-thinking"]
---

# 思维链推理 (Chain-of-Thought)

## 核心定义

通过显式生成一系列中间推理步骤，将复杂问题分解为连贯的思维链条，使语言模型能够逐步推导并得出正确结论的推理范式。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充问题背景或约束条件
- **发现矛盾**：停止推理，用 AskUserQuestion 向用户报告逻辑矛盾点，等待澄清
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 问题分解与理解

- 仔细阅读并理解问题的核心目标和约束条件
- 识别问题类型（数学计算、逻辑推理、常识推理、代码调试等）
- 将复杂问题分解为若干子问题或子任务
- 标注关键信息和已知条件

---

### Step 2: 构建推理链条

- 确定第一步应该做什么（从已知条件出发）
- 规划中间步骤的逻辑顺序（A → B → C → ...）
- 预估需要的推理步数（通常3-7步）
- 确保每一步都建立在前一步的基础上

---

### Step 3: 逐步执行推理

- 按顺序执行每一步推理
- 每步只处理一个逻辑单元
- 显式写出中间结果和推导依据
- 使用过渡词连接步骤（"首先..."、"然后..."、"因此..."、"由此可得..."）

---

### Step 4: 验证中间结果

- 检查每一步的逻辑一致性
- 验证计算或推导的正确性
- 识别可能的错误来源（计算错误、逻辑跳跃、假设不当）
- 如有错误，回溯到出错步骤重新推导

---

### Step 5: 整合与总结

- 整合所有中间步骤的结论
- 形成最终答案或解决方案
- 回顾整个推理过程，确认无遗漏
- 输出应包含：结论 + 推理过程摘要 + 关键假设 + 置信度评估

---

## 关键原则

1. **显式推导**：每一步推理都必须显式写出，不能跳跃。原因：隐式推理容易导致错误无法追溯，显式推导便于验证和调试。

2. **单步聚焦**：每一步只处理一个逻辑单元，避免多任务混杂。原因：降低认知负荷，提高每步的准确性。

3. **连贯衔接**：步骤之间必须有清晰的逻辑连接。原因：断裂的思维链会导致推理偏离正确方向。

4. **及时验证**：每完成关键步骤后立即验证正确性。原因：早期发现错误比最后才发现成本更低。

5. **回溯修正**：发现错误时不固执于当前路径，勇于回溯。原因：坚持错误路径会导致累积性偏差。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**思维链特有关键检查项**：

- [ ] **是否显式写出了所有中间步骤？** 有无跳跃性推理？
- [ ] **每一步是否有清晰的逻辑依据？** 还是凭空得出？
- [ ] **步骤之间是否有连贯的衔接？** 使用过渡词了吗？
- [ ] **是否验证了关键中间结果的正确性？**
- [ ] **最终结论是否能从第一步逻辑推导得出？** 形成完整链条了吗？
- [ ] **是否标注了推理中的假设和不确定性？**

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [tree-of-thought](../thinking/tree-of-thought/SKILL.md) | 进阶 | 当单一路径推理可能不够，需要探索多条推理路径时 |
| [self-reflection](../thinking/self-reflection-self-critique/SKILL.md) | 后置 | 完成思维链后，用于批判性审视推理过程 |
| [divide-and-conquer](../thinking/divide-and-conquer/SKILL.md) | 前置 | 在构建思维链前，先用分治将问题拆解为子问题 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 在推理过程中遇到不确定性时，动态更新置信度 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Wei, J., Wang, X., Schuurmans, D., Bosma, M., ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. *Advances in Neural Information Processing Systems*, 35, 24824-24837.
2. Kojima, T., Gu, S. S., Reid, M., Matsuo, Y., & Iwasawa, Y. (2022). Large Language Models are Zero-Shot Reasoners. *Advances in Neural Information Processing Systems*, 35, 22199-22213.
3. Wang, X., Wei, J., Schuurmans, D., Le, Q., Chi, E., Narang, S., Chowdhery, A., & Zhou, D. (2022). Self-Consistency Improves Chain of Thought Reasoning in Language Models. *arXiv preprint arXiv:2203.11171*.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
