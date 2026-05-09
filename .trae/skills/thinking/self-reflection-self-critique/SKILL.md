---
name: self-reflection-self-critique
description: |
  触发：当完成初步输出后需要质量提升、面对复杂问题需要迭代优化、或发现输出可能存在缺陷时；常见信号包括"检查..."、"改进..."、"反思..."、"优化..."、"迭代"。
  不触发：当时间紧迫且初稿质量可接受、当问题简单无需迭代、当过度反思会导致分析瘫痪时。
  Invoke when initial output needs quality improvement, facing complex problems requiring iterative optimization, or suspecting potential flaws.
  Do NOT invoke when time is critical and first draft is acceptable, when the problem is simple, or when over-reflection leads to analysis paralysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["critical-thinking", "iteration-thinking", "bayesian-updating", "second-order-thinking"]
---

# 自我反思与批判 (Self-Reflection / Self-Critique)

## 核心定义

通过让模型对自身输出进行批判性评估、识别缺陷、提出改进建议并迭代优化的元认知推理范式，实现无需外部监督的自我提升。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问明确质量标准或改进方向
- **发现矛盾**：当自我评估与原始输出存在根本性冲突时，标记并寻求用户决策
- **提前终止**：当迭代改进的收益低于成本或达到满意质量阈值时

---

## 思考流程

### Step 1: 初始输出生成

- 基于当前理解生成初步答案或方案
- 不追求完美，先完成再完善
- 记录生成过程中的关键假设
- 标注不确定性和已知局限

---

### Step 2: 多角度批判审视

- **正确性检查**：事实是否准确？逻辑是否严密？
- **完整性检查**：是否遗漏重要方面？边界条件是否考虑？
- **清晰性检查**：表达是否清晰？结构是否合理？
- **适用性检查**：是否真正回答了问题？是否满足用户需求？
- **偏见检查**：是否存在确认偏误？是否考虑了反方观点？

---

### Step 3: 缺陷识别与分类

- 列出发现的所有问题和不足
- 按严重程度分类（关键/重要/轻微）
- 分析问题根因（知识缺口/逻辑错误/表达不清）
- 评估修复的优先级和难度

---

### Step 4: 改进建议生成

- 针对每个缺陷提出具体的改进措施
- 考虑多种改进方案并比较优劣
- 评估改进措施的副作用和风险
- 选择最优改进策略组合

---

### Step 5: 迭代优化执行

- 根据改进建议修改原始输出
- 确保修改的一致性和连贯性
- 验证改进是否真正解决了问题
- 记录改进前后的对比

---

### Step 6: 收敛判断与终止

- 评估当前版本的质量水平
- 判断是否继续迭代或终止
- 设置最大迭代次数防止无限循环
- 输出应包含：最终版本 + 改进摘要 + 剩余局限 + 迭代次数

---

## 关键原则

1. **分离角色**：将"生成者"和"批判者"视为两个独立角色。原因：同一视角难以发现自身盲点，角色分离提升批判深度。

2. **具体批判**：批判必须具体到可操作的改进点。原因：模糊批判（"不够好"）无法指导改进，具体批判才能落地。

3. **证据优先**：基于证据而非感觉进行批判。原因：主观感觉容易偏差，证据支撑使批判客观可信。

4. **建设性导向**：批判的目的是改进而非否定。原因：破坏性批判会打击信心，建设性批判激发改进动力。

5. **适度迭代**：设置合理的迭代终止条件。原因：过度迭代可能导致过度优化或分析瘫痪，收益递减时需停止。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**自我反思特有关键检查项**：

- [ ] **是否真正分离了生成者和批判者角色？** 还是只是形式上的？
- [ ] **批判是否具体到了可操作的改进点？** 还是停留在模糊评价？
- [ ] **批判是否有证据支撑？** 还是基于主观感觉？
- [ ] **是否考虑了多个批判角度？** 还是只关注了某一方面？
- [ ] **迭代改进是否真正解决了识别的问题？**
- [ ] **迭代终止是否合理？** 是收益递减还是达到质量标准？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [critical-thinking](../thinking/critical-thinking/SKILL.md) | 基础 | 自我反思是批判性思维在自我评估上的应用 |
| [iteration-thinking](../thinking/iteration-thinking/SKILL.md) | 并行 | 迭代思维提供迭代框架，自我反思提供迭代内容 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 根据自我评估结果动态更新对答案的置信度 |
| [second-order-thinking](../thinking/second-order-thinking/SKILL.md) | 前置 | 反思改进措施的二阶后果，避免 unintended side effects |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Madaan, A., Tandon, N., Gupta, P., Hallinan, S., Gao, L., Wiegreffe, S., Alon, U., Dziri, N., Prabhumoye, S., Yang, Y., Welleck, S., Majumder, B. P., & Clark, P. (2023). Self-Refine: Iterative Refinement with Self-Feedback. *Advances in Neural Information Processing Systems*, 36.
2. Shinn, N., Cassano, F., Gopinath, A., Narasimhan, K., & Yao, S. (2023). Reflexion: Language Agents with Verbal Reinforcement Learning. *Advances in Neural Information Processing Systems*, 36.
3. Huang, J., Chen, X., Mishra, S., Zheng, H. S., Yu, A. W., Song, X., & Zhou, D. (2023). Large Language Models Cannot Self-Correct Reasoning Yet. *arXiv preprint arXiv:2310.01798*.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
