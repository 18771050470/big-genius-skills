---
name: react
description: |
  触发：当任务需要与外部世界交互（搜索、计算、API调用）、需要验证推理假设、或问题需要实时信息时；常见信号包括"搜索..."、"计算..."、"验证..."、"执行..."、"工具调用"。
  不触发：当问题完全基于内部知识可解决、当外部交互成本过高、当实时性非必需且内部知识足够可靠时。
  Invoke when tasks require interaction with external world, verifying reasoning assumptions, or needing real-time information.
  Do NOT invoke when the problem can be solved purely with internal knowledge, when external interaction costs are prohibitive, or when real-time info is unnecessary.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["chain-of-thought", "tool-use", "closed-loop-thinking", "observability-thinking"]
---

# ReAct: 推理+行动框架 (Reasoning + Acting)

## 核心定义

通过交替生成推理轨迹（Thought）和任务特定行动（Action），使语言模型能够进行动态推理、与外部环境交互、并根据观察结果调整策略的协同推理范式。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充工具使用权限或行动约束
- **发现矛盾**：当行动结果与推理预期严重不符时，停止并重新评估策略
- **提前终止**：当目标达成或确认当前路径不可行时

---

## 思考流程

### Step 1: 目标理解与任务分解

- 明确最终目标是什么
- 将目标分解为可执行的子任务
- 识别需要外部信息或工具支持的环节
- 规划可能的行动序列

---

### Step 2: 推理轨迹生成（Thought）

- 分析当前状态和已掌握信息
- 推理下一步应该采取什么行动
- 预测行动的可能结果
- 制定或调整行动计划

---

### Step 3: 行动执行（Action）

- 根据推理结果选择具体行动
- 行动类型包括：搜索、计算、API调用、代码执行等
- 明确行动的输入参数
- 执行行动并获取结果

---

### Step 4: 观察处理（Observation）

- 接收并解析行动返回的结果
- 评估结果是否符合预期
- 识别新获得的信息和洞察
- 标注不确定性和信息缺口

---

### Step 5: 循环迭代

- 基于新观察更新对问题的理解
- 生成新的推理轨迹
- 决定下一步行动
- 重复 Thought → Action → Observation 循环

---

### Step 6: 终止与总结

- 判断是否达成目标或达到终止条件
- 整合所有推理轨迹和观察结果
- 形成最终答案或结论
- 输出应包含：结论 + 行动轨迹 + 关键观察 + 最终推理

---

## 关键原则

1. **推理驱动行动**：每个行动都应有明确的推理支撑。原因：无推理的行动是盲目的，推理确保行动有目的性。

2. **观察反馈闭环**：行动结果必须被观察并用于调整后续推理。原因：闭环反馈使系统能够适应环境变化。

3. **增量式解决**：通过小步快跑逐步逼近目标。原因：大步可能出错且难恢复，小步允许及时调整。

4. **工具理性**：选择合适的工具解决特定子问题。原因：不同工具有不同优势，工具组合发挥各自长处。

5. **容错恢复**：行动失败时能够恢复并尝试替代方案。原因：外部交互必然存在失败可能，容错确保鲁棒性。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**ReAct 特有关键检查项**：

- [ ] **每个行动是否有明确的推理支撑？** 还是盲目执行？
- [ ] **是否形成了 Thought → Action → Observation 的完整闭环？**
- [ ] **观察结果是否被用于调整后续推理？** 还是被忽略？
- [ ] **工具选择是否合理？** 是否使用了最适合的工具？
- [ ] **当行动失败时是否有恢复机制？**
- [ ] **循环终止条件是否明确？** 避免无限循环

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [chain-of-thought](../thinking/chain-of-thought/SKILL.md) | 基础 | ReAct在CoT基础上增加了行动维度 |
| [closed-loop-thinking](../thinking/closed-loop-thinking/SKILL.md) | 并行 | 闭环思维提供反馈机制的理论基础 |
| [observability-thinking](../thinking/observability-thinking/SKILL.md) | 并行 | 可观测性思维指导如何设计有效的观察点 |
| [tool-use](../thinking/tool-use/SKILL.md) | 并行 | 工具使用提供具体的技术实现 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing Reasoning and Acting in Language Models. *arXiv preprint arXiv:2210.03629*.
2. Yao, S., He, D., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). Retroformer: Retrospective Large Language Agents with Policy Gradient Optimization. *arXiv preprint arXiv:2308.02151*.
3. Schick, T., Dwivedi-Yu, J., Dessì, R., Raileanu, R., Lomeli, M., Zettlemoyer, L., Cancedda, N., & Scialom, T. (2023). Toolformer: Language Models Can Teach Themselves to Use Tools. *Advances in Neural Information Processing Systems*, 36.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
