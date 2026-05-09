---
name: self-serving-bias
description: |
  触发：当需要评估归因是否受自我服务偏差影响、需要识别成功归己失败归外的模式、需要客观评估个人贡献时调用；常见信号包括"我成功了是因为能力"、"失败是因为外部因素"、"这不是我的错"。
  不触发：当只需记录事实、无需归因分析时；当有客观数据证明归因准确时；当分析他人行为时（基本归因错误更相关）。
  Invoke when needing to evaluate whether attributions are affected by self-serving bias, identify success-to-self failure-to-external patterns, or objectively assess personal contribution.
  Do NOT invoke when only recording facts without attribution analysis, when objective data proves attribution accuracy, or when analyzing others' behavior (fundamental attribution error is more relevant).
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["fundamental-attribution-error", "overconfidence-effect", "hindsight-bias", "confirmation-bias"]
---

# 自我服务偏差思维（Self-Serving Bias Thinking）

## 核心定义

人们倾向于将成功归因于内部因素（能力、努力），将失败归因于外部因素（运气、环境）。Miller和Ross在1975年提出：自我服务偏差保护自尊，维持积极自我形象。Zuckerman在1979年元分析证明：成功时内部归因强度是失败时的2倍。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充客观绩效数据、同行评价和外部视角
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别自我服务偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别自我服务信号

- 是否出现"我成功了是因为能力"、"失败是因为外部因素"、"这不是我的错"等表述？
- 成功时是否归因于内部因素（能力、努力）？
- 失败时是否归因于外部因素（运气、环境、他人）？
- 对同样结果，对自己和他人有不同归因吗？

---

### Step 2: 评估归因模式

- 列出最近3次成功和3次失败
- 每次归因：内部因素占比 vs 外部因素占比
- 比较成功和失败的归因模式差异
- 是否系统性偏向自我服务归因？

---

### Step 3: 分析心理机制

- 自尊保护：内部归因成功提升自尊，外部归因失败保护自尊
- 认知便利：自己的意图和努力比外部因素更可见
- 动机驱动：希望自己是能干的，影响归因方向
- 社会比较：向下比较增强自我服务归因

---

### Step 4: 校正归因

- 使用外部视角：未参与者如何归因？
- 寻找反证：成功中有多少运气成分？失败中有多少个人责任？
- 平衡归因：成功和失败都考虑内部和外部因素
- 记录归因模式，持续追踪偏差

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **成功≠全因自己**：成功包含能力、努力和运气，运气成分常被忽视。原因：大脑偏好内部归因，因为提升自尊，但忽视运气导致过度自信。
2. **失败≠全因外部**：失败包含个人责任和外部因素，个人责任常被回避。原因：承认个人失败伤害自尊，大脑自动寻找外部替罪羊。
3. **外部视角更客观**：未参与者没有自尊需求，归因更平衡。原因：旁观者看到完整图景，包括内部和外部因素。
4. **记录揭示模式**：持续记录归因模式，识别系统性偏差。原因：单次归因可能合理，模式揭示偏差方向。

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
- [ ] 是否识别了自我服务信号？
- [ ] 是否评估了归因模式（成功vs失败）？
- [ ] 是否分析了心理驱动机制？
- [ ] 是否使用外部视角校正？
- [ ] 是否平衡考虑内部和外部因素？
- [ ] 输出具体可执行，不含模糊建议（如"客观看待"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [fundamental-attribution-error](../thinking/fundamental-attribution-error/SKILL.md) | 并行 | 基本归因错误是对他人的偏差，自我服务偏差是对自己的偏差 |
| [overconfidence-effect](../thinking/overconfidence-effect/SKILL.md) | 并行 | 过度自信是自我服务偏差的后果 |
| [hindsight-bias](../thinking/hindsight-bias/SKILL.md) | 并行 | 后见之明强化自我服务归因 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误寻找支持自我归因的证据 |

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

1. Miller, D. T., & Ross, M. (1975). Self-serving biases in the attribution of causality: Fact or fiction? *Psychological Bulletin*, 82(2), 213-225.
2. Zuckerman, M. (1979). Attribution of success and failure revisited, or: The motivational bias is alive and well in attribution theory. *Journal of Personality*, 47(2), 245-287.
3. Mezulis, A. H., Abramson, L. Y., Hyde, J. S., & Hankin, B. L. (2004). Is there a universal positivity bias in attributions? A meta-analytic review of individual, developmental, and cultural differences in the self-serving attributional bias. *American Psychologist*, 59(8), 711-721.
4. Campbell, W. K., & Sedikides, C. (1999). Self-threat magnifies the self-serving bias: A meta-analytic integration. *Review of General Psychology*, 3(1), 23-43.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
