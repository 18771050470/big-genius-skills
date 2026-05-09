---
name: holism
description: |
  触发：当需要理解系统整体行为、需要识别部分间关系产生的涌现属性、需要评估系统层面干预效果时调用；常见信号包括"整体来看"、"系统层面"、"牵一发而动全身"。
  不触发：当只需理解单个组件功能时；当系统各部分完全独立、无交互时；当还原论分析已足够解决问题时。
  Invoke when needing to understand system-level behavior, identify emergent properties from part relationships, or evaluate system-level intervention effects.
  Do NOT invoke when only understanding single component function, when system parts are completely independent without interaction, or when reductionist analysis is sufficient.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["systems-thinking", "reductionism", "leverage-points", "second-order-thinking"]
---

# 整体论思维（Holism Thinking）

## 核心定义

系统整体具有其组成部分所不具备的属性和行为。Aristotle提出"整体大于部分之和"，Smuts在1926年正式提出"holism"概念。整体论强调：理解系统不能仅通过理解部分，必须理解部分之间的关系和系统整体结构。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统整体行为特征、部分间关系和系统层面干预历史
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别系统整体行为和涌现属性，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别系统整体特征

- 系统表现出哪些部分不具备的行为？
- 系统是否有自组织、自适应能力？
- 系统是否有涌现属性（无法从部分推导）？
- 系统整体目标与部分目标是否一致？

---

### Step 2: 分析部分间关系网络

- 部分之间如何连接？连接密度如何？
- 关系是强连接还是弱连接？
- 是否存在关键连接（移除后系统分裂）？
- 关系网络是否有层级结构或模块化结构？

---

### Step 3: 识别涌现行为

- 哪些系统行为是部分交互的产物？
- 涌现行为是否可预测？
- 涌现行为对系统功能的影响？
- 是否有负涌现（部分优秀但整体差）？

---

### Step 4: 评估系统层面干预

- 干预对系统整体的影响 vs 对部分的影响
- 干预是否产生二阶效应？
- 干预是否改变部分间关系？
- 是否有杠杆点（小干预产生大影响）？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **整体≠部分之和**：系统整体行为无法通过单独分析部分来理解。原因：部分之间的非线性交互产生新属性，这些属性不存在于任何单独部分中。
2. **关系比实体更重要**：系统的核心是部分之间的关系，而非部分本身。原因：改变关系可以改变系统行为，即使部分不变。
3. **涌现不可还原**：涌现行为无法从部分属性推导，必须在系统层面理解。原因：涌现是交互的产物，不是部分的属性。
4. **杠杆点在小不在大**：系统中最有效的干预点往往不是最明显的部分。原因：杠杆点位于系统结构和规则层面，而非实体层面。

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
- [ ] 系统整体特征是否被识别？
- [ ] 部分间关系网络是否被分析？
- [ ] 涌现行为是否被识别和评估？
- [ ] 系统层面干预效果是否被评估？
- [ ] 是否识别了杠杆点？
- [ ] 输出具体可执行，不含模糊建议（如"整体考虑"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [systems-thinking](../thinking/systems-thinking/SKILL.md) | 前置 | 系统思维提供分析系统结构的框架 |
| [reductionism](../thinking/reductionism/SKILL.md) | 互补 | 还原论关注部分，整体论关注整体，两者互补 |
| [leverage-points](../thinking/leverage-points/SKILL.md) | 并行 | 杠杆点识别系统中最有效的干预点 |
| [second-order-thinking](../thinking/second-order-thinking/SKILL.md) | 并行 | 二阶思维评估干预的长期和间接影响 |

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

1. Aristotle. *Metaphysics*. (Book VIII, 1045a)
2. Smuts, J. C. (1926). *Holism and Evolution*. Macmillan.
3. von Bertalanffy, L. (1968). *General System Theory: Foundations, Development, Applications*. George Braziller.
4. Meadows, D. H. (1999). Leverage points: Places to intervene in a system. *The Sustainability Institute*.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
