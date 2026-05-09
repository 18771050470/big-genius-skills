---
name: deductive-thinking
description: |
  触发：当需要从已知规则、公理或普遍性原则推导出具体结论时调用；常见信号包括验证假设应用既存理论、进行逻辑三段论推理、需要必然性的结论。
  不触发：当需要探索未知可能性、创新或生成新假设时（应使用归纳或溯因思维）；当前提尚不确定或存在争议时（应先验证前提）；当需要概率性判断而非确定性结论时。
  Invoke when deductive reasoning is required: to derive specific conclusions from general premises, when testing a hypothesis against established laws, or when logical certainty is needed.
  Do NOT invoke when: exploring unknown possibilities or generating new hypotheses (use inductive or abductive thinking); when premises are uncertain or controversial (validate premises first); when probabilistic judgment is needed rather than certainty.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["inductive-thinking", "abductive-thinking", "first-principles-thinking"]
---

# 演绎思维（Deductive Thinking）

## 核心定义

从普遍性规则出发，结合具体条件，推导出必然性结论的逻辑推理方式。结论由前提保证，只要前提正确且推理有效，结论 100% 可靠。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 确立大前提

- 明确陈述一个或多个被视为真实且适用于当前问题的普遍性规则
- 确保大前提在该领域内被公认或可证明
- 标注前提来源和可信度

---

### Step 2: 确立小前提

- 陈述与当前问题相关的具体事实或条件
- 确保该事实能与大前提关联（属于大前提的范畴）
- 验证事实的准确性

---

### Step 3: 应用逻辑规则进行推导

- 根据逻辑形式（三段论、假言推理、选言推理）将大前提与小前提结合
- 检查是否符合有效推理形式（modus ponens, modus tollens 等）
- 警惕常见谬误（肯定后件、否定前件等）

---

### Step 4: 重复推导（如果需要）

- 将前面步骤的结论作为新的小前提
- 与其余大前提结合，继续推导，形成推理链
- 检查推理链长度，过长则风险增加

---

### Step 5: 验证结论的有效性与可靠性

- 检查推理形式是否有效（逻辑正确）
- 检查前提是否全部真实且无歧义
- 检查是否存在隐含前提

---

### Step 6: 记录并输出最终结论

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **前提真实性原则**：演绎结论的可靠性完全依赖于前提的真实性。必须先确保大前提和小前提都是真实的，否则结论可能错误。原因：演绎思维不产生新知识，只是从前提中提取隐含信息，前提假则结论无法保证真。
2. **逻辑有效性原则**：推理形式必须有效，即结论必须逻辑上必然从前提导出。无效推理即使前提真，结论也可能假。原因：有效性是演绎推理的命脉，确保每一步推导都严格遵循公认的推理规则。
3. **清晰边界原则**：演绎推理只适用于封闭、定义明确的系统（如数学、经典逻辑、理论模型），不适用于完全开放或不确定的领域。原因：演绎需要完备的前提，当前提不完备或存在例外时，推理结果不成立。
4. **可追溯性原则**：每一步推理都必须可回溯，有明确依据。复杂推理链应分解为若干简单三段论，以便审查。原因：确保推理过程的透明性，便于发现错误和修正。
5. **一致性原则**：整个推理链不能产生逻辑矛盾。若从同一组前提推出矛盾结论，则前提集不一致，需要重新审视。原因：矛盾意味着前提或推理中有错误。

---

## 自检清单

> 聚焦演绎思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**演绎思维特有关键检查项**：

- [ ] **大前提是否在该领域内被公认或可证明？** 是否存在隐含的前提假设未被发现？
- [ ] **小前提是否真实且能与大前提关联？** 事实准确性是否经过验证？
- [ ] **推理形式是否有效？** 是否存在肯定后件、否定前件等常见谬误？
- [ ] **推理链是否过长？** 过长的链条是否增加了累积错误的风险？
- [ ] **是否检查了隐含前提？** 未明说的假设是否可能推翻整个结论？
- [ ] **结论的确定性是否被正确表述？** 是否将"前提正确则结论必然正确"误解为"结论绝对正确"？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [inductive-thinking](../thinking/inductive-thinking/SKILL.md) | 互补 | 当需要从观察中建立普遍性前提时 |
| [abductive-thinking](../thinking/abductive-thinking/SKILL.md) | 互补 | 当需要解释观察现象并生成假设时 |
| [first-principles-thinking](../thinking/first-principles-thinking/SKILL.md) | 前置 | 当需要分解问题到基础真理以确立牢靠的大前提时 |

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

1. Aristotle. (c. 350 BCE). *Prior Analytics*.
2. Copi, I. M., Cohen, C., & McMahon, K. (2014). *Introduction to Logic* (14th ed.). Pearson.
3. Tarski, A. (1941). *Introduction to Logic and to the Methodology of Deductive Sciences*. Oxford University Press.
4. Johnson-Laird, P. N. (1983). *Mental Models: Towards a Cognitive Science of Language, Inference, and Consciousness*. Harvard University Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
