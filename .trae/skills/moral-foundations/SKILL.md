---
name: moral-foundations
description: |
  触发：当需要评估决策是否受道德直觉影响、需要识别不同道德基础的冲突、需要分析道德判断差异时调用；常见信号包括"这不公平"、"这伤害了别人"、"这违背了传统"、"这不纯洁"。
  不触发：当只需描述道德观点、无需分析决策影响时；当道德判断确实一致、无冲突时（经多视角验证）；当只需记录价值观、无需理性分析时。
  Invoke when needing to evaluate whether decisions are affected by moral intuitions, identify conflicts between different moral foundations, or analyze moral judgment differences.
  Do NOT invoke when only describing moral viewpoints without analyzing decision impact, when moral judgments are truly consistent without conflicts (verified by multi-perspective analysis), or when only recording values without rational analysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["affect-heuristic", "framing-effect", "omission-bias", "empathy-gap"]
---

# 道德基础思维（Moral Foundations Thinking）

## 核心定义

人们基于5个道德基础（关爱/伤害、公平/欺骗、忠诚/背叛、权威/颠覆、圣洁/堕落）做道德判断。Haidt在2004年提出：道德判断是直觉驱动的，理性是事后辩护。不同文化权重不同。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充道德冲突场景、文化背景和利益相关方
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别道德基础冲突且解决方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别道德信号

- 是否出现"这不公平"、"这伤害了别人"、"这违背了传统"、"这不纯洁"等表述？
- 是否基于道德直觉做判断？
- 是否出现道德基础冲突？（如公平vs忠诚）
- 是否用理性为道德直觉辩护？

---

### Step 2: 分析道德基础

- 关爱/伤害：是否有人受到伤害？
- 公平/欺骗：是否公平公正？
- 忠诚/背叛：是否背叛群体？
- 权威/颠覆：是否挑战权威？
- 圣洁/堕落：是否违背纯洁/神圣？

---

### Step 3: 评估权重差异

- 不同利益相关方的道德基础权重？
- 文化背景如何影响道德基础优先级？
- 哪些道德基础冲突？
- 冲突强度如何？（1-10评分）

---

### Step 4: 设计道德协调

- 识别共同道德基础（各方都重视的）
- 设计多赢方案（满足多个道德基础）
- 使用道德框架重新表述问题
- 设计道德妥协方案

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **道德直觉先于理性**：人们先有道德直觉，再用理性辩护。原因：道德判断由情感系统快速生成，理性系统事后找理由支持直觉。
2. **5基础权重不同**：不同文化/政治倾向权重不同。原因： liberals重视关爱和公平，conservatives重视所有5个基础，权重差异导致道德分歧。
3. **冲突不可避免**：道德基础间常冲突（如公平vs忠诚）。原因：现实问题涉及多方利益，不同道德基础指向不同解决方案。
4. **多赢设计是解药**：寻找满足多个道德基础的方案。原因：多赢方案减少道德冲突，提高各方接受度。

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
- [ ] 是否识别了道德信号？
- [ ] 是否分析了5个道德基础？
- [ ] 是否评估了权重差异和冲突？
- [ ] 是否设计了道德协调方案？
- [ ] 是否识别了共同道德基础？
- [ ] 输出具体可执行，不含模糊建议（如"尊重道德"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [affect-heuristic](../thinking/affect-heuristic/SKILL.md) | 前置 | 情感启发式解释道德直觉的情感驱动 |
| [framing-effect](../thinking/framing-effect/SKILL.md) | 并行 | 框架效应影响道德判断表述 |
| [omission-bias](../thinking/omission-bias/SKILL.md) | 并行 | 不作为偏差影响道德权重评估 |
| [empathy-gap](../thinking/empathy-gap/SKILL.md) | 并行 | 共情差距使预测道德反应困难 |

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

1. Haidt, J., & Joseph, C. (2004). Intuitive ethics: How innately prepared intuitions generate culturally variable virtues. *Daedalus*, 133(1), 55-66.
2. Haidt, J. (2001). The emotional dog and its rational tail: A social intuitionist approach to moral judgment. *Psychological Review*, 108(4), 814-834.
3. Graham, J., Haidt, J., & Nosek, B. A. (2009). Liberals and conservatives rely on different sets of moral foundations. *Journal of Personality and Social Psychology*, 96(5), 1029-1046.
4. Haidt, J., & Graham, J. (2007). When morality opposes justice: Conservatives have moral intuitions that liberals may not recognize. *Social Justice Research*, 20(1), 98-116.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
