---
name: scale-thinking
description: |
  触发：当面对系统规模变化、数据量级提升、组织扩张或产品从0到1到N时调用；常见信号包括线性推断失效、系统行为突变、资源消耗非线性增长。
  不触发：当系统规模稳定且无增长预期时；当问题为小规模且规模变化不影响系统行为时；当只需优化现有规模下的性能无需考虑扩展时。
  Invoke when facing changes in system scale, data volume, organizational growth, or product scaling from 0 to 1 to N.
  Do NOT invoke when system scale is stable with no growth expectation; when the problem is small-scale and scale changes don't affect system behavior; when only optimizing performance at current scale without considering expansion.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["systems-thinking", "compound-effect", "leverage-thinking", "exponential-thinking"]
---

# 规模思维 (Scale Thinking)

## 核心定义

理解量变如何引起质变，不同规模下规律可能完全不同（微观规律≠宏观规律），避免线性外推。  
**一句话**：规模改变时，系统的行为、约束和最优策略可能发生根本性变化，必须重新审视而非简单放大。

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

## 思考流程

### Step 1: 定位规模维度与当前量级

- 列出所有可能影响系统行为的规模维度；标明每个维度的当前数值和预期增长倍数
- 规模维度和当前量级表

### Step 2: 识别支配规律与相变点

- 对每个维度分析其核心约束（如cpu、内存、网络、人工协调等）；寻找已知的相变阈值（如数据库分表阈值、组织扁平化边界、并发连接数上限）
- 每个维度的支配规律清单与潜在相变点

### Step 3: 检验线性外推假设

- 假设按当前模式放大 n 倍，预测各项指标；与实际物理规律（如阿姆达尔定律、梅特卡夫定律、帕金森定律）对比，识别非线性增长区域
- 线性外推偏差报告（哪些假设可能失效）

### Step 4: 应用规模缩放法则

- 针对每个非线性区域，选择适用的缩放法则或经验公式（如乘法扩展→加法扩展、平方增长→线性增长、指数增长→对数增长）
- 缩放法则映射表

### Step 5: 设计分阶段策略

- 根据当前规模和预期增长曲线，制定 3~5 个阶段的扩展策略；每个阶段明确架构变更、资源投入、组织调整
- 分阶段路线图（含关键里程碑）

### Step 6: 权衡过早优化与过度滞后

- 评估每个阶段引入的复杂度是否与规模匹配；避免在小规模阶段采用大规模方案（过早优化），也避免在大规模前夕仍未准备（滞后危机）
- 复杂度-规模适配矩阵

### Step 7: 持续监测与反馈调整

- 建立关键规模指标监控（如每日活跃用户、请求响应时间、团队沟通成本）；设置预警阈值，触发时重新执行整个流程
- 监控仪表盘设计 + 回滚策略

## 关键原则

| 原则 | 说明 | 原因 |
|------|------|------|
| **非线性原则** | 规模变化时，输出与输入不成比例，常见平方、对数、S型等关系 | 避免线性外推导致决策失误 |
| **相变原则** | 量变可能引发质变，系统在不同规模下遵循完全不同规律（如微观物理≠宏观众多体） | 必须在接近相变点前切换范式 |
| **尺度匹配原则** | 解决方案的复杂度应与问题规模匹配，既不过度也不过低 | 以最小成本满足当前与可预见的未来规模 |
| **不可外推原则** | 小规模规律不能直接推广到大规模，必须通过实验或理论验证 | 边界条件随量级改变 |
| **早期预判原则** | 在系统早期就规划可扩展性，但避免过早实现 | 预判为后续阶段预留空间，但实施只在必要时 |

## 自检清单

> 聚焦规模思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**规模思维特有关键检查项**：

- [ ] **关键规模维度是否被明确？** 用户、数据、组件、团队等维度中哪个是瓶颈？
- [ ] **是否识别了至少一个相变点（阈值）？** 量变引发质变的临界点是否被定位？
- [ ] **线性外推假设是否被验证？** 性能、成本、沟通成本随规模增长是否真的是线性的？
- [ ] **非线性影响是否被考虑？** O(N²)复杂度、平方增长、对数增长等是否被纳入分析？
- [ ] **是否为不同规模阶段设计了差异化策略？** 一成不变的方法是否被避免？
- [ ] **正负规模效应是否被平衡？** 梅特卡夫定律、学习曲线 vs 官僚化、耦合加剧？
- [ ] **是否平衡了扩展性与当前复杂度？** 过早优化和太迟扩展哪个陷阱更危险？
- [ ] **规模指标的监控和预警机制是否建立？** 增长是否可被实时追踪和预警？

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [systems-thinking](../thinking/systems-thinking/SKILL.md) | 并行 | 分析规模变化对系统各组件交互的影响，识别涌现行为 |
| [compound-effect](../thinking/compound-effect/SKILL.md) | 并行 | 规模增长带来的正反馈累积效应（如用户增长→网络效应） |
| [leverage-thinking](../thinking/leverage-thinking/SKILL.md) | 并行 | 找出在特定规模阶段投入产出比最高的杠杆点（如自动化、复用） |
| [exponential-thinking](../thinking/exponential-thinking/SKILL.md) | 前置 | 识别规模是否以指数增长，预判非线性拐点 |

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. West, G. B. (2017). *Scale: The Universal Laws of Growth, Life, Death, and Complexity in Living Systems*. Weidenfeld & Nicolson.
2. Anderson, P. W. (1972). More is Different. *Science*, 177(4047), 393-396.
3. Taleb, N. N. (2012). *Antifragile: Things That Gain from Disorder*. Random House. Chapter 3.
4. Meadows, D. H. (2008). *Thinking in Systems: A Primer*. Chelsea Green Publishing.
```