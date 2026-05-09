---
name: abstract-thinking
description: |
  触发：当需要从复杂现象中提取本质规律、设计可复用的抽象模型、或进行系统性设计时调用；常见信号包括"太复杂了，需要简化"、需要定义通用接口或模块、需要理解底层原理。
  不触发：当需要精确执行具体操作步骤时（如执行命令、配置参数）；当需要处理极低层次细节且不允许简化时（如调试硬件寄存器）；当对象本身就是抽象概念且没有进一步抽象必要时（如数学公理）。
  Invoke when: facing complex phenomena requiring essential pattern extraction, designing reusable abstractions, or establishing conceptual models for system design.
  Do NOT invoke when: precise execution of specific operations is needed; when handling low-level details that cannot be simplified; when the subject is already an abstract concept with no further abstraction needed.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["first-principles", "system-thinking", "modular-thinking", "dreyfus-model"]
---

# 抽象思维（Abstract Thinking）

## 核心定义

从具体事物中提取本质特征，忽略非关键细节，形成可复用概念模型的能力——它是所有建模活动的基础。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 收集具体实例

- 列出所有相关实例，保持原样，不做判断
- 标注每个实例的来源、背景和关键属性
- 检查实例的多样性和代表性

---

### Step 2: 识别共性特征

- 比较各实例，找出共同属性、行为、约束
- 标记差异点作为可变维度
- 排除偶然因素和噪音

---

### Step 3: 提取本质特征

- 从共性特征中区分本质与非本质
- 问自己：如果去掉这个特征，事物还是它吗？
- 用第一性原理验证本质特征的正确性

---

### Step 4: 构建抽象模型

- 用提取的本质特征构建概念模型
- 明确模型的边界和适用条件
- 标注模型的局限性和例外情况

---

### Step 5: 验证模型

- 用新实例检验模型的解释力和预测力
- 寻找反例，检查模型是否需要修正
- 评估模型的简洁性和通用性

---

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **本质优先**：区分本质特征与偶然特征，只保留决定事物根本性质的要素。原因：非本质细节会干扰模型的通用性和复用性。
2. **适度抽象**：抽象层次要恰到好处，既不过度简化丢失关键信息，也不过度复杂失去实用价值。原因：过度抽象会导致模型脱离实际，无法指导实践。
3. **可验证性**：抽象模型必须能被具体实例验证，不能是纯粹的理论构想。原因：无法验证的模型只是假设，不能作为决策依据。
4. **边界意识**：明确模型的适用范围和局限性，不无限推广。原因：所有抽象都有边界，超出边界应用会导致错误结论。
5. **迭代精炼**：抽象不是一次完成的，需要随着新实例不断修正和优化。原因：初始抽象往往不完整，持续迭代才能逼近真相。

---

## 自检清单

> 聚焦抽象思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**抽象思维特有关键检查项**：

- [ ] **是否从足够多样的实例中提取共性？** 实例的多样性是否足以支撑通用结论？
- [ ] **本质特征与非本质特征是否被区分？** "如果去掉这个特征，事物还是它吗？"是否被认真追问？
- [ ] **抽象层次是否适度？** 是否过度简化丢失了关键信息，或过度复杂失去了实用价值？
- [ ] **模型的适用边界是否明确？** 抽象结论是否被无限推广到了不适用的场景？
- [ ] **是否用新实例验证了模型的解释力和预测力？** 模型是否经过了反例检验？
- [ ] **是否记录了模型的局限性和例外情况？** 抽象不是万能钥匙，边界意识是否清晰？
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
| [first-principles](../thinking/first-principles/SKILL.md) | 前置 | 当需要拆解到最基本真理来验证抽象的正确性时 |
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 当抽象涉及多个相互作用的组件时 |
| [modular-thinking](../thinking/modular-thinking/SKILL.md) | 后置 | 当需要将抽象模型转化为可复用的模块时 |
| [dreyfus-model](../thinking/dreyfus-model/SKILL.md) | 参考 | 当需要评估团队对抽象概念的理解程度时 |

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

1. Piaget, J. (1952). *The Origins of Intelligence in Children*. International Universities Press.
2. Vygotsky, L. S. (1978). *Mind in Society: The Development of Higher Psychological Processes*. Harvard University Press.
3. Bruner, J. S. (1960). *The Process of Education*. Harvard University Press.
4. Simon, H. A. (1962). The Architecture of Complexity. *Proceedings of the American Philosophical Society*, 106(6), 467-482.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
