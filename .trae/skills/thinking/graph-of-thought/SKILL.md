---
name: graph-of-thought
description: |
  触发：当面对需要非线性思考、多源信息融合、思维重组或复杂依赖关系的 elaborated 问题时；常见信号包括"多维关联"、"信息融合"、"思维网络"、"循环依赖"、"协同增强"。
  不触发：当问题本质上是线性序列、当信息之间无复杂依赖、当简单链式或树状结构足够时。
  Invoke when facing elaborated problems requiring non-linear thinking, multi-source information fusion, or thought recombination.
  Do NOT invoke when the problem is essentially linear, when information has no complex dependencies, or when simple chain/tree structures suffice.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L3"
  related: ["chain-of-thought", "tree-of-thought", "system-thinking", "latticework-thinking"]
---

# 思维图推理 (Graph-of-Thought)

## 核心定义

将推理过程建模为任意图结构，其中思维单元作为节点、依赖关系作为边，支持聚合、精炼、生成等图操作，实现超越线性和树状结构的灵活推理范式。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充节点间的潜在关系
- **发现矛盾**：识别图中的循环依赖或逻辑冲突，标记并寻求消解
- **提前终止**：当图结构已充分覆盖问题空间且收敛到稳定解时

---

## 思考流程

### Step 1: 节点识别与初始化

- 识别问题中的所有关键思维单元（概念、事实、假设、子问题）
- 将每个单元初始化为图中的节点
- 为节点标注类型和属性（事实型/假设型/推理型）
- 评估每个节点的置信度和重要性

---

### Step 2: 关系映射与边构建

- 分析节点之间的依赖关系（A依赖B、A增强B、A矛盾B）
- 构建有向边表示依赖方向
- 标注边的类型（因果、支持、反驳、类比、组合）
- 识别并标注强连接组件和关键路径

---

### Step 3: 图操作执行

- **聚合（Aggregation）**：将多个相关节点合并为更高层次的抽象节点
- **精炼（Refinement）**：对节点进行细化，分解为更具体的子节点
- **生成（Generation）**：基于现有节点生成新的推理节点
- **遍历（Traversal）**：沿特定路径遍历图，提取推理链

---

### Step 4: 循环与反馈处理

- 识别图中的循环结构（正反馈/负反馈回路）
- 分析循环对推理稳定性的影响
- 处理相互依赖的节点（需要联合求解）
- 评估系统的整体收敛性

---

### Step 5: 协同增强与融合

- 识别可以相互增强的节点组合
- 通过信息融合提升节点置信度
- 发现跨领域的类比和迁移机会
- 构建协同效应网络

---

### Step 6: 全局优化与求解

- 从图的整体结构出发寻找最优解
- 考虑多目标优化（准确性、效率、简洁性）
- 识别图中的关键节点（移除会显著改变结果）
- 验证解的全局一致性和鲁棒性

---

### Step 7: 结构化输出

- 将图结构转化为可理解的推理说明
- 突出关键路径和核心洞察
- 标注不确定性和替代路径
- 输出应包含：结论 + 图结构摘要 + 关键洞察 + 置信度评估

---

## 关键原则

1. **关系优先**：关注节点间的连接关系而非孤立节点。原因：复杂问题的本质在于关系网络，而非独立事实的堆砌。

2. **动态重构**：图结构不是静态的，随推理深入不断演化。原因：新信息可能改变关系，静态图会限制推理灵活性。

3. **多源融合**：主动寻找不同来源信息的连接点。原因：创新往往发生在知识领域的交叉处。

4. **循环认知**：承认并正确处理循环依赖。原因：现实世界中循环反馈普遍存在，回避会导致模型失真。

5. **层次抽象**：在不同抽象层次上维护图的视图。原因：细节和全局视角互补，单一层次难以把握全貌。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**思维图特有关键检查项**：

- [ ] **是否识别了所有关键节点？** 有无遗漏重要思维单元？
- [ ] **节点间的关系是否被明确标注？** 边的类型清晰吗？
- [ ] **是否执行了图操作（聚合/精炼/生成）？** 还是只是静态图？
- [ ] **如何处理循环依赖？** 有明确的消解策略吗？
- [ ] **是否发现了跨节点的协同增强机会？**
- [ ] **最终解是否考虑了图的全局结构？** 还是局部最优？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [chain-of-thought](../thinking/chain-of-thought/SKILL.md) | 基础 | GoT是CoT的图泛化，当线性结构不够时使用GoT |
| [tree-of-thought](../thinking/tree-of-thought/SKILL.md) | 基础 | GoT是ToT的进一步扩展，支持更复杂的图结构 |
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 系统思维提供反馈回路和整体视角，GoT提供结构化表达 |
| [latticework-thinking](../thinking/latticework-thinking/SKILL.md) | 并行 | 思维模型格栅提供跨领域节点，GoT构建它们的关系网络 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Besta, M., Blach, N., Kubicek, A., Gerstenberger, R., Podstawski, M., Gianinazzi, L., Gajda, J., Lehmann, T., Niewiadomski, H., Nyczyk, P., & Hoefler, T. (2024). Graph of Thoughts: Solving Elaborate Problems with Large Language Models. *Proceedings of the AAAI Conference on Artificial Intelligence*, 38(16), 17682-17690.
2. Yao, Y., Wang, P., Tian, B., Cheng, S., Li, Z., Deng, S., Chen, H., & Li, N. (2024). GoT: Effective Graph-of-Thought Reasoning in Language Models. *Findings of the Association for Computational Linguistics: NAACL 2024*, 2911-2925.
3. Zhang, D., Hu, Z., Zhou, Y., Du, K., Chen, J., & Huang, F. (2024). Exploring the Uncertainty of LLM Explanations in Graph of Thoughts. *arXiv preprint arXiv:2409.03284*.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
