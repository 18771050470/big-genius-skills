---
name: zero-risk-bias
description: |
  触发：当需要评估是否偏好完全消除小风险而非大幅降低大风险、需要识别"零风险偏好"偏差、需要优化风险降低资源分配时调用；常见信号包括"完全消除这个风险"、"100%安全"、"宁可多花钱也要零风险"。
  不触发：当只需描述风险偏好、无需优化资源分配时；当零风险确实可行且成本合理时；当只需定性比较风险、无需量化分析时。
  Invoke when needing to evaluate whether complete elimination of small risks is preferred over large risk reduction, identify "zero risk preference" bias, or optimize risk reduction resource allocation.
  Do NOT invoke when only describing risk preferences without optimizing resource allocation, when zero risk is truly feasible and cost-effective, or when only qualitatively comparing risks without quantitative analysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["prospect-theory", "loss-aversion", "cost-benefit-analysis", "probabilistic-thinking"]
---

# 零风险偏差思维（Zero Risk Bias Thinking）

## 核心定义

人们偏好完全消除小风险，而非大幅降低大风险，即使后者节省更多总风险。Viscusi等人在1987年证明：人们愿意为将风险从5%降到0%支付比从55%降到50%更多，尽管两者都降低5%。零风险的心理价值远超其实际风险降低价值。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充各风险的概率、严重程度和降低成本数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别零风险偏差影响且优化方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别零风险信号

- 是否出现"完全消除这个风险"、"100%安全"、"宁可多花钱也要零风险"等表述？
- 是否偏好将小风险降到0%？
- 是否愿意为消除小风险支付不成比例的成本？
- 是否忽视了降低大风险的选项？

---

### Step 2: 评估风险降低效率

- 选项A：将风险从X%降到0%，成本C1
- 选项B：将风险从Y%降到(Y-Δ)%，成本C2
- 每降低1%风险的成本：C1/X vs C2/Δ
- 总风险降低量：哪个选项降低更多绝对风险？

---

### Step 3: 分析心理机制

- 零风险消除焦虑：0%风险感觉"安全"，任何正风险感觉"危险"
- 确定性偏好：确定性结果被过度加权
- 情绪驱动：恐惧驱动零风险偏好，非理性计算
- 框架效应："100%安全"比"降低5%风险"更有吸引力

---

### Step 4: 优化风险降低

- 计算各选项的风险-成本效率
- 优先降低大风险（绝对风险降低最多）
- 使用期望值：风险概率 × 严重程度
- 设计风险降低组合：有限资源下最大化总风险降低

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **零风险心理价值≠实际价值**：0%风险的心理安慰远超其实际风险降低。原因：大脑将"0%"视为质变，任何正风险都触发焦虑，即使概率极小。
2. **大风险降低效率更高**：降低大风险的绝对收益通常高于消除小风险。原因：大风险的期望值损失更大，降低大风险节省更多预期损失。
3. **资源有限需优化**：有限资源下，应最大化总风险降低而非追求零风险。原因：追求零风险消耗过多资源，减少其他风险降低投入。
4. **期望值计算是解药**：用风险概率×严重程度计算期望值，替代直觉判断。原因：期望值客观比较不同风险降低选项的真实价值。

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
- [ ] 是否识别了零风险信号？
- [ ] 是否评估了风险降低效率（成本/风险降低量）？
- [ ] 是否分析了心理驱动机制？
- [ ] 是否使用期望值计算优化？
- [ ] 是否设计了风险降低组合？
- [ ] 输出具体可执行，不含模糊建议（如"降低风险"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [prospect-theory](../thinking/prospect-theory/SKILL.md) | 前置 | 前景理论解释确定性偏好和概率加权 |
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 前置 | 损失厌恶使任何正风险感觉像损失 |
| [cost-benefit-analysis](../thinking/cost-benefit-analysis/SKILL.md) | 前置 | 成本效益分析提供风险降低效率计算框架 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供期望值计算方法 |

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

1. Viscusi, W. K., Magat, W. A., & Huber, J. (1987). An investigation of the rationality of consumer valuations of multiple health risks. *RAND Journal of Economics*, 18(4), 565-579.
2. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 28: Good Times and Bad Times)
3. Baron, J., Gould, J., & Spranca, M. (1993). The zero-risk bias: A preference for complete risk reduction. *Journal of Risk and Uncertainty*, 6(1), 5-16.
4. Gigerenzer, G. (2004). Dread risk, September 11, and fatal traffic accidents. *Psychological Science*, 15(4), 286-287.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
