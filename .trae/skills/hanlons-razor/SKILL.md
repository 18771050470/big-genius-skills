---
name: hanlons-razor
description: |
  触发：当需要评估他人行为的动机、需要识别恶意归因偏差、需要区分愚蠢/疏忽与恶意时调用；常见信号包括"他们故意搞我"、"这肯定是针对我们的"、"背后一定有阴谋"。
  不触发：当已有证据证明恶意意图时；当涉及安全/法律风险评估需假设最坏情况时；当只需记录行为、无需推断动机时。
  Invoke when needing to evaluate others' motives, identify malice attribution bias, or distinguish stupidity/neglect from malice.
  Do NOT invoke when there is already evidence of malicious intent, when security/legal risk assessment requires assuming worst-case scenarios, or when only recording behavior without inferring motives.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["fundamental-attribution-error", "confirmation-bias", "occams-razor", "cynicism"]
---

# 汉隆剃刀思维（Hanlon's Razor Thinking）

## 核心定义

能用愚蠢、疏忽或无知解释的，就不要归咎于恶意。Robert J. Hanlon 在 1980 年提出：在解释他人行为时，应优先考虑能力不足和认知局限，而非恶意动机。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充行为背景、当事人能力和历史行为模式
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别恶意归因偏差且替代解释清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别恶意归因信号

- 是否出现"他们故意搞我"、"这肯定是针对我们的"、"背后一定有阴谋"等表述？
- 是否将负面结果立即归因于他人恶意？
- 是否忽视了更简单解释的可能性？
- 是否因归因于恶意而产生过度情绪反应？

---

### Step 2: 收集行为证据

- 行为的具体表现是什么？（客观事实 vs 主观解读）
- 行为人的能力水平和知识背景？
- 行为发生的情境约束？（时间压力、资源限制、信息不足）
- 历史行为模式：此人是否一贯表现出恶意？

---

### Step 3: 构建替代解释

- 无知解释：是否因缺乏知识或信息导致？
- 疏忽解释：是否因注意力分散或流程漏洞导致？
- 能力解释：是否因技能不足或经验缺乏导致？
- 系统解释：是否因制度缺陷或激励错位导致？
- 恶意解释：是否有明确证据支持故意伤害？

---

### Step 4: 应用概率判断

- 各解释的先验概率？（基于基率：愚蠢和疏忽比恶意更常见）
- 各解释与证据的吻合度？
- 奥卡姆剃刀检验：最简单的解释是否足够？
- 是否存在确认偏误？（只寻找支持恶意的证据）

---

### Step 5: 设计应对策略

- 若解释为无知/疏忽：提供信息、培训、流程改进
- 若解释为系统问题：修复制度、调整激励、优化流程
- 若解释为恶意：收集证据、设定边界、升级处理
- 保持开放：随新证据调整归因，避免过早定论

---

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **愚蠢比恶意更常见**：在人群中，能力不足和认知局限的发生率远高于恶意动机。原因：恶意需要意图、计划和执行，而疏忽只需要注意力的瞬间缺失。
2. **归因需证据**：将行为归因于恶意需要积极证据，而非仅仅因为结果是负面的。原因：负面结果可以由多种非恶意因素导致，恶意只是其中一种且概率较低。
3. **情绪是信号**：强烈的被伤害感可能是归因偏差的信号，而非恶意存在的证明。原因：基本归因错误使倾向于将他人行为归因于内在特质（如恶意），而忽视情境因素。
4. **系统常是根源**：许多看似恶意的行为实际上是系统缺陷的产物。原因：制度设计、激励结构和流程漏洞可以系统性地产生负面结果，无需任何个人恶意。

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

**汉隆剃刀特有关键检查项**：

- [ ] **汉隆剃刀特供**：是否识别了恶意归因信号？是否出现"故意"、"针对"、"阴谋"等表述？
- [ ] **汉隆剃刀特供**：是否收集了行为人的能力水平和情境约束信息？
- [ ] **汉隆剃刀特供**：是否构建了非恶意的替代解释？（无知、疏忽、能力、系统）
- [ ] **汉隆剃刀特供**：是否应用了基率思维？（愚蠢/疏忽的先验概率是否高于恶意？）
- [ ] **汉隆剃刀特供**：是否存在确认偏误？是否只寻找支持恶意的证据而忽视反证？
- [ ] **汉隆剃刀特供**：应对策略是否与归因匹配？非恶意归因不应导致对抗性应对
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"先别急着生气"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [fundamental-attribution-error](../thinking/fundamental-attribution-error/SKILL.md) | 前置 | 基本归因错误解释为何倾向于将行为归因于内在特质（如恶意） |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误使只寻找支持恶意归因的证据 |
| [occams-razor](../thinking/occams-razor/SKILL.md) | 并行 | 奥卡姆剃刀偏好最简单的解释，汉隆剃刀偏好非恶意的解释 |
| [cynicism](../thinking/cynicism/SKILL.md) | 对立 | 犬儒主义假设他人动机不良，汉隆剃刀假设无知/疏忽更可能 |

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

1. Hanlon, R. J. (1980). In Bloch, A. (Ed.), *Murphy's Law, Book Two: More Reasons Why Things Go Wrong*. Price Stern Sloan.
2. Heinlein, R. A. (1941). *Logic of Empire*. Astounding Science Fiction. (注：类似思想更早出现)
3. Goethe, J. W. von. (1774). *The Sorrows of Young Werther*. (注："误解和疏忽比欺骗更常见"的早期表述)
4. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (关于归因偏差和基率忽视的论述)

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
