---
name: anchoring-effect
description: |
  触发：当面对数值估计、价格谈判、方案评估、时间预算或任何需要量化判断的场景时，首个信息（初始价格、上一个案例、基准值）会无形中锚定后续思考。常见信号包括首次报价、初始预期、参考数字、历史数据、最低门槛等。
  不触发：当决策不涉及数值判断时；当已有客观基准数据且无需主观估计时；当场景为纯创意发散不需要量化收敛时。
  Invoke when facing numerical estimation, price negotiation, solution evaluation, time budgeting, or any scenario where an initial value might anchor subsequent judgment.
  Do NOT invoke when decisions don't involve numerical judgment; when objective benchmark data exists and no subjective estimation is needed; when the scenario is purely creative brainstorming without quantitative convergence.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["framing-effect", "confirmation-bias", "availability-heuristic", "hindsight-bias"]
---

# 锚定效应 Anchoring Effect

## 核心定义

**锚定效应**是一种认知偏差，指人们在作出判断或决策时，会过度依赖最先获得的信息（即“锚点”），后续的思考往往围绕该锚点进行不充分的调整，即使该锚点与当前判断毫无关联或明显不合理。该效应在数值估计、价格议价、风险评估中尤为显著。

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

## 思考流程

### Step 1: 识别锚点

- 记录锚点数值、来源（谁/什么场景下提出的）
- 标注锚点是否与当前判断理性相关（如：首轮报价 vs. 成本价）

### Step 2: 启动去锚化评估

- 问自己：“如果换一个完全不同的初始值（如+50%或-50%），我的判断会变化吗？”
- 列出至少3个与锚点来源无关的独立参考源（市场数据、历史平均、专家意见）

### Step 3: 尝试临时替换锚点

- 选择其中一个参考值作为“替代锚点”
- 以该替代锚点为基础重新估算一次（不调整）
- 比较两次估算结果的差异

### Step 4: 构建中立范围

- 综合多个参考源，建立“无锚点理想范围”（最乐观到最悲观）
- 确保这个范围不是围绕原始锚点做的对称调整，而是独立推导

### Step 5: 重新做判断

- 使用该范围作为新基准，结合其他相关信息做出最终判断
- 如果最终判断落在中立范围之外，需给出强理由

### Step 6: 元认知记录

- 记录本次决策中锚点的影响力（如：初始报价 vs 最终决策的差值比例）
- 存入决策日志，供后续复盘

## 关键原则

| 原则 | 说明 | 原因 |
|------|------|------|
| **1. 先识别锚点** | 在任何数值判断前，先找出所有可能成为锚点的信息 | 未识别锚点就无从抵抗其影响 |
| **2. 独立性优先** | 寻找至少两个与原始锚点无关的独立参考源 | 单一参考源容易成为新锚点 |
| **3. 主动偏移测试** | 尝试用 ±30%~50% 的极端值做替代锚点重估 | 测试判断对锚点的敏感性 |
| **4. 多方验证** | 让不同背景的人给出独立估算，取其众数 | 个体偏差可以通过群体抵消 |
| **5. 延迟判断** | 不要在被给出锚点后立即做出最终判断 | 时间可以降低锚点的即时影响力 |

## 自检清单

> 聚焦锚定效应最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**锚定效应特有关键检查项**：

- [ ] **最早出现的数值/基准是否被明确记录？** 锚点是否被无意识接受？
- [ ] **锚点来源是否与当前决策理性相关？** 无关的初始数字是否影响了判断？
- [ ] **是否找到了至少2个独立参考源？** 这些参考源是否与原始锚点无关？
- [ ] **是否进行了替代锚点测试？** 用极端不同的值重新估算，结果是否大幅变化？
- [ ] **最终判断是否明显偏离原始锚点？** 如果偏差<20%，是否因为锚点仍然过度影响？
- [ ] **是否考虑了其他可能成为新锚点的信息？** 后续信息是否被不当地当作了新的锚？
- [ ] **团队决策中是否让成员先独立估算？** 群体讨论是否放大了锚定效应？
- [ ] **决策过程是否被记录以便复盘？** 锚点效应的影响是否可被事后追踪？

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [framing-effect](../thinking/framing-effect/SKILL.md) | 并行 | 当锚点以不同表述方式出现时（如"节省20%" vs "损失80%"），框架效应会放大锚定效应 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 后置 | 锚定后人们倾向于寻找支持该锚点的信息，确认偏差会进一步固化首因影响 |
| [availability-heuristic](../thinking/availability-heuristic/SKILL.md) | 并行 | 锚点通常来源于最近接触或最易回忆的案例（可得性），二者共同扭曲判断 |
| [hindsight-bias](../thinking/hindsight-bias/SKILL.md) | 后置 | 复盘时认为自己一开始就应该知道，容易忽略锚点的影响，导致归因错误 |

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Tversky, A., & Kahneman, D. (1974). Judgment under Uncertainty: Heuristics and Biases. *Science*, 185(4157), 1124–1131.
2. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. Chapter 10.
3. Ariely, D. (2008). *Predictably Irrational*. HarperCollins. Chapter 1.
4. Furnham, A., & Boo, H. C. (2011). A literature review of the anchoring effect. *The Journal of Socio-Economics*, 40(1), 35–42.