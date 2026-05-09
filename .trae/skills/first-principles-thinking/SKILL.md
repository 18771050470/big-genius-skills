---
name: first-principles-thinking
description: |
  触发：当面对复杂问题需要从根本上重新理解、现有方案失效或成本过高、需要创新突破时调用；常见信号包括"为什么一定要这样做"、"有没有更本质的方法"、"抛开现有方案重新想"。
  不触发：当已有成熟方案且成本可接受时；当时间极紧迫、只需快速修复时；当问题本身已是基础层面、无需进一步拆解时。
  Invoke when facing complex problems requiring fundamental understanding, when existing solutions fail or are too costly, or when breakthrough innovation is needed.
  Do NOT invoke when mature solutions exist at acceptable cost, when time is extremely tight and only quick fixes are needed, or when the problem is already at a fundamental level.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["abductive-thinking", "reductionism", "abstract-thinking", "creative-thinking"]
---

# 第一性原理思维（First Principles Thinking）

## 核心定义

将问题拆解到不可再分的基本真理，然后从零重建解决方案，摆脱类比和经验的束缚。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充关键事实
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已拆解到公认的基础真理且重建方案明确，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别并质疑现有假设

- 列出当前问题领域的所有"常识"和"既定做法"
- 逐一质疑：这个假设是真的吗？还是只是习惯或传统？
- 区分"物理/数学定律级别的真理"和"人为约定的规则"
- 警惕"我们一直这样做"类型的隐性假设

---

### Step 2: 拆解到基本真理

- 将问题分解到不可再分的基本组成部分
- 基本真理的标准：在该领域内被公认、不可再简化、有实证支撑
- 物理问题拆解到物理定律，工程问题拆解到材料和能量约束，商业问题拆解到用户需求和经济规律
- 持续追问"为什么"直到触及基础层面

---

### Step 3: 从零重建解决方案

- 仅使用 Step 2 确认的基本真理作为构建块
- 忽略现有方案，从"如果我是第一个解决这个问题的人会怎么做"的角度思考
- 组合基本要素，构建新的解决路径
- 允许天马行空，但每一步必须有基本真理支撑

---

### Step 4: 验证重建方案的可行性

- 新方案是否满足原始问题的核心约束？
- 与现有方案对比，在成本、效率、可扩展性上的差异
- 识别新方案的技术风险和实现难度
- 评估从现有方案迁移到新方案的成本

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **质疑一切，但区分层级**：不是所有假设都值得质疑，优先质疑影响最大的假设。原因：无限质疑会导致分析瘫痪，必须聚焦关键约束。
2. **基本真理必须有实证支撑**：不能把个人信念当作基本真理。原因：第一性原理的力量在于其不可辩驳的基础，伪基础会导致整个重建方案崩塌。
3. **重建时忘掉现有方案**：类比思维是第一性原理的敌人。原因：一旦参考现有方案，就会不自觉地被其约束，失去从零创新的机会。
4. **接受重建方案可能不如现有方案**：第一性原理不保证更好，只保证理解更深。原因：现有方案可能经过多年迭代优化，新方案需要时间成熟。

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
- [ ] 基本真理是否有实证支撑，而非个人信念？
- [ ] 重建方案是否真正从零开始，而非现有方案的微调？
- [ ] 是否识别了所有关键假设并逐一质疑？
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [reductionism](../thinking/reductionism/SKILL.md) | 前置 | 还原论提供拆解方法论，第一性原理在拆解后重建 |
| [abductive-thinking](../thinking/abductive-thinking/SKILL.md) | 并行 | 当基本真理不足以唯一确定方案时，用溯因生成最佳解释 |
| [creative-thinking](../thinking/creative-thinking/SKILL.md) | 后置 | 重建阶段需要创造性组合基本要素 |
| [analogical-thinking](../thinking/analogical-thinking/SKILL.md) | 对比 | 第一性原理与类比思维互斥，但可用于对比验证 |

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

1. Aristotle. (c. 350 BCE). *Metaphysics*. Book V, Part 1.
2. Descartes, R. (1637). *Discourse on the Method*. Part II.
3. Musk, E. (2013). *The Tesla Master Plan*. Tesla Motors Blog.
4. Bezos, J. (2016). *Jeff Bezos's 2016 Letter to Shareholders*. Amazon.com, Inc.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
