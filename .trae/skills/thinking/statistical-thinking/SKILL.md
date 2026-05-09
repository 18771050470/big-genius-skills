---
name: statistical-thinking
description: |
  触发：当需要从数据中提取洞察、需要识别统计显著性vs实际意义、需要避免统计误用时调用；常见信号包括"数据表明"、"统计显示"、"相关性证明"、"p值小于0.05"。
  不触发：当只需描述数据、无需统计推断时；当样本量太小、统计方法不适用时；当只需定性观察、无需量化分析时。
  Invoke when needing to extract insights from data, identify statistical significance vs practical significance, or avoid statistical misuse.
  Do NOT invoke when only describing data without statistical inference, when sample size is too small for statistical methods, or when only qualitative observation is needed without quantitative analysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["probabilistic-thinking", "regression-to-mean", "base-rate-fallacy", "decision-tree"]
---

# 统计思维（Statistical Thinking）

## 核心定义

用统计原理理解数据变异、区分信号与噪声、避免统计误用。Fisher在1925年建立现代统计基础：统计思维关注变异来源、抽样误差、因果推断，而非简单数字计算。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充样本量、数据分布和收集方法
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别统计结论且分析清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 评估数据质量

- 数据来源是什么？（抽样、实验、观察）
- 样本量是否足够？（统计功效）
- 样本是否代表总体？（抽样偏差）
- 数据收集方法是否有偏差？

---

### Step 2: 分析变异来源

- 总变异分解：组间变异 vs 组内变异
- 信号 vs 噪声：观察到的差异是真实效应还是随机波动？
- 混杂因素：是否有其他变量影响结果？
- 异常值：是否影响结论？

---

### Step 3: 评估统计显著性

- p值含义：在零假设下观察到当前结果的概率
- 效应量：差异的实际大小（不仅是统计显著）
- 置信区间：估计的不确定性范围
- 统计功效：检测到真实效应的概率

---

### Step 4: 区分统计vs实际意义

- 统计显著≠实际重要：小效应可能统计显著（大样本）
- 实际意义：效应量是否足够大以影响决策？
- 成本效益：改变的成本是否小于收益？
- 可重复性：结果是否在其他研究中复现？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **变异无处不在**：所有数据都有变异，区分信号与噪声是关键。原因：随机波动产生假模式，统计思维帮助识别真实效应。
2. **显著≠重要**：统计显著只说明效应不太可能是偶然，不说明效应大小。原因：大样本使小效应统计显著，但小效应可能无实际价值。
3. **相关≠因果**：相关性不证明因果关系，可能有混杂因素。原因：第三变量可能同时影响两个变量，产生虚假相关。
4. **效应量优于p值**：效应量提供实际意义，p值只提供统计显著性。原因：决策需要知道"有多大"，而非"是否非零"。

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
- [ ] 是否评估了数据质量和样本代表性？
- [ ] 是否分析了变异来源（信号vs噪声）？
- [ ] 是否评估了统计显著性和效应量？
- [ ] 是否区分了统计显著vs实际意义？
- [ ] 是否考虑了混杂因素和因果推断？
- [ ] 输出具体可执行，不含模糊建议（如"数据表明"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供不确定性量化框架 |
| [regression-to-mean](../thinking/regression-to-mean/SKILL.md) | 并行 | 回归均值解释极端值趋向平均 |
| [base-rate-fallacy](../thinking/base-rate-fallacy/SKILL.md) | 并行 | 基础概率谬误解释忽视先验概率 |
| [decision-tree](../thinking/decision-tree/SKILL.md) | 并行 | 决策树提供多阶段决策分析框架 |

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

1. Fisher, R. A. (1925). *Statistical Methods for Research Workers*. Oliver and Boyd.
2. Gelman, A., Hill, J., & Vehtari, A. (2020). *Regression and Other Stories*. Cambridge University Press.
3. Cohen, J. (1994). The earth is round (p < .05). *American Psychologist*, 49(12), 997-1003.
4. Wasserstein, R. L., & Lazar, N. A. (2016). The ASA statement on p-values: Context, process, and purpose. *The American Statistician*, 70(2), 129-133.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
