---
name: curse-of-dimensionality
description: |
  触发：当处理高维数据、设计机器学习算法、评估数据稀疏性或优化搜索空间时；常见信号包括"高维"、"维度灾难"、"数据稀疏"、"距离失效"、"组合爆炸"。
  不触发：当数据维度低（<10维）、当使用对高维鲁棒的特定算法（如随机投影）、当问题本质上是低维时。
  Invoke when dealing with high-dimensional data, designing ML algorithms, assessing data sparsity, or optimizing search spaces.
  Do NOT invoke when data has low dimensionality (<10), when using high-dimension-robust algorithms, or when the problem is inherently low-dimensional.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["feature-engineering-thinking", "constraint-thinking", "scale-thinking", "pattern-recognition-thinking"]
---

# 维度灾难思维 (Curse of Dimensionality)

## 核心定义

随着数据维度增加，数据空间体积呈指数级增长，导致数据稀疏、距离度量失效、样本需求爆炸，使得基于距离或密度的算法性能急剧下降的现象。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充数据维度信息或算法约束
- **发现矛盾**：当降维导致信息损失与维度灾难之间需要权衡时，标记并寻求决策
- **提前终止**：当已找到合适的维度处理方案或确认当前维度可管理时

---

## 思考流程

### Step 1: 维度评估与风险识别

- 确定数据的原始维度数量
- 评估有效样本量与维度的比值（样本/维度）
- 识别是否存在维度灾难风险（通常维度>20且样本不足）
- 分析维度之间的相关性和冗余度

---

### Step 2: 维度灾难影响分析

- **数据稀疏性**：高维空间中数据点极度稀疏
  - 同样数量样本在高维中覆盖度急剧下降
- **距离集中现象**：所有点对的距离趋于相似
  - 最近邻和最远邻的距离比趋近于1
- **组合爆炸**：搜索空间随维度指数增长
  - 网格搜索、优化问题计算不可行
- **过拟合风险**：模型参数随维度增加，小样本易过拟合

---

### Step 3: 降维策略选择

- **特征选择**：移除不重要或冗余特征
  - 过滤法、包装法、嵌入法
- **线性降维**：PCA、LDA、SVD
  - 保留最大方差方向，去除噪声维度
- **非线性降维**：t-SNE、UMAP、Autoencoder
  - 保留局部结构或流形结构
- **随机投影**：Johnson-Lindenstrauss引理
  - 随机降维保持距离近似
- **特征哈希**：Hashing Trick
  - 将高维稀疏特征映射到低维稠密空间

---

### Step 4: 算法适配策略

- **选择对高维鲁棒的算法**：
  - 树模型（随机森林、梯度提升）
  - 线性模型（带正则化）
  - 核方法（需谨慎选择核函数）
- **避免对高维敏感的算法**：
  - K近邻（距离失效）
  - K-means（距离失效）
  - 高斯混合模型（协方差矩阵估计困难）

---

### Step 5: 样本增强策略

- **数据增强**：生成合成样本扩充数据
  - SMOTE、GAN、数据变换
- **迁移学习**：利用相关领域的预训练知识
  - 减少对本领域数据量的依赖
- **贝叶斯方法**：引入先验知识约束参数空间
  - 小样本下的正则化效果

---

### Step 6: 验证与监控

- 评估降维后的信息保留率
- 监控模型在降维前后的性能变化
- 设置维度阈值预警机制
- 输出应包含：风险评估 + 降维方案 + 算法选择 + 监控建议

---

## 关键原则

1. **指数增长认知**：理解高维空间体积的指数增长特性。原因：人类直觉基于三维空间，高维空间的稀疏性远超直觉。

2. **距离度量审慎**：在高维空间谨慎使用基于距离的算法。原因：距离集中现象使距离区分度丧失，算法失效。

3. **降维优先**：优先考虑降维而非直接处理高维数据。原因：降维能同时解决稀疏性、距离失效、计算成本多个问题。

4. **信息保留权衡**：在降维和信息保留之间寻找平衡。原因：过度降维丢失关键信息，降维不足无法缓解维度灾难。

5. **样本维度比**：关注有效样本量与维度的比值。原因：样本/维度比是判断维度灾难风险的关键指标。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**维度灾难特有关键检查项**：

- [ ] **是否评估了样本/维度比？** 是否处于维度灾难风险区？
- [ ] **选择的算法是否对高维鲁棒？** 还是基于距离的算法？
- [ ] **降维方案是否考虑了信息保留率？** 还是盲目降维？
- [ ] **是否考虑了距离集中现象的影响？**
- [ ] **降维后的性能是否经过验证？** 相比原始维度如何？
- [ ] **是否设置了维度监控机制？** 新数据维度变化如何处理？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [feature-engineering-thinking](../thinking/feature-engineering-thinking/SKILL.md) | 并行 | 通过特征选择降低维度 |
| [constraint-thinking](../thinking/constraint-thinking/SKILL.md) | 并行 | 在计算资源约束下处理高维问题 |
| [scale-thinking](../thinking/scale-thinking/SKILL.md) | 基础 | 理解规模变化（维度增加）带来的质变 |
| [pattern-recognition-thinking](../thinking/pattern-recognition-thinking/SKILL.md) | 后置 | 在降维后的空间中寻找模式 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Bellman, R. E. (1961). *Adaptive Control Processes: A Guided Tour*. Princeton University Press.
2. Beyer, K., Goldstein, J., Ramakrishnan, R., & Shaft, U. (1999). When Is "Nearest Neighbor" Meaningful? *Proceedings of the 7th International Conference on Database Theory*, 217-235.
3. Verleysen, M., & François, D. (2005). The Curse of Dimensionality in Data Mining and Time Series Prediction. *International Work-Conference on Artificial Neural Networks*, 758-770.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
