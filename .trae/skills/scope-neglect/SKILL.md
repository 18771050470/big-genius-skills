---
name: scope-neglect
description: |
  触发：当需要评估判断是否忽视问题规模、需要识别"1只鸟vs100只鸟支付相同"偏差、需要校正规模敏感决策时调用；常见信号包括"反正都要救"、"大小差不多"、"数量不重要"。
  不触发：当只需定性描述问题、无需规模比较时；当规模确实不影响决策时（经成本效益验证）；当只需识别问题存在、无需量化分析时。
  Invoke when needing to evaluate whether judgments ignore problem scope, identify "1 bird vs 100 birds same payment" bias, or correct scope-sensitive decisions.
  Do NOT invoke when only qualitatively describing problems without scope comparison, when scope truly doesn't affect decisions (verified by cost-benefit analysis), or when only identifying problem existence without quantitative analysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["identifiable-victim-effect", "affect-heuristic", "zero-risk-bias", "cost-benefit-analysis"]
---

# 范围忽视思维（Scope Neglect Thinking）

## 核心定义

人们对问题规模的敏感度不足，支付意愿不随规模线性增长。Kahneman等人在1999年实验证明：人们为拯救2000只鸟、20000只鸟、200000只鸟的支付意愿几乎相同，完全忽视数量级差异。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充问题规模数据、单位成本和规模变化影响
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别范围忽视影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别范围信号

- 是否出现"反正都要救"、"大小差不多"、"数量不重要"等表述？
- 是否对规模变化不敏感？
- 是否支付意愿不随规模增长？
- 是否用定性判断替代定量分析？

---

### Step 2: 评估规模差异

- 问题规模是多少？（数量、范围、影响人数）
- 规模变化多少倍？（10倍？100倍？）
- 单位成本是多少？（每单位资源投入）
- 总影响是多少？（规模 × 单位影响）

---

### Step 3: 分析忽视机制

- 情感麻木：规模增加，情感反应不增加
- 抽象化：大规模数字变得抽象，失去具体性
- 原型思维：用单一原型代表所有规模
- 支付意愿饱和：情感驱动支付意愿，不随规模增长

---

### Step 4: 校正范围忽视

- 使用单位成本分析：每单位资源帮助多少
- 计算总影响：规模 × 单位影响
- 分解大规模：将大规模分解为可理解的小单元
- 设计规模敏感决策框架：支付意愿=规模 × 单位价值

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **规模≠情感**：情感反应不随规模线性增长。原因：大脑情感系统对具体个体反应强烈，对抽象数字麻木，导致"1人vs100人"情感差异远小于100倍。
2. **单位成本是关键**：每单位资源的影响比总规模更重要。原因：单位成本提供可比指标，使不同规模选项可比较。
3. **分解使规模可理解**：将大规模分解为小单元，恢复规模敏感度。原因：具体小单元触发情感反应，使规模差异可感知。
4. **定量分析是解药**：用规模×单位价值计算总影响。原因：定量分析客观比较不同规模选项的真实影响，不受情感麻木影响。

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
- [ ] 是否识别了范围信号？
- [ ] 是否评估了规模差异和倍数？
- [ ] 是否分析了忽视驱动机制？
- [ ] 是否使用单位成本分析？
- [ ] 是否分解大规模为可理解单元？
- [ ] 输出具体可执行，不含模糊建议（如"考虑规模"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [identifiable-victim-effect](../thinking/identifiable-victim-effect/SKILL.md) | 并行 | 可识别受害者效应使具体个体胜过统计群体，范围忽视使规模不敏感 |
| [affect-heuristic](../thinking/affect-heuristic/SKILL.md) | 前置 | 情感启发式解释为何情感反应不随规模增长 |
| [zero-risk-bias](../thinking/zero-risk-bias/SKILL.md) | 并行 | 零风险偏差偏好完全消除小风险，范围忽视忽视规模差异 |
| [cost-benefit-analysis](../thinking/cost-benefit-analysis/SKILL.md) | 前置 | 成本效益分析提供单位成本和总影响计算框架 |

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

1. Kahneman, D., Ritov, I., Jacowitz, K. E., & Grant, P. (1993). Stated willingness to pay for public goods: A psychological analysis. *Psychological Science*, 4(5), 310-315.
2. Kahneman, D., & Knetsch, J. L. (1992). Valuing public goods: The purchase of moral satisfaction. *Journal of Environmental Economics and Management*, 22(1), 57-70.
3. Desvousges, W. H., Johnson, F. R., Dunford, R. W., Boyle, K. J., Hudson, S. P., & Wilson, K. N. (1993). Measuring natural resource damages with contingent valuation: Tests of validity and reliability. In *Contingent Valuation* (pp. 91-159). Springer.
4. Slovic, P. (2007). "If I look at the mass I will never act": Psychic numbing and genocide. *Judgment and Decision Making*, 2(2), 79-95.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
