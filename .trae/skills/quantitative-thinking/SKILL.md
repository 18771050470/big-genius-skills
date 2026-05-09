---
name: quantitative-thinking
description: |
  触发：当面对需要做决策、评估风险、分配资源或优化方案时调用；常见信号包括模糊的判断（如"感觉很好"）、缺乏数据支撑的决策、需要对比多个选项优劣等。
  不触发：当问题为纯定性描述无法量化时；当数据完全缺失且无法合理估计时；当决策需要快速直觉判断且量化成本过高时。
  Invoke when facing decisions or evaluations that require objective measurement rather than subjective intuition, such as prioritizing features, evaluating trade-offs, or assessing performance.
  Do NOT invoke when the problem is purely qualitative and cannot be quantified; when data is completely absent and no reasonable estimation is possible; when decisions require quick intuitive judgment and quantification cost is too high.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["probabilistic-thinking", "first-principles", "cost-benefit-analysis"]
---

## 核心定义

量化思维是一种用数据和度量替代感觉与直觉的思考方式，强调将问题、选项和结果转化为可测量、可比较、可验证的数字，从而做出更客观、更可靠的决策。其根基是“能度量的才能管理”——没有数据支撑的决策本质上只是猜测。

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

## 思考流程

### Step 1: 明确决策目标与可度量指标

- 将目标分解为可测量的具体指标（KPI）。例如：“选择最佳数据库” → 指标集：查询延迟、吞吐量、维护成本、学习曲线
- 结构化指标清单（每个指标含定义、单位、数据来源）

### Step 2: 收集与生成数据

- 从基准测试、历史数据、调研、专家估算等渠道获取数据。对于缺失数据，使用保守估计或区间表示
- 原始数据表（或估算区间表）

### Step 3: 建立量化模型

- 根据决策类型选择合适的模型：
    - **对比型**：加权评分法（AHP）、成本效益分析（CBA）
    - **风险型**：决策树、蒙特卡洛模拟
    - **优化型**：线性规划、帕累托前沿
- 模型及参数（权重、假设条件）

### Step 4: 计算关键指标与不确定性

- 执行计算，输出量化结果（如总分、ROI、风险概率）。同时评估敏感性——哪些数据变化会显著改变结果
- 量化结果表（含置信区间或敏感性分析）

### Step 5: 基于数据做出决策或建议

- 用自然语言解释结果的核心含义，给出明确的推荐方案及其依据。如果结果有不确定性，说明概率范围和最可能场景
- 决策建议（含数据支撑的论点）

### Step 6: 验证与迭代

- 对比实际结果与量化预测，更新模型参数，修正偏差
- 验证报告（实际 vs 预测差异分析）及模型改进点

## 关键原则

1. **一切皆可度量** – 任何决策都至少存在一个可度量的维度。不要因为“难以度量”而放弃，可以先用代理指标（proxy metric）或相对比较。  
2. **数据优于直觉** – 当数据与直觉冲突时，优先审查数据质量；若数据可靠则修正直觉。但也要保持对数据偏差的警惕。  
3. **聚焦关键指标** – 避免“指标泛滥”，选择对目标影响最大、最敏感的少数几个指标（2-5个）。  
4. **量化比较，而非孤立** – 单个数字意义有限，将选项与基准（如历史值、行业标准、竞争对手）对比才能揭示真实优劣。  
5. **明确不确定性** – 用区间、概率分布代替点估计，避免虚假的精确感。承认“不知道”比给出错误的确信更诚实。

## 自检清单

> 聚焦量化思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**量化思维特有关键检查项**：

- [ ] **决策目标是否被转化为可度量的指标？** 模糊目标是否被拆解为具体的量化标准？
- [ ] **数据来源是否可靠？** 样本量、偏差、时效性是否被评估？
- [ ] **是否避免了度量偏差？** 幸存者偏差、确认偏差、选择偏差是否被识别和纠正？
- [ ] **不确定性是否被量化？** 置信区间、概率分布是否被明确，而非仅给出一个点估计？
- [ ] **计算结果是否与基准进行了比较？** 绝对数字是否有参照系（行业平均、历史数据、竞争对手）？
- [ ] **是否被忽略的定性因素？** 团队士气、品牌影响、用户体验等难以量化的因素是否被纳入？
- [ ] **是否存在过度拟合的风险？** 模型是否对历史数据过度优化，导致泛化能力差？
- [ ] **数据不足时假设是否被明确？** 可接受的误差范围和数据收集计划是否被记录？

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 后置 | 量化不确定性时，需要概率思维来正确理解概率和风险。 |
| [first-principles](../thinking/first-principles/SKILL.md) | 前置 | 在无法直接获得数据时，先从基本原理推演可度量参数。 |
| [cost-benefit-analysis](../thinking/cost-benefit-analysis/SKILL.md) | 并行 | 成本效益分析是量化思维在资源分配场景下的具体应用。 |
| [systems-thinking](../thinking/systems-thinking/SKILL.md) | 前置 | 量化前需要识别系统边界和关键杠杆点，避免遗漏重要变量。 |

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Kahneman, D., & Tversky, A. (1979). Prospect Theory: An Analysis of Decision under Risk. *Econometrica*, 47(2), 263-291.
2. Cialdini, R. B. (2001). The Science of Persuasion. *Scientific American*, 284(2), 76-81.
3. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux.