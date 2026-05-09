---
name: structured-thinking-via-system-prompt
description: |
  触发：当需要确保输出符合特定格式、需要引导模型按特定流程思考、或需要约束模型的行为边界时；常见信号包括"按格式..."、"遵循规则..."、"结构化..."、"系统提示"。
  不触发：当开放式探索更有价值、当格式约束会限制创造力、当问题需要灵活应变时。
  Invoke when needing to ensure output follows specific format, guide model through specific thinking process, or constrain behavior boundaries.
  Do NOT invoke when open-ended exploration is more valuable, when format constraints limit creativity, or when flexibility is required.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["meta-thinking-thinking-about-thinking", "contract-thinking", "constraint-thinking", "code-as-communication"]
---

# 结构化思维（系统提示）(Structured Thinking via System Prompt)

## 核心定义

通过精心设计的系统级提示（System Prompt），在推理前预设思维框架、约束条件和输出规范，引导模型进行结构化、可预测、高质量的思考范式。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统提示的设计目标
- **发现矛盾**：当系统提示与任务需求冲突时，标记并请求用户决策
- **提前终止**：当系统提示已充分引导思考且目标达成时

---

## 思考流程

### Step 1: 目标分析与框架选择

- 明确需要解决的核心问题
- 确定期望的输出格式和质量标准
- 选择适合的思维框架（分析型/创造型/决策型）
- 识别需要约束的行为边界

---

### Step 2: 系统提示设计

- **角色定义**：明确模型应扮演的角色和身份
- **任务描述**：清晰描述需要完成的任务
- **约束条件**：设定必须遵守的规则和限制
- **输出规范**：定义期望的输出格式和结构
- **示例提供**：给出输入-输出示例（可选但推荐）

---

### Step 3: 提示验证与测试

- 检查提示的清晰度和无歧义性
- 验证提示是否覆盖了所有关键要求
- 测试提示在不同输入下的表现
- 识别潜在的边界情况和失效模式

---

### Step 4: 结构化执行

- 严格按照系统提示的框架进行思考
- 遵循预设的步骤和流程
- 在约束边界内寻找解决方案
- 保持输出格式的一致性

---

### Step 5: 输出格式化

- 将思考结果整理为预设格式
- 确保所有必需的字段都有内容
- 检查格式的一致性和完整性
- 标注超出预设框架的额外发现

---

### Step 6: 效果评估与迭代

- 评估输出是否符合预期质量标准
- 识别系统提示的有效部分和待改进部分
- 根据反馈优化系统提示设计
- 记录最佳实践和常见陷阱

---

## 关键原则

1. **前置约束**：在思考开始前就设定好规则和框架。原因：事后约束难以改变思维路径，前置约束从源头引导方向。

2. **清晰具体**：系统提示必须清晰、具体、无歧义。原因：模糊的提示会导致不一致的输出，具体提示确保可预测性。

3. **平衡引导与自由**：既要引导方向，又要保留必要的灵活性。原因：过度约束会扼杀创造力，适度引导才能发挥模型潜力。

4. **可验证性**：设计的约束和格式应便于验证。原因：无法验证的约束等于没有约束，可验证确保执行质量。

5. **迭代优化**：系统提示不是一次性的，需要持续优化。原因：初始设计总有改进空间，迭代使提示越来越有效。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**结构化思维特有关键检查项**：

- [ ] **系统提示是否清晰具体？** 有无歧义？
- [ ] **是否覆盖了角色、任务、约束、输出规范所有要素？**
- [ ] **约束条件是否可验证？** 如何判断是否遵守？
- [ ] **输出是否符合预设格式？** 所有必需字段都有吗？
- [ ] **是否在约束边界内保留了必要的灵活性？**
- [ ] **系统提示的效果是否经过评估？** 如何改进？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [meta-thinking-thinking-about-thinking](../thinking/meta-thinking-thinking-about-thinking/SKILL.md) | 基础 | 结构化思维是元思维在提示工程上的应用 |
| [contract-thinking](../thinking/contract-thinking/SKILL.md) | 并行 | 契约思维指导如何设计清晰的约束和接口 |
| [constraint-thinking](../thinking/constraint-thinking/SKILL.md) | 并行 | 约束思维帮助在限制中寻找最优解 |
| [code-as-communication](../thinking/code-as-communication/SKILL.md) | 并行 | 系统提示也是一种"代码"，需要清晰表达意图 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Reynolds, L., & McDonell, K. (2021). Prompt Programming for Large Language Models: Beyond the Few-Shot Paradigm. *Extended Abstracts of the 2021 CHI Conference on Human Factors in Computing Systems*, 1-7.
2. White, J., Fu, Q., Hays, S., Sandborn, M., Olea, C., Gilbert, H., Elnashar, A., Spencer-Smith, J., & Schmidt, D. C. (2023). A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT. *arXiv preprint arXiv:2302.11382*.
3. Liu, P., Yuan, W., Fu, J., Jiang, Z., Hayashi, H., & Neubig, G. (2023). Pre-train, Prompt, and Predict: A Systematic Survey of Prompting Methods in Natural Language Processing. *ACM Computing Surveys*, 55(9), 1-35.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
