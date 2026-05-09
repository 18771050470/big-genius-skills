```yaml
---
name: circle-of-competence
description: |
  触发：当需要评估任务是否超出自身或团队能力范围时，接到陌生领域请求时，或面对决策不确定性时。
  不触发：当日常例行任务（如运维、代码review）且已经形成成熟SOP时；当紧急事件中需要直觉式快速决策时（应调用其他模型如"紧急思维"）。
  Invoke when assessing task feasibility within known expertise, evaluating whether to accept a project, or deciding on collaboration.
  Do NOT invoke when dealing with routine tasks with established SOPs, or when emergency quick decisions are needed.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["first-principles", "margin-of-safety", "second-curve"]
---
```

## 核心定义

清晰地界定自己或团队擅长的领域边界，在边界内深耕并自主决策，在边界外保持谨慎并主动寻求外部支持。

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

### Step 1: 任务范围拆解

- 将整体任务拆解为粒度适中的子问题
- 明确每个子问题所需的知识域（如：算法、前端、后端、安全、合规）
- 标注子问题之间的依赖关系
- 识别关键路径和瓶颈子问题

---

### Step 2: 能力边界扫描

- 对照自身或团队的历史项目、公开评价、认证资质
- 逐一判断"能否在无外部帮助下高质量完成"
- 区分"我有经验"和"我听说过"
- 标记圈内/圈外，附理由和置信度

---

### Step 3: 圈内自主策略

- 对圈内子问题直接输出自主决策方案
- 设计实现路径和排期
- 评估工时和资源需求
- 识别圈内任务的潜在风险

---

### Step 4: 圈外求助策略

- 列出具体缺失的知识点
- 识别可求助渠道：专家咨询、文献、培训、外包
- 评估求助成本和风险
- 制定备选方案（如第一渠道失效）

---

### Step 5: 整体决策与复核

- 整合所有子问题的策略为最终行动方案
- 交叉检查是否有误判（圈内标为圈外，或相反）
- 考虑团队成员中其他人可能拥有的能力
- 评估是否在风险和机会之间取得合理平衡

---

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

> 使用此思维模型时必须遵守的原则。3-5 条。每条包含"原则 + 原因/后果"。

1. **诚实认知边界**：高估能力是决策失败的主要原因。原因：诚实面对"不知道"比假装知道更能降低风险。
2. **圈内深耕**：把有限精力集中在能力圈内的任务上。原因：能持续积累专业优势，提升自主决策质量。
3. **圈外谨慎**：不熟悉的领域犯错概率极高。原因：主动求助或合作比冒险独立尝试更安全。
4. **动态扩展**：能力圈是动态的，应有计划地扩展。原因：通过学习和实践将圈外任务转化为圈内任务，而非固步自封。

---

## 自检清单

> 聚焦能力圈思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**能力圈思维特有关键检查项**：

- [ ] **能力圈特供**：是否诚实区分了"我有经验"和"我听说过"？能力边界是否被高估？是否使用了具体的项目案例来验证能力声明？
- [ ] **能力圈特供**：子问题拆解是否足够细致？粗粒度评估是否掩盖了局部的能力盲区？是否对每个子问题标注了置信度？
- [ ] **能力圈特供**：圈内任务是否识别了潜在风险？"在能力圈内"不等于"零风险"，是否评估了执行风险和外部依赖？
- [ ] **能力圈特供**：圈外求助策略是否具体可行？求助渠道、成本和备选方案是否被明确？是否评估了求助的时间成本和质量风险？
- [ ] **能力圈特供**：是否考虑了团队成员的能力互补？个人圈外是否可能是他人的圈内？是否建立了能力共享机制？
- [ ] **能力圈特供**：能力圈是否被动态评估？当前圈外任务是否可以通过学习转化为圈内？是否制定了有计划的能力扩展路径？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [opportunity-cost](../thinking/opportunity-cost/SKILL.md) | 前置 | 在决定是否扩展能力圈时，评估学习新领域的时间机会成本 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 随着经验积累，持续更新对自己能力边界的置信度评估 |
| [dunning-kruger-effect](../thinking/dunning-kruger-effect/SKILL.md) | 防范 | 能力圈思维天然对抗达克效应，防止无知者无畏 |
| [first-principles](../thinking/first-principles/SKILL.md) | 后置 | 当进入全新领域时，用第一性原理快速建立基础理解 |

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

1. Buffett, W. (1996). *The Essays of Warren Buffett: Lessons for Corporate America*. Cunningham, L. A. (Ed.).
2. Munger, C. T. (1994). *A Lesson on Elementary, Worldly Wisdom*. USC Business School Speech.
3. Kahneman, D., & Klein, G. (2009). Conditions for intuitive expertise: A failure to disagree. *American Psychologist*, 64(6), 515-526.
4. Ericsson, K. A., Krampe, R. T., & Tesch-Römer, C. (1993). The role of deliberate practice in the acquisition of expert performance. *Psychological Review*, 100(3), 363-406.
