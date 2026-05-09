---
name: cost-benefit-analysis
description: |
  触发：当需要评估选项的成本效益比、需要比较不同资源分配方案、需要识别低效投入时调用；常见信号包括"这个值得吗"、"投入产出比如何"、"花这么多钱值不值"。
  不触发：当只需定性描述选项、无需量化比较时；当成本效益数据完全不可得时；当只需记录事实、无需评估效率时。
  Invoke when needing to evaluate cost-benefit ratio of options, compare different resource allocation plans, or identify inefficient investments.
  Do NOT invoke when only qualitatively describing options without quantitative comparison, when cost-benefit data is completely unavailable, or when only recording facts without evaluating efficiency.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["opportunity-cost", "zero-risk-bias", "scope-neglect", "identifiable-victim-effect"]
---

# 成本效益分析思维（Cost-Benefit Analysis Thinking）

## 核心定义

系统比较选项的成本和效益，选择净效益（效益-成本）最大的方案。通过量化所有相关成本和效益，包括直接/间接、短期/长期、有形/无形，实现资源最优配置。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充成本数据、效益预期和时间范围
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别最优方案且分析清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 定义分析范围

- 分析的目标是什么？
- 时间范围？（短期/长期）
- 包含哪些成本和效益？（直接/间接）
- 利益相关方有哪些？

---

### Step 2: 量化成本

- 直接成本：资金、时间、人力
- 间接成本：机会成本、风险成本、转换成本
- 沉没成本：已发生不可回收（应忽略）
- 边际成本：每增加一单位的额外成本

---

### Step 3: 量化效益

- 直接效益：收入增加、成本节约
- 间接效益：品牌提升、风险降低、能力积累
- 无形效益：员工满意度、客户忠诚度
- 边际效益：每增加一单位的额外效益

---

### Step 4: 计算与比较

- 净效益 = 总效益 - 总成本
- 效益成本比 = 总效益 / 总成本
- 投资回收期 = 成本 / 年效益
- 净现值（NPV）：考虑时间价值

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **净效益最大化**：选择净效益最大的方案，而非效益最大或成本最小。原因：高效益可能伴随更高成本，净效益才是真实价值。
2. **忽略沉没成本**：已发生不可回收成本不应影响决策。原因：沉没成本无法改变，决策应基于未来成本和效益。
3. **考虑机会成本**：资源用于A就不能用于B，B的收益是A的机会成本。原因：机会成本是真实成本，忽视导致资源错配。
4. **时间价值重要**：未来效益不如当前效益有价值。原因：资金有时间价值，风险随时间增加，净现值计算考虑时间因素。

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
- [ ] **成本效益特供**：是否定义了分析范围和时间范围？分析目标、利益相关方、时间跨度是否被明确？
- [ ] **成本效益特供**：是否量化了所有相关成本？直接成本、间接成本、机会成本、沉没成本（应忽略）是否被完整识别？
- [ ] **成本效益特供**：是否量化了所有相关效益？直接效益、间接效益、无形效益、边际效益是否被完整识别？
- [ ] **成本效益特供**：是否计算了净效益和效益成本比？净效益=总效益-总成本、BCR=总效益/总成本、NPV是否被计算？
- [ ] **成本效益特供**：是否考虑了时间价值（净现值）？未来效益是否被贴现？贴现率是否合理？投资回收期是否被计算？
- [ ] 输出具体可执行，不含模糊建议（如"分析成本效益"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [opportunity-cost](../thinking/opportunity-cost/SKILL.md) | 前置 | 机会成本是成本效益分析的重要组成部分 |
| [zero-risk-bias](../thinking/zero-risk-bias/SKILL.md) | 并行 | 零风险偏差使人们为消除小风险支付过多，成本效益分析校正 |
| [scope-neglect](../thinking/scope-neglect/SKILL.md) | 并行 | 范围忽视使规模不敏感，成本效益分析量化规模影响 |
| [identifiable-victim-effect](../thinking/identifiable-victim-effect/SKILL.md) | 并行 | 可识别受害者效应使具体个体胜过统计群体，成本效益分析客观比较 |

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

1. Boardman, A. E., Greenberg, D. H., Vining, A. R., & Weimer, D. L. (2018). *Cost-Benefit Analysis: Concepts and Practice* (5th ed.). Cambridge University Press.
2. Sunstein, C. R. (2002). Risk and reason: Safety, law, and the environment. *Cambridge University Press*.
3. Hufschmidt, K. H. (2008). *Cost-Benefit Analysis: A Practical Guide*. McGraw-Hill.
4. Pearce, D. W. (1996). *Cost-Benefit Analysis: Theory and Practice*. Macmillan.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
