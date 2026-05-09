---
name: ensemble-thinking
description: |
  触发：当追求更高预测精度、提升模型稳定性、降低过拟合风险或处理复杂模式时；常见信号包括"集成学习"、"随机森林"、"梯度提升"、"模型融合"、"投票"、"堆叠"。
  不触发：当模型解释性优先于精度、当计算资源极其有限、当单一简单模型已足够时。
  Invoke when pursuing higher prediction accuracy, improving model stability, reducing overfitting, or handling complex patterns.
  Do NOT invoke when model interpretability is prioritized, when compute resources are extremely limited, or when a single simple model suffices.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["bias-variance-tradeoff", "divide-and-conquer", "probabilistic-thinking", "redundancy-thinking"]
---

# 集成思维 (Ensemble Thinking)

## 核心定义

通过组合多个基学习器的预测结果，利用"群体智慧"降低单个模型的偏差和方差，获得比任何单一模型更优、更稳定的预测性能的机器学习方法论。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充模型性能数据或集成约束
- **发现矛盾**：当集成模型性能不如单一模型时，标记并分析原因
- **提前终止**：当集成收益递减或计算成本超过收益时

---

## 思考流程

### Step 1: 基学习器分析

- 评估单一基学习器的性能（偏差、方差）
- 分析基学习器之间的相关性和多样性
- 识别基学习器的错误模式（是否互补）
- 确定集成策略的适用性

---

### Step 2: 集成策略选择

- **Bagging（并行集成）**：
  - 适用：高方差、低偏差模型（如决策树）
  - 方法：随机森林、Extra Trees
  - 原理：通过Bootstrap采样降低方差
- **Boosting（串行集成）**：
  - 适用：高偏差、低方差模型（如浅层树）
  - 方法：AdaBoost、Gradient Boosting、XGBoost、LightGBM
  - 原理：串行纠正前序模型错误，降低偏差
- **Stacking（模型堆叠）**：
  - 适用：异构模型组合
  - 方法：用元学习器组合基学习器输出
  - 原理：学习最优的组合权重
- **Voting（投票）**：
  - 适用：同构模型或性能相近模型
  - 方法：硬投票（多数决）或软投票（概率平均）

---

### Step 3: 多样性保障

- **数据层面**：
  - Bootstrap采样（Bagging）
  - 不同特征子集（Random Subspace）
- **模型层面**：
  - 不同类型算法（树、线性、神经网络）
  - 不同超参数配置
- **训练层面**：
  - 不同初始化
  - 不同训练数据顺序

---

### Step 4: 集成模型训练

- 按选定策略训练基学习器
- 确保基学习器之间的独立性（避免相关性过高）
- 对于Stacking，划分训练集和元学习器训练集
- 监控训练过程中的过拟合迹象

---

### Step 5: 组合策略优化

- **简单平均**：基学习器性能相近时使用
- **加权平均**：根据验证性能分配权重
- **学习组合**：用元学习器学习最优组合
- **动态选择**：根据输入特征动态选择基学习器

---

### Step 6: 性能评估与权衡

- 比较集成模型与单一模型的性能
- 评估性能提升与计算成本的权衡
- 分析集成模型的可解释性损失
- 输出应包含：集成方案 + 性能对比 + 成本分析 + 适用建议

---

## 关键原则

1. **多样性优于数量**：基学习器之间的多样性比数量更重要。原因：高度相关的基学习器无法通过平均降低方差，多样性带来互补性。

2. **偏差-方差针对性**：根据基学习器的偏差/方差特性选择集成策略。原因：Bagging降方差，Boosting降偏差，针对性选择才能有效。

3. **计算成本意识**：集成带来性能提升的同时也增加计算成本。原因：需要在精度和效率之间找到业务可接受的平衡点。

4. **避免过度集成**：过多的基学习器可能导致收益递减。原因：边际效益递减，且增加过拟合和计算风险。

5. **验证集独立**：集成权重的学习必须在独立验证集上进行。原因：在训练集上学习权重会导致过拟合估计。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**集成思维特有关键检查项**：

- [ ] **基学习器是否具有足够的多样性？** 相关性是否过高？
- [ ] **集成策略是否与基学习器特性匹配？** Bagging用于高方差？Boosting用于高偏差？
- [ ] **集成权重是否在独立验证集上学习？** 是否存在数据泄露？
- [ ] **集成收益是否超过计算成本？** 边际效益是否递减？
- [ ] **是否避免了过度集成？** 基学习器数量是否合理？
- [ ] **集成模型的可解释性损失是否可接受？**

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [bias-variance-tradeoff](../thinking/bias-variance-tradeoff/SKILL.md) | 基础 | 理解集成如何影响偏差和方差 |
| [divide-and-conquer](../thinking/divide-and-conquer/SKILL.md) | 并行 | 将复杂问题分解为多个子问题分别建模 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 量化集成的概率优势 |
| [redundancy-thinking](../thinking/redundancy-thinking/SKILL.md) | 并行 | 通过冗余提升系统可靠性 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Breiman, L. (1996). Bagging Predictors. *Machine Learning*, 24(2), 123-140.
2. Freund, Y., & Schapire, R. E. (1997). A Decision-Theoretic Generalization of On-Line Learning and an Application to Boosting. *Journal of Computer and System Sciences*, 55(1), 119-139.
3. Wolpert, D. H. (1992). Stacked Generalization. *Neural Networks*, 5(2), 241-259.
4. Dietterich, T. G. (2000). Ensemble Methods in Machine Learning. *International Workshop on Multiple Classifier Systems*, 1-15.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
