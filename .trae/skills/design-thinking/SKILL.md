---
name: design-thinking
description: |
  触发：当需要以用户为中心解决复杂问题、需要创新方案、需要理解用户真实需求时调用；常见信号包括"用户到底需要什么"、"如何创新"、"我们是不是在解决错误的问题"。
  不触发：当问题是技术性的、有明确答案时；当只需优化已有方案、无需重新定义问题时；当时间极紧迫、只需快速修复时。
  Invoke when needing user-centered solutions for complex problems, requiring innovation, or understanding real user needs.
  Do NOT invoke when the problem is technical with clear answers, when only optimizing existing solutions without redefining the problem, or when time is extremely tight and only quick fixes are needed.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["first-principles", "empathy-mapping", "iteration-thinking", "counterfactual-thinking"]
---

# 设计思维（Design Thinking）

## 核心定义

以用户为中心的创新方法论，通过共情（Empathize）→定义（Define）→构思（Ideate）→原型（Prototype）→测试（Test）的迭代循环，发现用户真实需求并创造创新解决方案。IDEO和Stanford d.school推广。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充用户画像、使用场景和现有解决方案的痛点
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已完成原型测试且获得明确用户反馈，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 共情（Empathize）

- 深入理解用户：观察、访谈、沉浸体验
- 区分用户说的和做的：言行不一是洞察来源
- 识别未表达的需求：用户不知道自己要什么，直到你展示给他们
- 收集情感线索：挫折、惊喜、困惑都是需求信号

---

### Step 2: 定义（Define）

- 将共情阶段的洞察整合为清晰的问题陈述
- 使用POV（Point of View）格式：[用户]需要[需求]因为[洞察]
- 避免过早跳入解决方案：先确保问题定义正确
- 问题定义应该是人类中心的，不是技术中心的

---

### Step 3: 构思（Ideate）

- 生成大量创意，不评判、不筛选
- 使用头脑风暴规则：延迟评判、追求数量、鼓励疯狂想法、建立在他人想法上
- 超越渐进式改进：追求范式转换而非优化
- 收敛：将创意分类、组合、投票，选出最有潜力的方向

---

### Step 4: 原型（Prototype）

- 用最低成本制作可体验的原型：纸面原型、故事板、角色扮演
- 原型目的是学习，不是展示
- 快速制作，快速失败，快速学习
- 原型应该能引发用户真实反应，不是抽象讨论

---

### Step 5: 测试（Test）

- 让真实用户使用原型，观察行为而非听取意见
- 测试不是验证，是学习：失败比成功产生更多洞察
- 迭代：根据测试结果回到Define或Ideate阶段
- 记录学习：什么有效、什么无效、为什么

---

## 关键原则

1. **问题定义比解决方案更重要**：解决错误的问题比不解决问题更糟。原因：资源被浪费在无用方案上，且错失解决正确问题的机会。
2. **用户不知道自己要什么**：Henry Ford说"如果我问用户要什么，他们会说更快的马"。原因：用户受限于现有认知框架，创新者需要洞察未表达需求。
3. **原型即思考**：制作原型的过程就是思考的过程。原因：动手制作迫使抽象想法具体化，暴露隐藏的假设和矛盾。
4. **失败是学习工具**：快速失败比缓慢成功更有价值。原因：每次失败都排除一个错误方向，加速找到正确方向。

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
- [ ] 共情阶段是否区分了用户说的和做的？
- [ ] 问题定义是否使用POV格式？是否人类中心？
- [ ] 构思阶段是否产生了足够多的创意？
- [ ] 原型是否足够低成本、可快速迭代？
- [ ] 测试阶段是否观察了用户行为而非仅听取意见？
- [ ] 输出具体可执行，不含模糊建议（如"以用户为中心"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [first-principles](../thinking/first-principles/SKILL.md) | 并行 | 第一性原理重新定义问题，设计思维以用户为中心创新 |
| [iteration-thinking](../thinking/iteration-thinking/SKILL.md) | 并行 | 迭代思维提供快速循环节奏，设计思维提供创新框架 |
| [counterfactual-thinking](../thinking/counterfactual-thinking/SKILL.md) | 并行 | 反事实思维探索替代方案，设计思维生成创新创意 |
| [empathy-mapping](../thinking/empathy-mapping/SKILL.md) | 前置 | 共情地图是设计思维共情阶段的工具 |

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

1. Brown, T. (2009). *Change by Design: How Design Thinking Transforms Organizations and Inspires Innovation*. Harper Business.
2. Kelley, T., & Kelley, D. (2013). *Creative Confidence: Unleashing the Creative Potential Within Us All*. Crown Business.
3. Plattner, H., Meinel, C., & Leifer, L. (2011). *Design Thinking: Understand - Improve - Apply*. Springer.
4. Martin, R. L. (2009). *The Design of Business: Why Design Thinking is the Next Competitive Advantage*. Harvard Business Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
