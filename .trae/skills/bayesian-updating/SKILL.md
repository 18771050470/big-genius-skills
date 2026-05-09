```yaml
---
name: bayesian-updating
description: |
  触发：当需要根据新证据持续校准判断、更新已有结论或调整概率估计时调用；常见信号包括预测与事实不符、收到不确定新数据、需要量化推理过程。
  不触发：当已有确定性结论且无需新证据的场景；当证据质量极低或存在系统性偏差无法量化更新时；当需要快速行动且没有足够时间评估概率时。
  Invoke when facing decisions requiring iterative belief revision based on new evidence, especially when prior knowledge exists and uncertainty needs to be quantified.
  Do NOT invoke when conclusions are already certain, evidence quality is too low, or when quick action is needed without time for probability assessment.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["confirmation-bias", "critical-thinking", "first-principles", "systems-thinking"]
---
```

# 贝叶斯更新 (Bayesian Updating)

## 核心定义

根据新证据不断更新判断，遵循先验概率 + 新证据 → 后验概率的贝叶斯公式，持续校准置信度，实现对不确定性的量化动态管理。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

> 思维类 Skill 的核心模块。引导 Agent 怎么思考，不规定数据流转格式。
> 4-8 个步骤，每步只写思考要点，不写输入/输出格式。
> 占全文 40-60% 篇幅。

### Step 1: 定义先验概率

- 用数值 [0,1] 表示假设为真的初始置信度
- 若信息不足，采用均匀分布或最大熵原则
- 明确先验的来源：历史数据、专家判断还是主观估计
- 标注先验的不确定性

---

### Step 2: 收集新证据

- 筛选与假设相关的客观证据，去除噪声或无关信息
- 记录证据来源与可靠性
- 评估证据的独立性与相关性
- 判断证据质量是否足以支持更新

---

### Step 3: 评估似然

- 量化假设成立下观察到该证据的概率 P(E|H)
- 量化假设不成立下观察到该证据的概率 P(E|¬H)
- 使用频率统计、专家判断或模拟估计
- 检查是否陷入确认偏差（只关注支持证据）

---

### Step 4: 计算后验概率

- 代入贝叶斯公式计算更新后的置信度
- 检查分母（归一化常数）是否正确包含备择假设
- 验证后验概率是否在合理范围内 [0,1]
- 与直觉对比，若差异过大则检查似然评估

---

### Step 5: 评估更新幅度

- 检查更新幅度是否与证据强度匹配
- 避免对噪声证据反应过度
- 若证据强度有限，保留适度惯性
- 决定是否接受新先验或暂缓更新

---

### Step 6: 迭代准备

- 将后验作为新的先验，等待下一轮证据
- 明确下一步需要何种证据才能进一步改善置信度
- 记录本次更新的关键假设和局限性
- 规划持续校准的节奏

---

### Step 7: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

> 使用此思维模型时必须遵守的原则。3-5 条。每条包含"原则 + 原因/后果"。

1. **量化不确定性**：始终用概率而非直觉表示置信度，避免模糊词语如"很可能"。原因：概率提供可比较、可更新的数字基础。
2. **区分先验与证据**：先验代表已有知识，证据必须独立且可观察，不可混淆。原因：防止循环论证，确保更新源自外部信息。
3. **考虑备择假设**：似然评估必须包含假设为假的情形，否则更新失真。原因：仅看 P(E|H) 会导致确认偏差，低估反证价值。
4. **节制单次更新幅度**：证据强度有限时，不应过度跳跃，应保留适度惯性。原因：避免噪声驱动的不稳定判断，保持鲁棒性。
5. **持续迭代**：贝叶斯更新本质是循环过程，一次更新不是终点。原因：科学思维要求在低成本下不断校准，积累后趋近真相。

---

## 自检清单

> 聚焦贝叶斯更新最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**贝叶斯更新特供关键检查项**：

- [ ] **贝叶斯更新特供**：先验概率是否被明确声明？先验的来源（历史数据、专家判断、主观估计）是否被标注？先验的不确定性是否被量化？
- [ ] **贝叶斯更新特供**：是否同时评估了 P(E|H) 和 P(E|¬H)？似然比（Likelihood Ratio）是否被计算？只看支持证据是否会导致确认偏差？
- [ ] **贝叶斯更新特供**：证据质量是否被独立评估？证据来源、可靠性和独立性是否被审查？噪声证据是否被错误地赋予了过高更新权重？
- [ ] **贝叶斯更新特供**：更新幅度是否与证据强度匹配？贝叶斯因子（Bayes Factor）是否被用于量化证据强度？是否存在对弱证据反应过度或对强证据反应不足？
- [ ] **贝叶斯更新特供**：后验概率是否经过合理性检查？计算结果是否与直觉严重冲突？冲突时是否回溯检查计算过程和似然评估？
- [ ] **贝叶斯更新特供**：是否规划了持续校准的节奏？贝叶斯更新是循环过程，下一步需要什么证据才能进一步改善置信度是否被明确？后验是否被准备作为新的先验？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 贝叶斯更新是概率思维的具体实现机制，两者常结合使用 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 防范 | 贝叶斯更新天然要求评估反证，可对抗确认偏误 |
| [decision-tree](../thinking/decision-tree/SKILL.md) | 后置 | 更新后的后验概率可作为决策树的输入参数 |
| [opportunity-cost](../thinking/opportunity-cost/SKILL.md) | 前置 | 在评估是否值得收集新证据时，考虑机会成本 |

---

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Bayes, T. (1763). An essay towards solving a problem in the doctrine of chances. *Philosophical Transactions of the Royal Society*, 53, 370-418.
2. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. Chapter 13-16.
3. Silver, N. (2012). *The Signal and the Noise: Why So Many Predictions Fail—but Some Don't*. Penguin Press.
4. Gelman, A., Carlin, J. B., Stern, H. S., & Rubin, D. B. (2013). *Bayesian Data Analysis* (3rd ed.). Chapman and Hall/CRC.
