
---
name: meta-thinking-thinking-about-thinking
description: |
  触发：当需要反思决策、评估思考质量、解决复杂问题、学习新知识或进行复盘时调用；常见信号包括"我刚才为什么那样想？"、"这个思路对吗？"、"我是不是陷入了偏见？"、"我该怎么改进我的思考？"。
  Invoke when facing decisions requiring introspection, evaluating thought quality, solving complex problems, learning new material, or conducting retrospectives; common signals include "Why did I think that?", "Is this reasoning correct?", "Am I falling into a bias?", "How can I improve my thinking?".
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["system-thinking", "first-principles-thinking", "reflective-thinking", "critical-thinking"]
---
# 元思维（Meta-Thinking / Thinking about Thinking）

## 核心定义

对自己的思维过程进行观察、评估和调节——"我知道我在想什么，我也能审视我为什么这样想"，是一切自我改进的基础。

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

## 思考流程

### Step 1: 觉察当前思维状态

- 暂停并问自己："我正在如何思考？" 记录思维的内容、语气、速度、情感色彩
- 清晰的觉察记录（例如："我正用直觉快速给出方案，情绪是焦虑的，没有验证数据"）

### Step 2: 识别思维模式与偏差

- 分析识别主流思维类型（分析型/直觉型/发散型）和可能的认知偏差（确认偏差、锚定效应等）
- 思维模式列表及偏差标记（例如："模式：快速判断 + 偏差：确认偏差，只找支持自己的证据"）

### Step 3: 评估思考质量

- 用元认知标准（逻辑一致性、证据充分性、目标相关性、情感干扰度）逐项评分（1-5分）
- 评估报告，包含各维度得分和改进建议

### Step 4: 选择调整策略

- 根据薄弱维度选择策略（如：证据不足→查找反例；情绪干扰→暂停呼吸并重述问题；逻辑跳跃→画决策树）
- 调整计划（如："先列出三个可能错误的假设，然后验证"）

### Step 5: 执行调整并再观察

- 按照计划改变思考方式，同时继续用元视角观察效果，记录变化
- 调整后的思考结果和元观察记录

### Step 6: 反思与内化

- 总结这次元思维练习的收获，提炼成一条可复用的元认知口诀或规则
- 一条元认知经验（如："当情绪评级超过7/10时，先做三次深呼吸再决策"）

## 关键原则

| 原则 | 内容 | 原因 |
|------|------|------|
| 第二层观察 | 建立"观察者-思考者"的双层结构，即我在思考的同时，还有一个"我"在看着自己思考 | 避免被直觉完全主导，提供修正的窗口 |
| 非评判性觉察 | 初期只描述不评判（如"我注意到我正在使用确认偏差"而非"我太蠢了"） | 评判会触发防御心理，阻碍真实观察 |
| 持续校准 | 元思维不是一次性的，每次练习后记录效果，逐步优化流程 | 大脑的元认知能力像肌肉，需要重复训练 |
| 多维度评估 | 对思考从逻辑、证据、目标、情绪四个维度综合打分 | 单维度评估（如只看逻辑）容易忽视整体质量 |
| 行动导向 | 元思维的终点必须是"接下来我该怎么做"的具体行动 | 单纯观察而不调节是无效的，改进才是目的 |

## 自检清单

> 聚焦元思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**元思维特有关键检查项**：

- [ ] **觉察记录是否是客观的？** "我正在快速给出方案，情绪焦虑，没有验证数据"而非"我太草率了"？
- [ ] **是否识别了至少一种思维模式或认知偏差？** 分析型/直觉型/发散型中哪种主导？
- [ ] **是否从逻辑、证据、目标、情绪四个维度评估了思考质量？** 单维度评估是否被避免？
- [ ] **评估分数是否基于具体事实？** 还是仅凭"感觉"打分？
- [ ] **调整策略是否具体到可执行？** "列出三个反例"而非"多思考"？
- [ ] **执行调整后是否重新做了元观察？** 改变思考方式后的效果是否被记录？
- [ ] **是否提炼出可复用的元认知规则？** 如"情绪评级超过7/10时，先做三次深呼吸再决策"？
- [ ] **是否陷入了"过度元思维"？** 在需要快速行动时，元思维是否反而造成了分析瘫痪？

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [系统思维](../system-thinking/SKILL.md) | 前置 | 在应用元思维之前，先用系统思维理解问题结构，确保元思维聚焦在关键环节 |
| [第一性原理](../first-principles-thinking/SKILL.md) | 后置 | 元思维识别出思维误区后，用第一性原理重新拆解问题本质 |
| [反思思维](../reflective-thinking/SKILL.md) | 并行 | 两者都注重回顾，但元思维更关注思考过程的自我观察，反思思维更关注经验教训提炼 |
| [批判性思维](../critical-thinking/SKILL.md) | 并行 | 批判性思维提供评估论证的工具，元思维则提供监控认知偏差的元视角，常组合使用 |

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Flavell, J. H. (1979). Metacognition and cognitive monitoring: A new area of cognitive-developmental inquiry. *American Psychologist*, 34(10), 906-911.
2. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux.
3. Schön, D. A. (1983). *The Reflective Practitioner: How Professionals Think in Action*. Basic Books.
4. Nelson, T. O., & Narens, L. (1990). Metamemory: A theoretical framework and new findings. *The Psychology of Learning and Motivation*, 26, 125-173.