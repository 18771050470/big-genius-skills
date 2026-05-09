---
name: cross-validation-thinking
description: |
  触发：当评估机器学习模型性能、比较不同模型、选择超参数或估计模型泛化能力时；常见信号包括"模型评估"、"泛化误差"、"超参数调优"、"模型选择"、"避免过拟合"。
  不触发：当数据量极大且分布稳定、当使用预定义测试集、当时间序列数据需特殊处理时。
  Invoke when evaluating ML model performance, comparing models, selecting hyperparameters, or estimating generalization.
  Do NOT invoke when data is extremely large and stable, when using predefined test sets, or when time series requires special handling.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["bias-variance-tradeoff", "probabilistic-thinking", "ab-testing-thinking", "gigo-thinking"]
---

# 交叉验证思维 (Cross-Validation Thinking)

## 核心定义

通过将数据集多次划分为训练集和验证集，反复训练和评估模型，获得对模型泛化性能更稳定、更可靠估计的验证方法论。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充数据分布信息或评估目标
- **发现矛盾**：当不同折的验证结果差异巨大时，标记并分析原因
- **提前终止**：当已获得稳定的性能估计或确认模型不可行时

---

## 思考流程

### Step 1: 数据特性分析

- 评估数据总量和类别分布
- 识别是否存在类别不平衡
- 分析数据的时间依赖性（是否时间序列）
- 确定是否需要分层抽样

---

### Step 2: 交叉验证策略选择

- **K折交叉验证（K-Fold）**：
  - 标准选择：K=5或K=10
  - 数据量小：增大K（如K=10或留一法）
  - 数据量大：减小K（如K=3或K=5）
- **分层K折（Stratified K-Fold）**：
  - 类别不平衡时保持每折类别比例
  - 分类问题的首选方法
- **留一法（LOO）**：
  - 数据量极小（N<100）时使用
  - 计算成本高但偏差低
- **时间序列分割（Time Series Split）**：
  - 数据有时间依赖性时使用
  - 确保训练集始终在验证集之前

---

### Step 3: 评估指标确定

- **分类问题**：准确率、精确率、召回率、F1、AUC-ROC
- **回归问题**：MSE、RMSE、MAE、R²
- **排序问题**：NDCG、MAP
- **业务指标**：根据业务目标定制（如转化率、收入）
- 确定主要指标和次要指标

---

### Step 4: 执行交叉验证

- 按选定策略划分数据
- 每折训练模型并记录验证性能
- 确保每折使用相同的模型和超参数
- 记录训练时间和资源消耗

---

### Step 5: 结果分析与稳定性评估

- 计算各折性能的平均值和标准差
- 评估结果的稳定性（标准差是否可接受）
- 分析异常折的原因（数据分布差异？异常值？）
- 比较不同模型的交叉验证结果

---

### Step 6: 模型选择与置信评估

- 选择平均性能最优且稳定的模型
- 评估性能估计的置信区间
- 考虑模型复杂度和训练成本
- 输出应包含：性能估计 + 稳定性分析 + 模型选择建议 + 置信度评估

---

## 关键原则

1. **数据泄露防范**：确保验证数据不参与任何训练过程。原因：数据泄露导致过于乐观的估计，模型上线后性能骤降。

2. **分布一致性**：保持训练集和验证集的分布一致。原因：分布不一致使验证结果无法反映真实泛化性能。

3. **多次验证**：单次验证不可靠，需要多次重复。原因：数据划分的随机性影响结果，多次验证降低方差。

4. **指标对齐**：验证指标必须与业务目标对齐。原因：技术指标高但业务指标低是常见的模型失败模式。

5. **计算成本权衡**：在验证精度和计算成本之间平衡。原因：过高的K值提升有限但成本剧增。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**交叉验证特有关键检查项**：

- [ ] **是否存在数据泄露？** 验证数据是否参与了特征工程或预处理？
- [ ] **选择的K值是否合理？** 是否考虑了数据量和计算成本？
- [ ] **是否使用了分层抽样？** 类别分布是否在各折中保持一致？
- [ ] **评估指标是否与业务目标对齐？**
- [ ] **各折结果是否稳定？** 标准差是否过大？
- [ ] **时间序列数据是否使用了时间感知分割？**

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [bias-variance-tradeoff](../thinking/bias-variance-tradeoff/SKILL.md) | 前置 | 理解验证误差的偏差-方差分解 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 量化验证结果的不确定性 |
| [ab-testing-thinking](../thinking/ab-testing-thinking/SKILL.md) | 并行 | 实验设计与统计显著性检验 |
| [gigo-thinking](../thinking/gigo-thinking/SKILL.md) | 前置 | 确保验证数据质量，避免垃圾入垃圾出 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Kohavi, R. (1995). A Study of Cross-Validation and Bootstrap for Accuracy Estimation and Model Selection. *Proceedings of the 14th International Joint Conference on Artificial Intelligence*, 2, 1137-1143.
2. Arlot, S., & Celisse, A. (2010). A Survey of Cross-Validation Procedures for Model Selection. *Statistics Surveys*, 4, 40-79.
3. Bergmeir, C., & Benítez, J. M. (2012). On the Use of Cross-Validation for Time Series Predictor Evaluation. *Information Sciences*, 191, 192-213.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
