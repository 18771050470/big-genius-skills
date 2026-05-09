---
name: overconfidence-effect
description: |
  触发：当需要评估判断是否过度自信、需要校准概率估计、需要识别"过度确定"偏差时调用；常见信号包括"我确定"、"绝对没问题"、"100%会成功"、"不可能出错"。
  不触发：当有客观验证数据证明判断准确时；当只需记录主观信心水平、无需校准时；当决策者已证明自己具备准确校准能力时。
  Invoke when needing to evaluate whether judgments are overconfident, calibrate probability estimates, or identify "overprecision" bias.
  Do NOT invoke when objective validation data proves judgment accuracy, when only recording subjective confidence levels without calibration, or when the decision maker has demonstrated accurate calibration ability.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["dunning-kruger-effect", "hindsight-bias", "bayesian-updating", "probabilistic-thinking"]
---

# 过度自信效应思维（Overconfidence Effect Thinking）

## 核心定义

人们倾向于高估自己的知识、能力和判断准确性。Moore和Healy在2008年提出三种过度自信：过度精确（overprecision，置信区间过窄）、过度定位（overplacement，认为自己优于他人）、过度估计（overestimation，高估绝对表现）。过度自信被称为"最普遍且最强大的认知偏差"。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充历史判断准确率、客观表现数据和同行评价
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别过度自信影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别过度自信信号

- 是否出现"我确定"、"绝对"、"100%"等表述？
- 置信区间是否过窄？（90%置信区间实际覆盖率远低于90%）
- 是否认为自己优于平均水平？（统计上不可能所有人都高于平均）
- 是否忽视反面证据或不确定性？

---

### Step 2: 评估过度自信类型

- 过度精确：置信区间过窄，对自己的知识过于确定
- 过度定位：认为自己优于大多数人（优于平均效应）
- 过度估计：高估自己的绝对表现或能力
- 标注属于哪种类型，或多种类型组合

---

### Step 3: 校准判断

- 历史判断准确率是多少？（如果有记录）
- 扩大置信区间：将直觉置信区间扩大2-3倍
- 考虑基准率：同类判断的平均准确率是多少？
- 使用外部视角：未参与者的判断是什么？

---

### Step 4: 设计防偏差机制

- 记录预测和置信度，持续追踪校准曲线
- 强制考虑反面：列出3个为什么可能错的理由
- 使用概率语言替代确定性语言（"70%可能"替代"确定"）
- 邀请独立评审者挑战判断

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **过度自信是最强偏差**：被称为"最普遍且最强大的认知偏差"，影响从日常判断到专业决策。原因：自信带来心理舒适感，大脑偏好确定性而非不确定性。
2. **专家也过度自信**：专业知识和经验不能消除过度自信，有时反而加剧。原因：专家对自己的判断更有信心，但不一定更准确，信心-准确度脱节。
3. **校准曲线揭示真相**：当人们说"90%确定"时，实际准确率通常只有50-70%。原因：人类不擅长校准主观置信度和客观概率。
4. **记录是解药**：记录预测和结果，持续追踪校准曲线，逐步改善。原因：反馈循环帮助大脑学习真实概率，减少系统性偏差。

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
- [ ] 是否识别了过度自信信号？
- [ ] 是否评估了过度自信类型（精确/定位/估计）？
- [ ] 是否进行了判断校准？
- [ ] 是否设计了防偏差机制（记录、反面考虑、概率语言）？
- [ ] 输出具体可执行，不含模糊建议（如"保持谦虚"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [dunning-kruger-effect](../thinking/dunning-kruger-effect/SKILL.md) | 并行 | 达克效应解释能力不足者为何过度自信 |
| [hindsight-bias](../thinking/hindsight-bias/SKILL.md) | 并行 | 后见之明导致事后过度自信 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 贝叶斯更新根据新证据校准置信度 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供校准方法 |

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

1. Moore, D. A., & Healy, P. J. (2008). The trouble with overconfidence. *Psychological Review*, 115(2), 502-517.
2. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 21: Intuitions vs Formulas)
3. Russo, J. E., & Schoemaker, P. J. H. (1992). Managing overconfidence. *Sloan Management Review*, 33(2), 7-17.
4. De Bondt, W. F., & Thaler, R. H. (1995). Financial decision-making in markets and firms: A behavioral perspective. *Handbooks in OR & MS*, 9, 385-410.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
