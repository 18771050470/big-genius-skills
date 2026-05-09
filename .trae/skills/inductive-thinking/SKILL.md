---
name: inductive-thinking
description: |
  触发：当需要从具体案例、数据或观察中总结出一般性规律、原则或预测未来趋势时调用；常见信号包括总结历史经验、发现数据模式、建立经验法则、预测未来走向。
  不触发：当已有普遍适用的理论或规则可以直接应用时（应使用演绎思维）；当需要解释特定异常现象的原因时（应使用溯因思维）；当样本量过小或数据质量差，无法支撑可靠归纳时。
  Invoke when: needing to derive general patterns or principles from specific cases, data, or observations; common signals include summarizing historical experience, discovering data patterns, establishing empirical rules.
  Do NOT invoke when: general theories or rules are already available for direct application (use deductive thinking); when explaining the cause of a specific anomaly (use abductive thinking); when sample size is too small or data quality is poor.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["deductive-thinking", "abductive-thinking", "statistical-thinking", "pattern-recognition"]
---

# 归纳思维（Inductive Thinking）

## 核心定义

从具体案例、数据或观察中总结出一般性规律、原则或预测未来趋势的推理方式。结论具有或然性，非必然性，但可通过增加样本量和多样性提高可靠性。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 收集案例

- 罗列所有相关案例，确保案例多样性和无偏性
- 标注每个案例的来源、时间、背景
- 检查是否存在选择偏误（只收集支持自己观点的案例）

---

### Step 2: 识别共同特征

- 对比各案例，找出所有共享的显著特征
- 排除偶然因素和噪音
- 区分相关性与因果性

---

### Step 3: 形成初步规律

- 基于共同特征，提出一般性陈述或规律
- 明确规律的适用边界和条件
- 标注规律的可信度（基于样本量和一致性）

---

### Step 4: 检验规律的可靠性

- 寻找反例：是否有案例不符合该规律？
- 评估样本代表性：样本是否覆盖足够多样的场景？
- 检查替代解释：是否有其他规律也能解释这些案例？

---

### Step 5: 应用与预测

- 将归纳出的规律应用于新场景
- 做出预测，并明确预测的不确定性
- 设计验证方案，检验预测准确性

---

### Step 6: 输出结论与信度

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **样本多样性原则**：归纳的可靠性取决于样本的多样性和代表性。必须确保案例覆盖不同场景、时间、条件，避免单一来源。原因：同质样本会导致以偏概全，规律在更广泛场景中失效。
2. **反例检验原则**：主动寻找反例是检验归纳规律可靠性的最有效方法。如果一个规律没有反例，其可信度更高；若存在反例，则需要修正或限定适用范围。原因：确认偏误使人类倾向于忽视反例，主动寻找才能避免盲目自信。
3. **边界明确原则**：归纳规律必须明确其适用边界和条件，不能无限推广。原因：所有归纳结论都有适用范围，超出边界应用会导致错误决策。
4. **因果谨慎原则**：观察到的相关性不等于因果性。在宣称因果关系前，必须排除第三方变量、巧合、反向因果等替代解释。原因：错误归因是归纳思维最常见的陷阱，会导致无效的干预措施。
5. **迭代更新原则**：归纳规律应随新证据不断修正。当新案例与现有规律矛盾时，优先修正规律而非忽视案例。原因：归纳结论本质上是暂时的，固执于旧规律会导致系统性错误。

---

## 自检清单

> 聚焦归纳思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**归纳思维特有关键检查项**：

- [ ] **样本是否具有多样性和代表性？** 是否存在选择偏误（只收集支持自己观点的案例）？
- [ ] **是否主动寻找了反例？** 反例的存在是否被认真考虑而非被忽视？
- [ ] **相关性与因果性是否被区分？** 观察到的共同特征是否被错误地当作因果？
- [ ] **规律的适用边界是否明确？** 归纳结论是否被无限推广到了不适用的场景？
- [ ] **替代解释是否被排除？** 是否有其他规律也能解释这些案例？
- [ ] **样本量是否足够支撑结论的可靠性？** 基于少量案例的归纳是否被过度自信？
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
| [deductive-thinking](../thinking/deductive-thinking/SKILL.md) | 互补 | 当需要用归纳出的规律推导具体结论时 |
| [abductive-thinking](../thinking/abductive-thinking/SKILL.md) | 互补 | 当需要解释异常案例并修正规律时 |
| [statistical-thinking](../thinking/statistical-thinking/SKILL.md) | 前置 | 当需要量化样本代表性和结论信度时 |
| [pattern-recognition](../thinking/pattern-recognition/SKILL.md) | 并行 | 当需要从大量数据中自动发现模式时 |

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

1. Mill, J. S. (1843). *A System of Logic*. John W. Parker.
2. Carnap, R. (1950). *Logical Foundations of Probability*. University of Chicago Press.
3. Goodman, N. (1955). *Fact, Fiction, and Forecast*. Harvard University Press.
4. Popper, K. R. (1959). *The Logic of Scientific Discovery*. Hutchinson.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
