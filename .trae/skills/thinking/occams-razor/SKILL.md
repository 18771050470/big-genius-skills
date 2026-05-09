---
name: occams-razor
description: |
  触发：当面对多个 competing 解释或方案、需要选择最简路径、防止过度设计时调用；常见信号包括"哪个方案更靠谱"、"是不是想复杂了"、"有没有更简单的做法"。
  不触发：当问题本身复杂、简单方案无法覆盖关键约束时；当已有明确证据支持复杂方案时；当"简单"的定义不明确、需要先澄清标准时。
  Invoke when facing multiple competing explanations or solutions, needing to choose the simplest path, or preventing over-engineering.
  Do NOT invoke when the problem is inherently complex and simple solutions cannot cover key constraints, when clear evidence supports a complex solution, or when the definition of "simple" is unclear and needs clarification first.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["minimalism-thinking", "anti-corrosion", "constraint-thinking", "first-principles-thinking"]
---

# 奥卡姆剃刀（Occam's Razor）

## 核心定义

在多个同等解释力的方案中，选择假设最少、实体最少、复杂度最低的那个。简单性不是目的，而是减少错误概率的策略。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充方案细节
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某方案明显更简单且解释力不弱于其他方案，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 列出所有候选方案/解释

- 穷举当前可行的解决方案或解释
- 确保每个方案都能解释已知事实
- 排除明显无法解释关键事实的方案
- 不预设偏好，保持开放

---

### Step 2: 评估解释力

- 每个方案能解释多少已知事实？
- 是否有方案能解释其他方案无法解释的现象？
- 是否有方案与已知事实矛盾？
- 解释力是剃刀应用的前提：解释力不等价的方案不能直接比简单性

---

### Step 3: 量化复杂度

- 计算每个方案的假设数量
- 计算每个方案引入的新实体/概念/依赖数量
- 评估实现复杂度：代码行数、维护成本、认知负荷
- 区分"表面简单"（看起来简单但隐含复杂）和"本质简单"（真正减少实体）

---

### Step 4: 应用剃刀选择

- 在解释力等价的方案中，选择假设最少的
- 如果简单方案解释力略弱，评估差距是否可接受
- 警惕"虚假简单"：表面简单但隐藏了关键假设
- 记录选择理由和放弃方案的原因

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **解释力优先于简单性**：剃刀只在解释力等价时适用。原因：选择更简单但解释力不足的方案会导致后续问题。
2. **区分简单与简陋**：简单是消除不必要的复杂，简陋是遗漏必要的组件。原因：过度简化会丢失关键信息，与剃刀本意相悖。
3. **复杂度必须可量化**：不能凭感觉判断"这个更简单"。原因：主观判断容易被熟悉度偏差影响，量化确保客观。
4. **剃刀是启发式而非定律**：简单方案不总是正确方案。原因：自然界和工程中确实存在复杂但必要的结构。

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
- [ ] 所有候选方案的解释力是否被公平评估？
- [ ] 复杂度是否被量化而非凭感觉判断？
- [ ] 是否警惕了"虚假简单"方案？
- [ ] 选择理由是否清晰记录了假设数量对比？
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [minimalism-thinking](../thinking/minimalism-thinking/SKILL.md) | 并行 | 最小主义追求功能精简，奥卡姆剃刀追求假设精简 |
| [first-principles-thinking](../thinking/first-principles-thinking/SKILL.md) | 前置 | 第一性原理拆解后，奥卡姆剃刀选择最简重建路径 |
| [anti-corrosion](../thinking/anti-corrosion/SKILL.md) | 后置 | 剃刀选择简单方案后，反腐蚀防止方案随时间变复杂 |
| [critical-thinking](../thinking/critical-thinking/SKILL.md) | 并行 | 批判性思维验证简单方案是否真的充分 |

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

1. Ockham, W. (1323). *Summa Logicae*. Part I, Chapter 12.
2. Sober, E. (2015). *Ockham's Razors: A User's Manual*. Cambridge University Press.
3. Thorburn, W. M. (1918). The evolution of Occam's razor. *Mind*, 27(105), 1-19.
4. Jaynes, E. T. (2003). *Probability Theory: The Logic of Science*. Cambridge University Press. Chapter 18.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
