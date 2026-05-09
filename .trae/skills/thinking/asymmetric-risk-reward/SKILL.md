---
name: asymmetric-risk-reward
description: |
  触发：当需要评估决策的潜在收益与损失不对称性、设计"下行有限、上行无限"的策略、或在不确定性下优化资源配置时调用；常见信号包括投资组合构建、职业转型决策、技术选型风险评估、创业方向选择、杠铃策略实施。
  不触发：当决策的收益和损失完全对称且概率已知时（应使用概率思维或期望价值计算）；当仅需最小化风险而不考虑收益时（应使用风险规避框架）；当所有选项的风险收益特征相似时。
  Invoke when: evaluating the asymmetry between potential gains and losses, designing strategies with limited downside and unlimited upside, or optimizing resource allocation under uncertainty; common signals include portfolio construction, career transition decisions, technology selection risk assessment, startup direction choice, barbell strategy implementation.
  Do NOT invoke when: gains and losses are perfectly symmetric with known probabilities (use probabilistic-thinking); when merely minimizing risk without considering upside (use risk-aversion framework); when all options have similar risk-reward profiles.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["antifragility", "probabilistic-thinking", "optionality-thinking", "barbell-strategy", "skin-in-the-game"]
---

# 不对称风险收益思维（Asymmetric Risk/Reward）

## 核心定义

主动寻找和构建"下行损失有限、上行收益无限"的决策结构，避免"下行无限、上行有限"的陷阱——财富积累的本质是持续获取正凸性敞口。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 绘制收益函数曲线

- 将每个选项的收益/损失表示为结果变量的函数
- 识别曲线的凸性（∪形，波动受益）与凹性（∩形，波动受损）
- 标注最大可能损失（下限）和最大可能收益（上限）
- 检查是否存在"尾部风险"：小概率事件是否会导致毁灭性后果

---

### Step 2: 量化不对称比率

- 计算每个选项的"上行潜力 / 下行风险"比率
- 比率 > 3:1 视为具有吸引力的不对称性
- 比率 < 1:1 视为危险的不对称性（下行大于上行）
- 区分"概率加权期望值"与"实际可承受损失"：即使期望值为正，单次毁灭性损失也可能不可接受

---

### Step 3: 评估非遍历性风险

- 问自己：这个决策是"一次性"的还是"重复进行"的？
- 非遍历性陷阱：对群体有利的策略，对个体可能是毁灭性的
- 如果存在"吸收态壁垒"（一旦触及即永久退出），必须优先确保不触及该壁垒
- 参考凯利公式：即使期望值为正，过度下注仍可能导致破产

---

### Step 4: 设计凸性结构

- 寻找或创造具有期权特征的敞口：损失有上限，收益无上限
- 实践方法：购买深度虚值期权、参与早期风险投资、保持职业选择的灵活性
- 避免"负凸性"敞口：如卖出裸期权、高杠杆负债、不可逆的单一技能依赖
- 验证结构的实际凸性：在极端情景下是否真的能保护下行？

---

### Step 5: 实施杠铃配置

- 将资源分配到两个极端：极度安全 + 极度冒险
- 安全端（85-90%）：确保生存和底线，抵御毁灭性风险
- 冒险端（10-15%）：承担可控的小损失，换取巨大潜在收益
- 彻底避开中等风险区域：这是最容易被黑天鹅击穿的脆弱地带
- 定期再平衡：当冒险端收益巨大时，将部分收益转移到安全端

---

### Step 6: 建立动态退出机制

- 为每个冒险头寸预设止损点和止盈点
- 止损点应基于"可承受损失"而非"成本价"
- 止盈点应允许"让利润奔跑"，不提前限制上行空间
- 建立"部分退出"机制：在收益达到特定阈值时回收本金，让利润继续冒险

---

### Step 7: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **赔率优于胜率**：决策质量取决于"对的时候赚多少 / 错的时候亏多少"，而非"对的频率"。原因：一个30%胜率但盈利时赚10倍、亏损时只亏1倍的策略，长期远优于70%胜率但盈亏相等的策略。
2. **生存优先于期望**：即使期望值为正，如果存在毁灭性尾部风险，该决策也不应采纳。原因：非遍历性意味着个体只有一条命，群体层面的正期望值对个体毫无意义（吸收态壁垒）。
3. **凸性即自由**：拥有正凸性敞口（收益加速增长、损失减速增长）的系统在波动中自动受益。原因：根据詹森不等式，凸函数在波动环境下的期望收益恒大于静态环境。
4. **减法创造不对称**：通过消除下行风险（如债务、不可逆承诺）而非增加上行潜力来构建不对称性。原因：下行风险往往来自已有的脆弱性结构，减法比加法更可靠。
5. **时间放大不对称**：持续的小额正不对称性决策，长期会产生指数级回报（复利效应）。原因：单次大赢可以覆盖多次小亏，而持续的小额正期望值在重复博弈中必然累积。

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
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）
- [ ] **不对称特供**：是否正确绘制了收益函数曲线，识别了凸性/凹性特征
- [ ] **不对称特供**：是否计算了具体的不对称比率（上行/下行），而非仅定性描述
- [ ] **不对称特供**：是否评估了非遍历性风险（吸收态壁垒、毁灭性尾部风险）
- [ ] **不对称特供**：是否设计了具体的杠铃配置比例和再平衡机制

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [antifragility](../antifragility/SKILL.md) | 前置/互补 | 反脆弱系统天然具备正凸性，是不对称风险收益的理想载体 |
| [probabilistic-thinking](../probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供先验概率估计，为不对称性计算提供输入 |
| [optionality-thinking](../optionality-thinking/SKILL.md) | 并行 | 可选性是不对称结构的核心机制，提供"权利而非义务" |
| [barbell-strategy](../barbell-strategy/SKILL.md) | 后置 | 杠铃策略是不对称风险收益的具体实施框架 |
| [skin-in-the-game](../skin-in-the-game/SKILL.md) | 并行 | 确保决策者自身承担不对称后果，避免将下行风险转嫁给他人 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | 思维模型的理论背景（塔勒布、凯利公式等） |

---

## 参考文献

1. Taleb, N. N. (2012). *Antifragile: Things That Gain from Disorder*. Random House.
2. Taleb, N. N. (2018). *Skin in the Game: Hidden Asymmetries in Daily Life*. Random House.
3. Kelly, J. L. (1956). "A New Interpretation of Information Rate." *Bell System Technical Journal*, 35(4), 917-926.
4. Thorp, E. O. (2006). *The Kelly Capital Growth Investment Criterion*. World Scientific.
5. Peters, O., & Gell-Mann, M. (2016). "Evaluating gambles using dynamics." *Chaos: An Interdisciplinary Journal of Nonlinear Science*, 26(2), 023103.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
