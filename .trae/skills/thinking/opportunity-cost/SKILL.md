---
name: opportunity-cost
description: |
  触发：当需要在多个选项间分配有限资源、需要评估选择的真实代价、需要识别被放弃选项的价值时调用；常见信号包括"选A还是选B"、"资源有限只能做一个"、"做了这个就不能做那个"。
  不触发：当资源充足、可同时执行所有选项时；当只需评估单个选项绝对价值、无需比较时；当选项间互不影响、无资源竞争时。
  Invoke when needing to allocate limited resources among multiple options, evaluate the true cost of choices, or identify the value of foregone alternatives.
  Do NOT invoke when resources are sufficient to execute all options, when only evaluating single option absolute value without comparison, or when options do not compete for resources.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["sunk-cost-fallacy", "trade-off-analysis", "decision-tree", "bayesian-updating"]
---

# 机会成本思维（Opportunity Cost Thinking）

## 核心定义

选择某个选项的真实代价是放弃的其他选项中价值最高的那个。von Wieser在1914年提出：成本不是花费的金钱，而是放弃的替代用途。机会成本是经济学核心概念，提醒我们资源有限，每个选择都有代价。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充所有可行选项、资源约束和各选项预期收益
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确各选项机会成本且最优选择清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别所有可行选项

- 当前有哪些可行选项？（至少列出3个）
- 每个选项需要什么资源？（时间、金钱、人力、注意力）
- 资源约束是什么？为什么不能同时做所有选项？
- 标注每个选项的预期收益和成本

---

### Step 2: 计算机会成本

- 如果选择A，放弃的选项中价值最高的是哪个？
- 机会成本 = 放弃的最佳替代选项的预期收益
- 机会成本不仅包括金钱，还包括时间、注意力、声誉
- 量化机会成本：用统一单位（如金额、时间）比较

---

### Step 3: 比较净收益

- 各选项净收益 = 预期收益 - 直接成本 - 机会成本
- 选择净收益最高的选项
- 考虑非货币因素：风险、不确定性、战略价值
- 评估选择的可逆性：选择后能否改变？

---

### Step 4: 评估长期影响

- 当前选择对未来选项的影响？
- 是否有路径依赖？（当前选择限制未来选择）
- 是否有复合效应？（小选择长期积累成大影响）
- 是否保持选择开放性？（在不确定环境中，保持灵活性有价值）

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **没有免费的选择**：每个选择都有代价，即使不花钱也花时间。原因：资源有限，投入A就不能投入B，B的价值是选择A的真实成本。
2. **机会成本常被忽视**：人们倾向于只考虑直接成本，忽视放弃的替代选项价值。原因：直接成本可见，机会成本不可见，大脑偏好处理可见信息。
3. **时间是最稀缺资源**：时间的机会成本最高，因为时间不可再生。原因：金钱可以赚回，时间不能，时间投入的机会成本是永久性的。
4. **保持选择开放性有价值**：在不确定环境中，延迟决策以保持灵活性可能比立即决策更有价值。原因：未来信息可能改变选项价值，灵活性本身有价值。

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
- [ ] 所有可行选项是否被完整识别？
- [ ] 机会成本是否被量化？
- [ ] 各选项净收益是否被比较？
- [ ] 长期影响和路径依赖是否被评估？
- [ ] 是否考虑了保持选择开放性的价值？
- [ ] 输出具体可执行，不含模糊建议（如"权衡利弊"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [sunk-cost-fallacy](../thinking/sunk-cost-fallacy/SKILL.md) | 互补 | 沉没成本关注历史投入，机会成本关注未来放弃的选项 |
| [trade-off-analysis](../thinking/trade-off-analysis/SKILL.md) | 并行 | 权衡分析提供多选项比较的具体方法 |
| [decision-tree](../thinking/decision-tree/SKILL.md) | 并行 | 决策树可视化各选项路径和预期收益 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 贝叶斯更新根据新信息调整选项预期收益 |

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

1. von Wieser, F. (1914). *Theorie der gesellschaftlichen Wirtschaft* (Theory of Social Economy).
2. Mankiw, N. G. (2020). *Principles of Economics* (9th ed.). Cengage Learning. (Chapter 1: Ten Principles of Economics)
3. Dixit, A. K., & Pindyck, R. S. (1994). *Investment Under Uncertainty*. Princeton University Press.
4. Schwartz, A. (1992). Opportunity cost and the behavior of the firm. *Journal of Political Economy*, 100(2), 271-294.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
