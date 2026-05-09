---
name: leverage-thinking
description: |
  触发：当需要找到投入产出比最高的干预点、资源有限需优先分配、寻找"四两拨千斤"的解决方案时调用；常见信号包括"做什么事能带来最大改变"、"资源有限应该先投哪里"、"有没有事半功倍的方法"。
  不触发：当所有行动同等重要、无明显优先级差异时；当只需按部就班执行、无需寻找捷径时；当杠杆点已被明确识别、只需执行时。
  Invoke when needing to find the highest ROI intervention points, prioritizing limited resources, or seeking "maximum impact with minimum effort" solutions.
  Do NOT invoke when all actions are equally important without priority differences, when only step-by-step execution is needed without seeking shortcuts, or when leverage points are already clearly identified and only execution remains.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["system-thinking", "constraint-thinking", "opportunity-cost", "pareto-principle"]
---

# 杠杆思维（Leverage Thinking）

## 核心定义

识别系统中投入产出比最高的干预点，用最小资源撬动最大改变。核心公式：杠杆效应 = 影响幅度 × 影响持久度 / 投入成本。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充可用资源、约束条件和目标
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已找到明确的高杠杆点且行动方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 列出所有可行行动

- 穷举当前可采取的所有行动
- 不预设优先级，保持开放
- 标注每个行动所需的资源（时间、资金、人力）
- 排除明显不可行的行动

---

### Step 2: 评估影响幅度

- 每个行动能影响多少人/多少系统组件？
- 影响是局部的还是全局的？
- 影响是表面的还是根本的？
- 量化影响范围：影响人数、影响金额、影响系统比例

---

### Step 3: 评估影响持久度

- 影响是一次性的还是持续性的？
- 影响是否会随时间衰减或增强？
- 是否会产生连锁反应（触发其他正向变化）？
- 标注每个影响的半衰期

---

### Step 4: 计算杠杆率并排序

- 杠杆率 = (影响幅度 × 影响持久度) / 投入成本
- 按杠杆率从高到低排序所有行动
- 识别前20%的高杠杆行动（帕累托原则）
- 检查高杠杆行动之间的依赖关系：是否需要先做A才能做B

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **杠杆点不总是显而易见的**：最高杠杆的行动往往不是最紧急的。原因：紧急事务消耗注意力，但不一定产生最大长期价值。
2. **杠杆率随时间变化**：今天的杠杆点明天可能不是。原因：系统状态变化会改变各行动的影响幅度和成本。
3. **组合杠杆 > 单一杠杆**：多个中等杠杆行动的组合可能超过单一高杠杆行动。原因：行动之间可能产生协同效应。
4. **负杠杆同样存在**：有些行动投入大但产生负面效果。原因：错误方向的"努力"比不努力更糟。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **记录方式**：自检结果写入 `self_check_result.md`（临时文件），包含：通过项、未通过项、修正记录
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**完整检查项**：

- [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
- [ ] 每步思考要点已覆盖，无遗漏
- [ ] 每步结论标注了置信度和反证可能性
- [ ] 所有可行行动是否被穷举？是否有遗漏的高杠杆选项？
- [ ] 影响幅度是否被量化？
- [ ] 影响持久度是否被评估？是否有半衰期估计？
- [ ] 杠杆率计算是否合理？分子分母单位是否一致？
- [ ] 是否识别了负杠杆行动（投入大但产生负面效果）？
- [ ] 高杠杆行动之间的依赖关系是否被标注？
- [ ] 输出具体可执行，不含模糊建议（如"做重要的事"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [system-thinking](../thinking/system-thinking/SKILL.md) | 前置 | 系统思维识别系统结构和反馈回路，杠杆思维在结构中寻找高杠杆点 |
| [constraint-thinking](../thinking/constraint-thinking/SKILL.md) | 并行 | 约束思维识别瓶颈，杠杆思维评估突破瓶颈的投入产出比 |
| [opportunity-cost](../thinking/opportunity-cost/SKILL.md) | 并行 | 机会成本评估放弃的代价，杠杆思维评估选择的收益 |
| [compound-thinking](../thinking/compound-thinking/SKILL.md) | 后置 | 杠杆思维找到高杠杆行动，复利思维评估长期累积效应 |

---

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Meadows, D. H. (2008). *Thinking in Systems: A Primer*. Chelsea Green Publishing. Chapter 3: Places to Intervene in a System.
2. Koch, R. (1997). *The 80/20 Principle: The Secret to Achieving More with Less*. Doubleday.
3. Rumelt, R. (2011). *Good Strategy/Bad Strategy: The Difference and Why It Matters*. Crown Business.
4. Grove, A. S. (1983). *High Output Management*. Random House.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
