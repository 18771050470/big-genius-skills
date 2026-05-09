---
name: reductionism
description: |
  触发：当需要将复杂系统分解为可理解的组成部分、需要识别系统核心机制、需要简化问题以找到解决方案时调用；常见信号包括"拆解来看"、"核心问题是"、"本质上是"。
  不触发：当系统整体行为无法从部分推导时（涌现现象）；当部分之间的交互关系比部分本身更重要时；当只需理解系统整体功能、无需了解内部机制时。
  Invoke when needing to decompose complex systems into understandable components, identify core mechanisms, or simplify problems to find solutions.
  Do NOT invoke when system-level behavior cannot be derived from parts (emergence), when interactions between parts are more important than parts themselves, or when only understanding system-level function without internal mechanisms.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["systems-thinking", "divide-and-conquer", "first-principles", "holism"]
---

# 还原论思维（Reductionism Thinking）

## 核心定义

将复杂系统分解为其组成部分，通过理解部分来理解整体。Descartes在《方法论》中提出：将复杂问题分解为尽可能多的部分，以便更好地解决。还原论是科学方法的核心，但需注意"整体大于部分之和"的涌现现象。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统组成部分信息、部分间交互关系和整体行为特征
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已完成系统分解且核心机制清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别系统边界

- 系统的边界在哪里？什么属于系统、什么不属于？
- 系统的输入和输出是什么？
- 系统与外部环境的交互方式？
- 标注系统层级：子系统、系统、超系统

---

### Step 2: 分解系统组成部分

- 系统由哪些核心部分组成？
- 每个部分的功能是什么？
- 部分之间的层级关系？
- 识别关键部分和非关键部分

---

### Step 3: 分析部分间交互

- 部分之间如何交互？
- 交互是线性的还是非线性的？
- 是否存在反馈循环？
- 交互关系是否产生涌现行为（整体行为无法从部分推导）？

---

### Step 4: 识别核心机制

- 哪些部分和交互是系统行为的关键驱动因素？
- 移除哪些部分会导致系统失效？
- 简化模型：最少需要哪些部分才能解释系统行为？
- 区分必要条件和充分条件

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **分解是理解复杂性的第一步**：将大问题拆分为小问题，逐个解决。原因：人类认知能力有限，无法同时处理过多变量。
2. **部分之和不等于整体**：系统可能表现出部分不具备的涌现行为。原因：部分之间的非线性交互产生新属性，无法从部分单独推导。
3. **简化模型有价值但不完整**：简化模型帮助理解核心机制，但忽略细节可能导致错误预测。原因：模型是现实的抽象，不是现实本身。
4. **还原论有边界**：某些系统（如生态系统、社会系统）的整体行为无法从部分推导。原因：这些系统的核心是部分之间的关系，而非部分本身。

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
- [ ] 系统边界是否被清晰定义？
- [ ] 系统组成部分是否被完整识别？
- [ ] 部分间交互关系是否被分析？
- [ ] 是否识别了涌现行为（如果有）？
- [ ] 核心机制是否被准确识别？
- [ ] 输出具体可执行，不含模糊建议（如"拆解分析"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [systems-thinking](../thinking/systems-thinking/SKILL.md) | 互补 | 系统思维关注整体和关系，还原论关注部分和机制 |
| [divide-and-conquer](../tools/divide-and-conquer/SKILL.md) | 并行 | 分而治之提供问题分解的具体方法 |
| [first-principles](../thinking/first-principles/SKILL.md) | 前置 | 第一性原理从最基本部分重建理解 |
| [holism](../thinking/holism/SKILL.md) | 互补 | 整体论强调系统整体性，与还原论形成对比 |

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

1. Descartes, R. (1637). *Discourse on the Method*. (Part II: Rules for the Direction of the Mind)
2. Simon, H. A. (1962). The architecture of complexity. *Proceedings of the American Philosophical Society*, 106(6), 467-482.
3. Wimsatt, W. C. (2007). *Re-Engineering Philosophy for Limited Beings: Piecewise Approximations to Reality*. Harvard University Press.
4. Anderson, P. W. (1972). More is different. *Science*, 177(4047), 393-396.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
