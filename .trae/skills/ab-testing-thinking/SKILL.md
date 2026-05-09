---
name: ab-testing-thinking
description: |
  触发：当评估产品改动效果、比较不同方案、验证假设或进行因果推断时；常见信号包括"实验"、"对照组"、"转化率"、"统计显著"、"p值"、"置信区间"。
  不触发：当无法进行随机分组、当样本量不足以检测效应、当伦理或法律禁止实验时。
  Invoke when evaluating product changes, comparing alternatives, validating hypotheses, or causal inference.
  Do NOT invoke when randomization is impossible, when sample size is insufficient, or when ethics/law prohibit experimentation.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["probabilistic-thinking", "cross-validation-thinking", "bayesian-updating", "causal-thinking"]
---

# A/B测试思维 (A/B Testing Thinking)

## 核心定义

通过随机将用户分为对照组（A）和实验组（B），控制其他变量，比较两组在关键指标上的差异，从而科学评估改动因果效果的实验方法论。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充业务指标定义或实验约束
- **发现矛盾**：当实验结果与业务直觉严重冲突时，标记并分析原因
- **提前终止**：当达到统计显著性或确认实验无法得出结论时（提前终止需谨慎）

---

## 思考流程

### Step 1: 实验目标与假设定义

- 明确实验要验证的核心假设
- 定义主要指标（North Star Metric）
- 定义 guardrail 指标（不能损害的指标）
- 设定实验成功/失败的标准

---

### Step 2: 实验设计

- **样本量计算**：
  - 确定最小可检测效应（MDE）
  - 设定统计功效（通常80%）和显著性水平（通常5%）
  - 计算所需样本量和实验时长
- **随机化策略**：
  - 用户级随机 vs 会话级随机
  - 确保随机化无偏（检查预实验指标平衡性）
- **分流比例**：
  - 通常50/50，可根据风险调整（如90/10）

---

### Step 3: 实验执行与监控

- 确保实验组和对照组正确分流
- 监控实验运行状态（样本积累速度、技术故障）
- 检查 guardrail 指标是否异常
- 避免"偷看"结果导致的过早结论（peeking problem）

---

### Step 4: 统计分析

- **点估计**：计算两组指标差异
- **置信区间**：估计效应大小的置信区间
- **统计显著性**：计算p值，判断是否<显著性水平
- **实际显著性**：评估效应大小是否具有业务意义
- **细分分析**：按用户群体、设备、地域等维度分析

---

### Step 5: 结果解释与决策

- **统计显著 + 实际显著**：建议上线
- **统计显著 + 实际不显著**：效应太小，不值得上线
- **统计不显著**：无法拒绝零假设，实验无结论
- **guardrail 指标受损**：即使主要指标提升也不应上线
- 考虑长期效应和副作用

---

### Step 6: 实验总结与学习

- 记录实验设计、结果和决策
- 总结成功或失败的原因
- 沉淀实验洞察，指导后续实验
- 输出应包含：实验结论 + 统计结果 + 业务建议 + 后续行动

---

## 关键原则

1. **随机化是金标准**：随机分组是因果推断的基础。原因：随机化平衡了混杂变量，使两组唯一系统性差异是实验处理。

2. **样本量先行**：实验前必须计算所需样本量。原因：样本不足导致统计功效低，无法检测真实效应。

3. **指标分层**：区分主要指标、次要指标和guardrail指标。原因：防止指标钓鱼（cherry-picking），确保全面评估。

4. **统计vs实际显著**：统计显著不等于业务价值。原因：大样本可使微小效应统计显著，但业务上无意义。

5. **避免偷看**：实验进行中不要频繁查看结果做决策。原因：多次检验增加假阳性概率，破坏统计有效性。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**A/B测试特有关键检查项**：

- [ ] **随机化是否正确执行？** 两组基线指标是否平衡？
- [ ] **样本量是否充足？** 是否达到预设的统计功效？
- [ ] **是否存在"偷看"问题？** 实验过程中是否多次查看结果？
- [ ] **guardrail指标是否受损？** 是否只关注了主要指标？
- [ ] **效应是否具有实际业务意义？** 还是仅统计显著？
- [ ] **实验时长是否足够？** 是否覆盖了完整的用户行为周期？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 基础 | 理解p值、置信区间的概率含义 |
| [cross-validation-thinking](../thinking/cross-validation-thinking/SKILL.md) | 并行 | 离线实验设计与在线A/B测试结合 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 进阶 | 使用贝叶斯A/B测试动态更新信念 |
| [causal-thinking](../thinking/causal-thinking/SKILL.md) | 基础 | 理解随机化如何实现因果推断 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Kohavi, R., Tang, D., & Xu, Y. (2020). *Trustworthy Online Controlled Experiments: A Practical Guide to A/B Testing*. Cambridge University Press.
2. Kohavi, R., Crook, T., Longbotham, R., Frasca, B., Henne, R., Ferres, J. L., & Melamed, T. (2012). Online Controlled Experiments at Large Scale. *Proceedings of the 19th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, 1168-1176.
3. Johari, R., Koomen, P., Pekelis, L., & Walsh, D. (2017). Peeking at A/B Tests: Why It Matters, and What to Do about It. *Proceedings of the 23rd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, 1517-1525.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
