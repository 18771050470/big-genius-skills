---
name: conjunction-fallacy
description: |
  触发：当需要评估判断是否违反概率合取规则、需要识别"详细描述更可能"偏差、需要纠正复合事件概率估计时调用；常见信号包括" Linda是银行出纳且女权主义者"、"这个方案既安全又高效"、"同时发生X和Y"。
  不触发：当只需描述复合事件、无需概率判断时；当使用概率模型计算合取概率时；当事件间存在强因果关系使合取概率接近单一事件时。
  Invoke when needing to evaluate whether judgments violate probability conjunction rules, identify "detailed description more likely" bias, or correct compound event probability estimates.
  Do NOT invoke when only describing compound events without probability judgment, when using probability models to calculate conjunction probability, or when strong causal relationships between events make conjunction probability close to single event.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["representativeness-heuristic", "base-rate-fallacy", "narrative-thinking", "probabilistic-thinking"]
---

# 合取谬误思维（Conjunction Fallacy Thinking）

## 核心定义

人们认为两个事件同时发生的概率高于其中单一事件发生的概率。Tversky和Kahneman在1983年Linda实验中证明：85%参与者认为"Linda是银行出纳且女权主义者"比"Linda是银行出纳"更可能，违反概率论P(A∧B)≤P(A)规则。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充各单一事件的独立概率数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别合取谬误影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别合取信号

- 是否出现"既...又..."、"同时发生X和Y"、"A且B"等表述？
- 是否认为复合事件比单一事件更可能？
- 是否因描述详细而认为更可信？
- 是否违反P(A∧B)≤P(A)概率规则？

---

### Step 2: 评估合取概率

- P(A) = 事件A的独立概率
- P(B) = 事件B的独立概率
- P(A∧B) = P(A) × P(B)（独立事件）或 P(A) × P(B|A)（相关事件）
- 合取概率永远≤任一单一事件概率

---

### Step 3: 分析心理机制

- 代表性启发式：复合描述更"典型"，感觉更可能
- 叙事连贯性：故事越完整，感觉越真实
- 确认偏误：细节支持已有信念
- 情感共鸣：生动描述触发情感，情感替代概率判断

---

### Step 4: 校正概率判断

- 分解复合事件为单一事件
- 计算各单一事件独立概率
- 使用概率乘法规则计算合取概率
- 比较直觉判断与计算结果

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **合取概率≤单一概率**：两个事件同时发生的概率永远不超过其中任一事件单独发生的概率。原因：数学规则P(A∧B)≤P(A)是概率论基本定理，不可违反。
2. **详细不等于可能**：描述越详细的事件不一定更可能。原因：每个额外细节都是额外约束，降低整体概率。
3. **故事连贯性≠概率**：好故事不等于高概率。原因：叙事连贯性激活情感系统，不激活概率计算系统。
4. **分解是解药**：将复合事件分解为单一事件，分别评估概率。原因：分解迫使使用分析思维，绕过直觉偏差。

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
- [ ] **合取谬误特供**：是否识别了合取信号？是否出现"既...又..."、"同时发生X和Y"等表述？是否认为复合事件比单一事件更可能？
- [ ] **合取谬误特供**：是否计算了合取概率？是否应用了P(A∧B)≤P(A)规则？是否区分了独立事件（P(A)×P(B)）和相关事件（P(A)×P(B|A)）？
- [ ] **合取谬误特供**：是否分析了心理驱动机制？代表性启发式、叙事连贯性、确认偏误、情感共鸣是否被识别？
- [ ] **合取谬误特供**：是否分解复合事件为单一事件？是否分别评估了各单一事件的独立概率？是否使用了概率乘法规则？
- [ ] **合取谬误特供**：是否比较了直觉判断与计算结果？直觉是否违反了概率论基本规则？是否量化了直觉偏差程度？
- [ ] 输出具体可执行，不含模糊建议（如"考虑概率"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [representativeness-heuristic](../thinking/representativeness-heuristic/SKILL.md) | 前置 | 代表性启发式是合取谬误的心理根源 |
| [base-rate-fallacy](../thinking/base-rate-fallacy/SKILL.md) | 并行 | 基础概率谬误与合取谬误都违反概率规则 |
| [narrative-thinking](../thinking/narrative-thinking/SKILL.md) | 并行 | 叙事偏差使连贯故事感觉更可能 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供合取规则数学框架 |

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

1. Tversky, A., & Kahneman, D. (1983). Extensional versus intuitive reasoning: The conjunction fallacy in probability judgment. *Psychological Review*, 90(4), 293-315.
2. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 15: Linda's Problem)
3. Tentori, K., Bonini, N., & Osherson, D. (2004). The conjunction fallacy: A misunderstanding about conjunction? *Cognitive Science*, 28(3), 467-477.
4. Fisk, J. E., & Pidgeon, N. (1996). Conditional probabilities, probability conjunctions, and the conjunction fallacy: A review and reconciliation of conflicting findings. *Organizational Behavior and Human Decision Processes*, 68(1), 1-16.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
