---
name: ikea-effect
description: |
  触发：当需要评估是否因投入劳动而高估价值、需要识别"自己做的更好"偏差、需要客观评估自制vs外购方案时调用；常见信号包括"我自己做的肯定好"、"花了这么多心血"、"自己人做的更可靠"。
  不触发：当只需描述劳动投入、无需价值评估时；当劳动确实增加价值时（经客观质量验证）；当只需记录制作过程、无需比较价值时。
  Invoke when needing to evaluate whether value is overestimated due to labor投入, identify "self-made is better" bias, or objectively assess make-vs-buy options.
  Do NOT invoke when only describing labor input without value evaluation, when labor truly adds value (verified by objective quality assessment), or when only recording production process without comparing value.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["endowment-effect", "effort-justification", "sunk-cost-fallacy", "overconfidence-effect"]
---

# IKEA效应思维（IKEA Effect Thinking）

## 核心定义

人们对自己参与制作的产品赋予更高价值。Norton等人在2012年证明：参与者对自己组装的宜家家具估值比预组装的高63%，即使质量相同。劳动投入导致情感依恋和价值高估。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充客观质量数据、外部评估和替代方案成本
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别IKEA效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别IKEA信号

- 是否出现"我自己做的肯定好"、"花了这么多心血"、"自己人做的更可靠"等表述？
- 是否因投入劳动而高估价值？
- 是否忽视外部更优方案？
- 是否将劳动投入等同于价值？

---

### Step 2: 评估劳动投入

- 投入了多少劳动？（时间、精力、技能）
- 劳动是否增加实际价值？（质量提升）
- 劳动是否只增加情感价值？（依恋感）
- 外部方案的成本和质量如何？

---

### Step 3: 分析估值偏差

- 客观质量评估 vs 主观估值差异
- 劳动投入与估值的相关性
- 是否期望他人也高估？（错误共识）
- 失败时效应是否消失？（未完成品）

---

### Step 4: 校正IKEA效应

- 使用盲测评估：隐藏来源，只评估质量
- 比较自制vs外购的总成本（含时间成本）
- 邀请第三方客观评估
- 设计决策检查清单：劳动≠价值

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **劳动≠价值**：投入劳动不必然增加客观价值。原因：劳动可能只增加情感依恋，不提升功能质量，盲测中自制品常不如专业品。
2. **成功完成是关键**：只有成功完成的任务才触发IKEA效应。原因：未完成或失败的作品不产生成就感，效应消失，甚至产生负面评价。
3. **总成本比较**：自制成本=材料+时间+机会成本。原因：忽视时间成本导致低估自制真实成本，外购可能更经济。
4. **盲测是解药**：隐藏来源只评估质量。原因：盲测消除情感依恋影响，提供客观质量比较，识别真实价值差异。

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
- [ ] 是否识别了IKEA信号？
- [ ] 是否评估了劳动投入和实际价值？
- [ ] 是否分析了估值偏差？
- [ ] 是否使用盲测或第三方评估校正？
- [ ] 是否比较了自制vs外购总成本？
- [ ] 输出具体可执行，不含模糊建议（如"客观评估"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [endowment-effect](../thinking/endowment-effect/SKILL.md) | 并行 | 禀赋效应因拥有而高估，IKEA效应因劳动而高估 |
| [effort-justification](../thinking/effort-justification/SKILL.md) | 前置 | 努力正当化解释为何劳动导致价值高估 |
| [sunk-cost-fallacy](../thinking/sunk-cost-fallacy/SKILL.md) | 并行 | 沉没成本谬误因已投入而继续，IKEA效应因已投入而高估 |
| [overconfidence-effect](../thinking/overconfidence-effect/SKILL.md) | 并行 | 过度自信高估自制质量，IKEA效应高估自制价值 |

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

1. Norton, M. I., Mochon, D., & Ariely, D. (2012). The IKEA effect: When labor leads to love. *Journal of Consumer Psychology*, 22(3), 453-460.
2. Aronson, E., & Mills, J. (1959). The effect of severity of initiation on liking for a group. *Journal of Abnormal and Social Psychology*, 59(2), 177-181.
3. Franke, N., Schreier, M., & Kaiser, U. (2010). The "I designed it myself" effect in mass customization. *Management Science*, 56(1), 125-140.
4. Mochon, D., Norton, M. I., & Ariely, D. (2012). Bolstering and restoring feelings of competence via the IKEA effect. *International Journal of Research in Marketing*, 29(4), 329-337.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
