---
name: simpsons-paradox
description: |
  触发：当分析分组数据与总体数据出现矛盾结论、评估聚合统计指标或进行因果推断时；常见信号包括"分组分析"、"总体vs分组"、"趋势反转"、"混杂变量"、"分层分析"。
  不触发：当数据无需分组分析、当各组样本分布均匀、当已明确控制所有混杂变量时。
  Invoke when analyzing grouped vs aggregate data with conflicting conclusions, evaluating aggregated statistics, or causal inference.
  Do NOT invoke when data doesn't require grouping, when groups have uniform distribution, or when all confounders are controlled.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["causal-thinking", "probabilistic-thinking", "ab-testing-thinking", "correlation-vs-causation"]
---

# 辛普森悖论 (Simpson's Paradox)

## 核心定义

在分组比较中占优势的一方，在总体比较中反而处于劣势的现象——由混杂变量（lurking variable）导致的统计关联反转，揭示了聚合数据可能掩盖真实关系。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充分组维度或潜在混杂变量
- **发现矛盾**：当分组结论与总体结论冲突时，标记并深入分析混杂因素
- **提前终止**：当已识别混杂变量并确定正确的分析层次时

---

## 思考流程

### Step 1: 数据分层检查

- 识别可能的分组维度（性别、年龄、地区、时间等）
- 检查各组的样本量分布是否均衡
- 分析分组变量与目标变量的关联性
- 评估是否存在潜在的分层结构

---

### Step 2: 总体vs分组分析对比

- **总体分析**：计算聚合层面的统计指标
- **分组分析**：按各维度分别计算统计指标
- **对比检查**：比较总体结论与各组结论是否一致
- **识别反转**：标记出现辛普森悖论的分组维度

---

### Step 3: 混杂变量识别

- **混杂变量定义**：
  - 与自变量相关
  - 与因变量相关
  - 不是自变量和因变量之间的中介变量
- **常见混杂变量**：
  - 样本量分布不均
  - 时间因素
  - 选择偏差
  - 测量方法差异

---

### Step 4: 因果机制分析

- 分析混杂变量如何影响自变量和因变量的关系
- 绘制因果图（Causal Diagram）理清关系
- 确定正确的条件化策略（何时分组、何时聚合）
- 评估不同分析层次的业务含义

---

### Step 5: 正确分析层次选择

- **应该分组的情况**：
  - 混杂变量是真实的因果前因
  - 各组代表不同的因果机制
  - 业务决策需要在组内比较
- **应该聚合的情况**：
  - 分组变量是结果而非原因
  - 总体效应是关注的重点
  - 分组差异是随机波动

---

### Step 6: 结论表述与建议

- 明确说明分析层次（总体或分组）
- 解释辛普森悖论出现的原因
- 提供基于正确分析层次的结论
- 输出应包含：悖论识别 + 混杂分析 + 正确结论 + 决策建议

---

## 关键原则

1. **分层优先**：优先进行分组分析，再考虑是否聚合。原因：聚合数据可能掩盖重要的组间差异，分层分析更接近真实机制。

2. **因果导向**：根据因果关系而非统计关联选择分析层次。原因：正确的条件化需要理解变量间的因果结构，而非仅凭数据表现。

3. **样本权重意识**：注意各组样本量的权重影响。原因：样本量不均可能导致大组主导总体结论，掩盖小组的真实模式。

4. **多维度验证**：从多个分组维度验证结论的稳健性。原因：单一分组可能遗漏其他混杂因素，多维度验证提高可靠性。

5. **业务语境解读**：结合业务语境判断哪个分析层次更有意义。原因：统计正确的结论不一定符合业务逻辑，需要综合判断。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**辛普森悖论特有关键检查项**：

- [ ] **是否进行了分层分析？** 还是仅看总体数据？
- [ ] **总体结论与分组结论是否一致？** 是否存在悖论？
- [ ] **是否识别了混杂变量？** 混杂变量与自变量、因变量的关系是什么？
- [ ] **选择的分析层次是否有因果依据？** 还是仅凭统计结果？
- [ ] **各组样本量分布是否均衡？** 是否存在大组主导？
- [ ] **结论是否经过多维度验证？** 稳健性如何？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [causal-thinking](../thinking/causal-thinking/SKILL.md) | 基础 | 理解变量间的因果关系，正确选择条件化策略 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 量化条件概率和边际概率的关系 |
| [ab-testing-thinking](../thinking/ab-testing-thinking/SKILL.md) | 并行 | 在实验分析中识别辛普森悖论 |
| [correlation-vs-causation](../thinking/correlation-vs-causation/SKILL.md) | 基础 | 区分相关性和因果性 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Simpson, E. H. (1951). The Interpretation of Interaction in Contingency Tables. *Journal of the Royal Statistical Society: Series B*, 13(2), 238-241.
2. Blyth, C. R. (1972). On Simpson's Paradox and the Sure-Thing Principle. *Journal of the American Statistical Association*, 67(338), 364-366.
3. Pearl, J. (2014). Comment: Understanding Simpson's Paradox. *The American Statistician*, 68(1), 8-13.
4. Hernán, M. A., Clayton, D., & Keiding, N. (2011). The Simpson's Paradox Unraveled. *International Journal of Epidemiology*, 40(3), 780-785.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
