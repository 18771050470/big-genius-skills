---
name: feature-engineering-thinking
description: |
  触发：当构建机器学习模型、数据预处理、提升模型性能或理解数据内在结构时；常见信号包括"特征提取"、"特征选择"、"数据转换"、"领域知识"、"特征重要性"。
  不触发：当使用端到端深度学习且特征自动学习、当数据已充分结构化、当特征工程成本超过收益时。
  Invoke when building ML models, preprocessing data, improving model performance, or understanding data structure.
  Do NOT invoke when using end-to-end deep learning with automatic feature learning, when data is already well-structured, or when feature engineering cost exceeds benefit.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["domain-driven-design", "first-principles", "constraint-thinking", "gigo-thinking"]
---

# 特征工程思维 (Feature Engineering Thinking)

## 核心定义

利用领域知识和数据理解，通过创造、选择、转换特征，将原始数据转化为更能有效表达问题本质、提升模型预测能力的输入表示的过程。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充领域知识或业务背景
- **发现矛盾**：当领域知识与数据表现冲突时，标记并寻求澄清
- **提前终止**：当特征已充分表达问题且边际收益递减时

---

## 思考流程

### Step 1: 业务理解与领域知识获取

- 深入理解业务问题和目标
- 收集相关领域知识和专家经验
- 识别影响目标的关键业务因素
- 建立数据字段与业务概念的映射

---

### Step 2: 数据探索与模式发现

- 分析各特征的分布、相关性、缺失情况
- 识别目标变量与特征的潜在关系
- 发现数据中的异常值和异常模式
- 评估特征的质量和可信度

---

### Step 3: 特征创造（Feature Creation）

- **基于领域知识**：根据业务逻辑创造有物理意义的特征
  - 例：用经纬度计算Haversine距离
  - 例：从时间戳提取时段特征（早高峰/晚高峰）
- **特征组合**：将多个特征组合产生新特征
  - 例：比率、差值、乘积、多项式特征
- **特征分解**：将复杂特征拆解为更细粒度
  - 例：地址拆分为省、市、区
- **聚合特征**：基于分组统计创造聚合特征
  - 例：用户历史平均消费、商品类别销量排名

---

### Step 4: 特征转换（Feature Transformation）

- **缩放与归一化**：统一量纲，处理不同尺度
  - 标准化（Z-score）、Min-Max缩放
- **分布变换**：处理偏态分布
  - 对数变换、Box-Cox变换
- **编码转换**：处理类别变量
  - One-Hot编码、Label编码、Target编码
- **时间特征提取**：从时间数据提取模式
  - 周期性编码（sin/cos）、时间差、趋势

---

### Step 5: 特征选择（Feature Selection）

- **过滤法**：基于统计指标筛选
  - 方差阈值、相关系数、卡方检验
- **包装法**：基于模型性能迭代选择
  - 递归特征消除（RFE）、前向/后向选择
- **嵌入法**：利用模型内置特征重要性
  - L1正则化、树模型的特征重要性
- **降维**：将高维特征映射到低维空间
  - PCA、t-SNE、Autoencoder

---

### Step 6: 验证与迭代

- 评估特征工程对模型性能的提升
- 分析特征重要性，识别关键特征
- 移除无效或冗余特征
- 根据反馈迭代优化特征集

---

## 关键原则

1. **领域知识优先**：优先创造有业务意义的特征。原因：领域知识特征往往比纯数学变换更有效、更可解释。

2. **可解释性平衡**：在追求性能的同时保持特征可解释性。原因：黑盒特征难以调试，可解释特征便于发现问题。

3. **避免数据泄露**：确保特征不会引入未来信息。原因：数据泄露导致过于乐观的评估，模型上线后失效。

4. **计算成本意识**：考虑特征工程的计算开销。原因：复杂的特征工程可能使推理延迟不可接受。

5. **迭代优化**：特征工程是迭代过程，非一次性完成。原因：初始假设可能不完善，需要数据反馈来优化。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**特征工程特有关键检查项**：

- [ ] **特征是否有明确的业务意义？** 还是纯数学变换？
- [ ] **是否存在数据泄露风险？** 特征是否使用了未来信息？
- [ ] **特征选择是否基于验证集而非测试集？**
- [ ] **是否考虑了特征工程的计算成本？** 推理时可行吗？
- [ ] **特征是否经过缩放/编码等必要转换？**
- [ ] **是否移除了无效或冗余特征？** 特征集是否精简？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [domain-driven-design](../thinking/domain-driven-design/SKILL.md) | 前置 | 利用领域知识指导特征创造 |
| [first-principles](../thinking/first-principles/SKILL.md) | 并行 | 从业务本质出发设计特征 |
| [constraint-thinking](../thinking/constraint-thinking/SKILL.md) | 并行 | 在计算资源约束下优化特征工程 |
| [gigo-thinking](../thinking/gigo-thinking/SKILL.md) | 后置 | 确保输入特征质量，避免垃圾入垃圾出 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Kuhn, M., & Johnson, K. (2019). *Feature Engineering and Selection: A Practical Approach for Predictive Models*. CRC Press.
2. Zheng, A., & Casari, A. (2018). *Feature Engineering for Machine Learning: Principles and Techniques for Data Scientists*. O'Reilly Media.
3. Michelucci, U. (2022). *Applied Deep Learning: Feature Engineering and Optimization*. Springer.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
