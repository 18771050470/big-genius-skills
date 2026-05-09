---
name: dunning-kruger-effect
description: |
  触发：当需要评估能力判断是否受认知偏差影响、需要识别"无知者无畏"现象、需要设计能力评估机制时调用；常见信号包括"这很简单"、"我什么都懂"、"专家都是骗子"。
  不触发：当有客观能力测试数据时；当只需评估具体技能水平、无需考虑元认知偏差时；当决策者已证明自己具备准确自我评估能力时。
  Invoke when needing to evaluate whether ability judgments are affected by cognitive bias, identify "unconscious incompetence" phenomenon, or design ability assessment mechanisms.
  Do NOT invoke when objective ability test data is available, when only assessing specific skill levels without considering metacognitive bias, or when the decision maker has demonstrated accurate self-assessment ability.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["overconfidence-effect", "metacognition", "feedback-loop", "bayesian-updating"]
---

# 达克效应思维（Dunning-Kruger Effect Thinking）

## 核心定义

能力不足的人倾向于高估自己的能力，而能力强的人倾向于低估自己。Kruger和Dunning在1999年提出：能力不足者缺乏"元认知"能力，无法认识到自己的不足。随着能力提升，人们会经历"绝望之谷"（意识到自己无知），最终达到"开悟之坡"（准确评估自己）。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充客观能力测试结果、同行评价和具体表现数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确达克效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别能力评估信号

- 自我评估与客观表现的差距
- 是否出现"这很简单"、"我什么都懂"等表述？
- 是否缺乏对该领域的深入理解却自信满满？
- 是否忽视专家意见或同行反馈？

---

### Step 2: 评估元认知能力

- 能否准确识别自己的知识盲区？
- 能否区分"知道"和"知道如何知道"？
- 是否理解该领域的复杂性和深度？
- 能否解释该领域的核心概念和争议？

---

### Step 3: 定位能力阶段

- 愚昧山峰：能力低但自信高（无知者无畏）
- 绝望之谷：意识到自己无知，自信骤降
- 开悟之坡：能力逐渐提升，自信恢复
- 持续平稳：能力高且自信准确
- 标注当前所处阶段

---

### Step 4: 设计校正机制

- 客观测试：用标准化测试替代自我评估
- 同行评审：邀请领域专家评估能力
- 反馈循环：建立持续反馈机制
- 谦逊训练：刻意练习识别自己的知识盲区

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **无知者最自信**：能力不足者缺乏元认知能力，无法认识到自己的不足。原因：元认知需要领域知识，能力不足者恰好缺乏这种知识。
2. **能力曲线非线性**：学习过程中自信先升后降再升，形成"绝望之谷"。原因：随着知识增加，人们意识到领域复杂性，自信下降。
3. **专家低估自己**：能力强的人倾向于低估自己，因为他们知道多少是自己不知道的。原因：专家知道领域边界，意识到未知领域更大。
4. **反馈是解药**：持续、具体、可操作的反馈帮助校准自我认知。原因：外部反馈提供客观参照，对抗主观偏差。

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
- [ ] 自我评估与客观表现的差距是否被量化？
- [ ] 元认知能力是否被评估？
- [ ] 是否定位了当前能力阶段？
- [ ] 是否设计了客观测试和同行评审机制？
- [ ] 是否建立了持续反馈循环？
- [ ] 输出具体可执行，不含模糊建议（如"保持谦逊"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [overconfidence-effect](../thinking/overconfidence-effect/SKILL.md) | 并行 | 过度自信是达克效应的表现之一 |
| [metacognition](../thinking/metacognition/SKILL.md) | 前置 | 元认知是识别达克效应的核心能力 |
| [feedback-loop](../thinking/feedback-loop/SKILL.md) | 并行 | 反馈循环是校正达克效应的关键机制 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 贝叶斯更新根据新证据调整自我评估 |

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

1. Kruger, J., & Dunning, D. (1999). Unskilled and unaware of it: How difficulties in recognizing one's own incompetence lead to inflated self-assessments. *Journal of Personality and Social Psychology*, 77(6), 1121-1134.
2. Dunning, D., Heath, C., & Suls, J. M. (2004). Flawed self-assessment: Implications for health, education, and the workplace. *Psychological Science in the Public Interest*, 5(3), 69-106.
3. Ehrlinger, J., et al. (2008). Why the unskilled are unaware: Further explorations of (absent) self-insight among the incompetent. *Organizational Behavior and Human Decision Processes*, 105(1), 98-121.
4. Burson, K. A., Larrick, R. P., & Klayman, J. (2006). Skilled or unskilled, but still unaware of it: How perceptions of difficulty drive miscalibration in relative comparisons. *Journal of Personality and Social Psychology*, 90(1), 60-77.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
