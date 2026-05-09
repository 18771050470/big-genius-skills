---
name: decision-tree
description: |
  触发：当需要在不确定环境下做序列决策、需要可视化各选项路径和结果、需要计算期望值时调用；常见信号包括"如果A发生就选B，否则选C"、"先做X再看情况"、"有多种可能结果"。
  不触发：当决策是简单的二选一、无需序列分析时；当所有结果确定、无不确定性时；当只需定性比较、无需量化期望值时。
  Invoke when needing to make sequential decisions under uncertainty, visualize option paths and outcomes, or calculate expected values.
  Do NOT invoke when decision is simple binary choice without sequential analysis, when all outcomes are certain without uncertainty, or when only qualitative comparison is needed without quantifying expected values.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["probabilistic-thinking", "expected-value", "scenario-planning", "bayesian-updating"]
---

# 决策树思维（Decision Tree Thinking）

## 核心定义

用树状结构可视化决策路径、可能结果和概率，计算各路径期望值以选择最优策略。Howard和Raiffa在1960年代发展决策树方法：决策节点（方形）、机会节点（圆形）、结果节点（三角形），通过逆向归纳法（rollback）从结果回溯到当前决策。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充各选项概率估计、结果金额和决策时间线
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若决策树已构建完毕且最优路径清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 构建决策树结构

- 当前决策点是什么？（决策节点）
- 每个决策有哪些可选行动？
- 每个行动后有哪些可能结果？（机会节点）
- 结果发生的概率是多少？结果的价值是多少？
- 是否有后续决策点？（序列决策）

---

### Step 2: 量化概率和结果

- 各结果概率估计：基于数据、专家判断还是直觉？
- 概率总和是否为1？（互斥且穷尽）
- 各结果的价值量化：用统一单位（如金额、效用）
- 标注概率来源和置信度

---

### Step 3: 计算期望值

- 各路径期望值 = Σ(概率 × 结果价值)
- 从结果节点逆向回溯到决策节点
- 在每个决策节点选择期望值最高的行动
- 标注计算过程和中间结果

---

### Step 4: 敏感性分析

- 哪些概率或结果值对决策影响最大？
- 如果概率估计偏差±10%，决策是否改变？
- 识别关键假设：哪些假设必须准确？
- 评估信息价值：获取更准确概率值得多少成本？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **期望值是最优决策标准**：长期重复决策中，选择期望值最高的行动产生最好结果。原因：大数定律保证，长期平均结果趋近期望值。
2. **概率估计质量决定决策质量**：垃圾概率输入产生垃圾决策输出。原因：期望值计算依赖概率，概率偏差直接导致期望值偏差。
3. **敏感性分析识别关键假设**：不是所有概率都同等重要，少数关键假设决定决策。原因：某些路径概率微小变化导致决策翻转，这些是敏感点。
4. **信息有价值**：获取更准确概率信息的价值 = 有完美信息时期望值 - 当前期望值。原因：更好信息减少不确定性，提高决策质量。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **记录方式**：自检结果写入 `self_check_result.md`（临时文件），包含：通过项、未通过项、修正记录
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**完整检查项**：

- [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
- [ ] 每步思考要点已覆盖，无遗漏
- [ ] 每步结论标注了置信度和反证可能性
- [ ] 决策树结构是否完整（决策节点、机会节点、结果节点）？
- [ ] 概率估计是否合理？概率总和是否为1？
- [ ] 期望值计算是否正确？
- [ ] 是否进行了敏感性分析？
- [ ] 是否识别了关键假设和信息价值？
- [ ] 输出具体可执行，不含模糊建议（如"综合考虑"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供概率估计和期望值计算方法 |
| [expected-value](../thinking/expected-value/SKILL.md) | 并行 | 期望值计算是决策树的核心运算 |
| [scenario-planning](../thinking/scenario-planning/SKILL.md) | 并行 | 场景规划提供多结果情景分析方法 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 贝叶斯更新根据新信息调整概率估计 |

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

1. Howard, R. A. (1966). Decision analysis: Applied decision theory. *Proceedings of the Fourth International Conference on Operational Research*, 55-71.
2. Raiffa, H. (1968). *Decision Analysis: Introductory Lectures on Choices Under Uncertainty*. Addison-Wesley.
3. Clemen, R. T., & Reilly, T. (2013). *Making Hard Decisions with DecisionTools* (3rd ed.). Cengage Learning.
4. Keeney, R. L., & Raiffa, H. (1993). *Decisions with Multiple Objectives: Preferences and Value Trade-offs*. Cambridge University Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
