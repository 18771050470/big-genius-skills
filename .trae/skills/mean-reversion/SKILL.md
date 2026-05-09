---
name: mean-reversion
description: |
  触发：当评估极端表现是否会持续、需要判断趋势是否可持续、需要识别短期异常与长期规律时调用；常见信号包括"涨太多了该跌了""这次不一样""业绩会回归正常""极端表现能否持续"。
  不触发：当结构性变化已发生且不可逆时；当存在明确的持续驱动因素时；当评估的是一次性事件而非序列数据时。
  Invoke when evaluating whether extreme performance will persist, judging trend sustainability, or distinguishing short-term anomalies from long-term patterns.
  Do NOT invoke when structural changes have occurred and are irreversible, when clear persistent drivers exist, or when evaluating one-time events rather than sequential data.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["regression-to-the-mean", "base-rate-fallacy", "probabilistic-thinking", "bayesian-updating"]
---

# 均值回归思维（Mean Reversion Thinking）

## 核心定义

极端表现终将回归长期平均水平。Francis Galton在19世纪研究遗传时发现：父母身高极端偏离均值时，子女身高会向均值"回归"。DeBondt和Thaler在1985年证明股市也存在均值回归：过去赢家未来跑输，过去输家未来跑赢。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充历史数据、时间窗口和潜在结构性变化信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确判断是均值回归还是结构性变化，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别极端偏离

- 当前表现与历史均值偏离多少？（标准差倍数）
- 偏离持续了多长时间？
- 偏离方向：正向极端（过高）还是负向极端（过低）？
- 标注偏离的测量方法和时间窗口

### Step 2: 评估历史回归模式

- 历史上类似偏离后是否回归？回归速度如何？
- 回归的半衰期是多少？（50%回归所需时间）
- 是否存在"超调"现象？（回归时越过均值到另一端）
- 统计检验：回归的显著性和置信度

### Step 3: 区分结构性变化与暂时偏离

- 是否有根本性变化改变了均值本身？（技术革命、监管变化、竞争格局）
- 驱动极端表现的因素是否可持续？
- 均值本身是否在移动？（非平稳过程）
- 标注"这次不一样"的论据和反论据

### Step 4: 预测回归路径

- 预期回归时间：多久回到均值？
- 回归方式：渐进式还是突变式？
- 回归后的稳定状态：回到原均值还是新均值？
- 置信区间：预测的不确定性范围

### Step 5: 设计应对策略

- 如果预期回归：如何利用回归获利或规避风险？
- 如果是结构性变化：如何调整长期预期？
- 对冲策略：同时准备回归和结构变化两种情景
- 监控指标：哪些信号表明判断错误？

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **均值回归≠必然回归**：统计规律不是物理定律，极端可能更极端（黑天鹅）。原因：均值回归是概率性趋势，不是确定性保证，尾部风险始终存在。
2. **均值本身会移动**：技术革命、政策变化可能永久改变均值。原因：将移动均值误判为固定均值会导致回归预测完全错误。
3. **回归速度不可预测**：知道会回归不等于知道何时回归。原因：市场可以在"错误"方向持续很长时间，早一步等于错。
4. **回归是机会也是陷阱**：逆向投资者利用回归获利，但可能接飞刀。原因：区分"暂时偏离"和"永久性损失"是均值回归应用的核心挑战。

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
- [ ] 偏离是否被量化？（标准差倍数、百分位数）
- [ ] 历史回归模式是否被评估？回归半衰期是否被估计？
- [ ] 是否区分了结构性变化与暂时偏离？
- [ ] "这次不一样"的论据和反论据是否都被考虑？
- [ ] 回归路径预测是否有置信区间？
- [ ] 是否设计了回归和结构变化两种情景的应对策略？
- [ ] 输出具体可执行，不含模糊建议（如"等待回归"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [regression-to-the-mean](../regression-to-the-mean/SKILL.md) | 并行 | 统计上的回归均值概念，均值回归思维将其应用于决策 |
| [base-rate-fallacy](../base-rate-fallacy/SKILL.md) | 前置 | 基础比率谬误忽视基准率，均值回归思维利用基准率做预测 |
| [probabilistic-thinking](../probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供量化框架，均值回归思维提供具体预测模式 |
| [bayesian-updating](../bayesian-updating/SKILL.md) | 后置 | 均值回归做出先验预测，贝叶斯更新根据新证据调整 |

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

1. Galton, F. (1886). Regression towards mediocrity in hereditary stature. *The Journal of the Anthropological Institute of Great Britain and Ireland*, 15, 246-263.
2. De Bondt, W. F. M., & Thaler, R. H. (1985). Does the stock market overreact? *The Journal of Finance*, 40(3), 793-805.
3. De Bondt, W. F. M., & Thaler, R. H. (1987). Further evidence on investor overreaction and stock market seasonality. *The Journal of Finance*, 42(3), 557-581.
4. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 17: Regression to the Mean)

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
