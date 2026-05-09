---
name: lateral-thinking
description: |
  触发：当需要打破思维定势、寻找非传统解决方案、面对难题常规思路无效时调用；常见信号包括"换个角度想想""有没有完全不同的方法""跳出框框思考""常规方法行不通"。
  不触发：当问题已有标准解决方案且执行即可时；当需要严谨逻辑推导而非创意发散时；当时间紧迫无法容忍探索性思考时。
  Invoke when needing to break mental fixedness, seek unconventional solutions, or when standard approaches fail.
  Do NOT invoke when standard solutions exist and only execution is needed, when rigorous logical deduction is required, or when time constraints prohibit exploratory thinking.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["creative-thinking", "first-principles-thinking", "constraint-thinking", "analogical-thinking"]
---

# 水平思考（Lateral Thinking）

## 核心定义

不沿直线逻辑推进，而是从侧面/非常规角度打破思维定势，寻找被垂直思考忽略的解决方案。由Edward de Bono于1967年提出，核心信条是"你无法通过把同一个洞挖得更深来在不同地方挖洞"。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充问题约束、可用资源和可接受的非传统程度
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已通过水平思考找到明确可行方案且无需进一步发散，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别思维定势

- 当前问题的默认假设是什么？（"必须这样做""一直都是这样"）
- 哪些假设是真实的约束，哪些只是习惯？
- 问题的边界是否被人为缩小？
- 标注所有被当作"理所当然"的前提

### Step 2: 应用水平思考技术

- **随机输入法**：引入一个完全无关的词/概念，强制建立连接
- ** provocation（激发）**：提出一个明显荒谬的陈述（前缀"Po"），从中推导有用想法
- **挑战法**：质疑"为什么必须这样做"，不问对错只问可能性
- **反转法**：将问题或解决方案的元素颠倒过来
- **类比迁移**：从完全不相关的领域寻找结构相似性
- 记录每个技术产生的所有想法，不评判可行性

### Step 3: 生成替代方案

- 从水平思考产生的想法中筛选有潜力的方向
- 每个方向至少发展出2-3个具体方案
- 标注每个方案打破的原始假设
- 评估每个方案的新颖程度（1-10评分）

### Step 4: 评估与收敛

- 用垂直思考（逻辑分析）评估每个方案的可行性
- 权衡新颖性 vs 可行性 vs 成本
- 识别"虚假新颖"：看起来新但实际上是旧方案包装
- 选择最优方案或方案组合

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **水平思考≠垂直思考的替代品**：水平思考生成可能性，垂直思考评估可能性。原因：两者互补，先用水平思考发散，再用垂直思考收敛。
2. **荒谬是通往创新的桥梁**：de Bono的"Po"（激发）技术故意制造荒谬，因为荒谬能打破思维定势。原因：大脑对合理陈述自动归类，只有荒谬才能迫使大脑建立新连接。
3. **假设是创新的敌人**：每个"理所当然"都可能是被忽略的创新点。原因：假设限制了搜索空间，挑战假设能打开新空间。
4. **随机性是结构化的工具**：随机输入法不是碰运气，而是强制大脑建立不寻常连接。原因：大脑的联想网络需要外部刺激才能跳出局部最优。

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
- [ ] 是否识别了当前思维定势和默认假设？
- [ ] 是否应用了至少2种水平思考技术（随机输入、激发、挑战、反转、类比）？
- [ ] 生成的方案是否真正打破了原始假设？还是只是表面包装？
- [ ] 是否用垂直思考评估了方案的可行性？
- [ ] 是否识别了"虚假新颖"方案？
- [ ] 输出具体可执行，不含模糊建议（如"换个角度"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [creative-thinking](../creative-thinking/SKILL.md) | 并行 | 创造性思维提供发散框架，水平思考提供具体技术 |
| [first-principles-thinking](../first-principles-thinking/SKILL.md) | 前置 | 第一性原理拆解假设，水平思考在拆解后重建非传统方案 |
| [constraint-thinking](../constraint-thinking/SKILL.md) | 并行 | 约束思维在限制中寻找解，水平思考打破限制本身 |
| [analogical-thinking](../analogical-thinking/SKILL.md) | 并行 | 类比思维提供跨领域迁移，水平思考提供强制连接技术 |

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

1. de Bono, E. (1967). *The Use of Lateral Thinking*. Jonathan Cape.
2. de Bono, E. (1990). *Lateral Thinking: Creativity Step by Step*. Harper & Row.
3. de Bono, E. (1992). *Serious Creativity: Using the Power of Lateral Thinking to Create New Ideas*. HarperBusiness.
4. de Bono, E. (1971). *Lateral Thinking for Management*. American Management Association.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
