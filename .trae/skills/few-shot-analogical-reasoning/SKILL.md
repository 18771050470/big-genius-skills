---
name: few-shot-analogical-reasoning
description: |
  触发：当面对新类型问题、需要迁移已知领域知识到未知领域、或缺乏明确解决路径时；常见信号包括"类似..."、"参考..."、"迁移学习"、"类比"、"举一反三"。
  不触发：当问题类型完全已知且有标准解法、当示例可能引入偏见、当问题需要严格逻辑而非类比时。
  Invoke when facing novel problem types, needing to transfer knowledge from known to unknown domains, or lacking clear solution paths.
  Do NOT invoke when the problem type is well-known with standard solutions, when examples may introduce bias, or when strict logic rather than analogy is required.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["analogical-thinking", "pattern-recognition-thinking", "bayesian-updating", "first-principles"]
---

# 少样本类比推理 (Few-Shot Analogical Reasoning)

## 核心定义

通过提供少量示例（问题-推理-答案三元组），引导模型识别跨问题的抽象模式，并将该模式迁移应用到新问题的推理范式。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充示例或明确类比维度
- **发现矛盾**：当示例之间模式不一致时，停止并请求澄清
- **提前终止**：当已识别清晰模式且成功迁移到新问题时

---

## 思考流程

### Step 1: 示例分析与模式提取

- 仔细分析提供的示例（问题 → 推理 → 答案）
- 识别示例间的共同结构和解决模式
- 提取抽象的问题类型和对应的解决策略
- 标注每个示例的独特性和代表性

---

### Step 2: 关系映射识别

- 识别示例中的源域（已知）和目标域（待解决）
- 建立源域与目标域之间的对应关系
- 识别属性映射（A对应A'、B对应B'）
- 识别关系映射（R(A,B) 对应 R(A',B')）

---

### Step 3: 结构对齐与验证

- 验证源域和目标域的结构相似性
- 检查映射的一致性和完整性
- 识别可能的映射冲突或歧义
- 评估类比的有效性和适用边界

---

### Step 4: 知识迁移应用

- 将源域的解决策略迁移到目标域
- 根据目标域特性调整迁移方案
- 执行迁移后的推理过程
- 记录迁移过程中的假设和变形

---

### Step 5: 结果验证与校准

- 验证迁移结果的合理性
- 检查是否存在类比过度或类比不足
- 评估结果对源域示例的符合程度
- 如有偏差，回溯调整映射关系

---

### Step 6: 模式泛化与总结

- 从具体类比中提炼一般性原则
- 总结可复用的推理模式
- 标注模式的适用条件和边界
- 输出应包含：答案 + 类比映射说明 + 模式摘要 + 置信度评估

---

## 关键原则

1. **结构映射优先**：关注深层结构相似性而非表面相似性。原因：表面相似容易误导，结构相似才能确保有效迁移。

2. **多示例交叉验证**：使用多个示例交叉验证模式的稳健性。原因：单一示例可能包含特异性，多示例能提取真正的一般模式。

3. **关系中心**：重点关注元素间的关系而非元素本身。原因：类比的核心是关系结构的映射，属性只是关系的载体。

4. **边界意识**：明确类比的适用范围和失效条件。原因：所有类比都是有限的，超出边界会导致错误推理。

5. **动态调整**：根据迁移效果动态调整映射关系。原因：初始映射可能不完美，需要根据反馈迭代优化。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**少样本类比特有关键检查项**：

- [ ] **是否识别了示例间的共同模式？** 还是只记住了示例本身？
- [ ] **映射是基于结构相似性还是表面相似性？**
- [ ] **是否验证了映射的一致性和完整性？**
- [ ] **迁移过程中做了哪些必要的调整？** 为什么？
- [ ] **是否明确了类比的适用边界？** 什么时候会失效？
- [ ] **结果是否经过与示例的交叉验证？**

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [analogical-thinking](../thinking/analogical-thinking/SKILL.md) | 基础 | 少样本类比是类比思维的特定实现，利用示例引导类比 |
| [pattern-recognition-thinking](../thinking/pattern-recognition-thinking/SKILL.md) | 并行 | 从示例中识别抽象模式是类比推理的核心 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 后置 | 根据迁移效果动态更新模式置信度 |
| [first-principles](../thinking/first-principles/SKILL.md) | 对比 | 当类比失效时，回归第一性原理从头推导 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Brown, T., Mann, B., Ryder, N., Subbiah, M., Kaplan, J. D., Dhariwal, P., ... & Amodei, D. (2020). Language Models are Few-Shot Learners. *Advances in Neural Information Processing Systems*, 33, 1877-1901.
2. Webb, T., Holyoak, K. J., & Lu, H. (2023). Emergent Analogical Reasoning in Large Language Models. *Nature Human Behaviour*, 7(9), 1526-1541.
3. Ushio, A., Camacho-Collados, J., Wang, Y., Neves, L., Anke, L. E., Schockaert, S., & Rei, M. (2023). The Curious Case of Analogies: Investigating Analogical Reasoning in Large Language Models. *Proceedings of the AAAI Conference on Artificial Intelligence*, 38(17), 19137-19145.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
