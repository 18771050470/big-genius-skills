---
name: process-over-outcome
description: |
  触发：当需要评估决策质量应基于过程而非结果、需要区分决策过程和结果、需要防止结果偏差时调用；常见信号包括"结果好说明决策对"、"亏了就是决策失误"、"成功了证明方法正确"。
  不触发：当只需记录结果、无需评估决策质量时；当决策过程和结果确实强相关时（经多次重复验证）；当分析确定性决策时。
  Invoke when needing to evaluate decision quality based on process rather than outcome, distinguish decision process from outcome, or prevent outcome bias.
  Do NOT invoke when only recording outcomes without evaluating decision quality, when decision process and outcomes are truly strongly correlated (verified by repeated trials), or when analyzing deterministic decisions.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["outcome-bias", "probabilistic-thinking", "bayesian-updating", "dual-process-thinking"]
---

# 过程优于结果思维（Process Over Outcome Thinking）

## 核心定义

决策质量应基于决策过程而非结果。好决策可能产生坏结果（运气差），坏决策可能产生好结果（运气好）。决策过程可控，结果受运气影响，长期结果趋近期望值。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充决策过程信息、决策时可用信息和可选方案
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别过程vs结果评估方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别结果偏差信号

- 是否出现"结果好说明决策对"、"亏了就是决策失误"、"成功了证明方法正确"等表述？
- 是否仅根据结果评估决策？
- 是否考虑了决策时的信息环境？
- 是否区分了决策质量和结果？

---

### Step 2: 重建决策过程

- 决策时有哪些信息可用？
- 决策时有哪些选项？
- 决策过程是否合理？（信息收集、分析、选择）
- 决策过程是否符合最佳实践？

---

### Step 3: 评估运气成分

- 结果中多少是决策质量，多少是运气？
- 如果重复同样决策100次，平均结果如何？
- 是否存在"黑天鹅"事件影响结果？
- 结果是否在预期范围内？

---

### Step 4: 分离过程与结果

- 使用决策质量评估框架（独立于结果）
- 比较决策过程与最佳实践
- 评估信息利用效率
- 计算决策期望值（而非实际结果）

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **过程可控，结果不可控**：决策过程可优化，结果受运气影响。原因：结果=决策质量+运气，运气不可控，过程可控。
2. **长期结果趋近期望值**：短期结果受运气影响大，长期结果趋近期望值。原因：大数定律使运气平均化，决策质量决定期望值。
3. **决策时信息是关键**：评估决策应基于决策时可用信息，而非事后信息。原因：事后信息决策者无法利用，用事后信息评估不公平。
4. **期望值优于实际结果**：决策期望值比单次实际结果更能反映决策质量。原因：期望值考虑所有可能结果和概率，实际结果只是单次抽样。

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
- [ ] 是否识别了结果偏差信号？
- [ ] 是否重建了决策过程？
- [ ] 是否评估了运气成分？
- [ ] 是否分离了决策过程和结果？
- [ ] 是否计算了决策期望值？
- [ ] 输出具体可执行，不含模糊建议（如"看过程不看结果"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [outcome-bias](../thinking/outcome-bias/SKILL.md) | 并行 | 结果偏差用结果评价决策，过程优于结果提供评估框架 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供期望值计算框架 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 贝叶斯更新根据新结果校准决策模型 |
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 前置 | 双系统理论解释直觉vs理性决策过程 |

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

1. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 17: Regression to the Mean)
2. Mauboussin, M. J. (2012). *The Success Equation: Untangling Skill and Luck in Business, Sports, and Investing*. Harvard Business Review Press.
3. Duke, A. (2018). *Thinking in Bets: Making Smarter Decisions When You Don't Have All the Facts*. Portfolio.
4. Gino, F., Moore, D. A., & Schweitzer, M. E. (2009). Success, failure, and attention: The outcome bias in decision making. *Organizational Behavior and Human Decision Processes*, 108(1), 138-149.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
