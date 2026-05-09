---
name: information-bias
description: |
  触发：当需要评估是否过度追求信息、需要识别"更多信息一定更好"偏差、需要判断信息收集是否已足够时调用；常见信号包括"再收集点信息"、"信息越多决策越好"、"还不够了解"。
  不触发：当只需描述信息需求、无需评估收集成本时；当信息确实不足、关键数据缺失时（经决策质量验证）；当只需记录信息、无需分析收集动机时。
  Invoke when needing to evaluate whether information seeking is excessive, identify "more information is always better" bias, or judge whether information collection is sufficient.
  Do NOT invoke when only describing information needs without evaluating collection cost, when information is truly insufficient with key data missing (verified by decision quality), or when only recording information without analyzing collection motivation.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["analysis-paralysis", "confirmation-bias", "cost-benefit-analysis", "bounded-rationality"]
---

# 信息偏差思维（Information Bias Thinking）

## 核心定义

人们追求更多信息即使对决策无用。Baron等人在1988年医学诊断实验证明：医生追求额外检验即使不改变治疗方案。信息本身被视为有价值，即使不改变决策。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充信息收集成本、决策改变可能性和时间约束
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别信息偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别信息信号

- 是否出现"再收集点信息"、"信息越多决策越好"、"还不够了解"等表述？
- 是否追求信息即使不改变决策？
- 是否高估信息价值低估收集成本？
- 是否因信息不足而延迟决策？

---

### Step 2: 评估信息价值

- 信息是否改变决策？（决策敏感性）
- 信息收集成本？（时间、金钱、精力）
- 信息准确性如何？（噪声vs信号）
- 延迟决策的成本？（机会成本）

---

### Step 3: 分析信息驱动

- 控制错觉：更多信息感觉更可控
- 确定性偏好：追求100%确定性不可能
- 社会压力：展示"充分调研"避免指责
- 焦虑缓解：信息收集缓解不确定焦虑

---

### Step 4: 校正信息偏差

- 计算信息价值：信息是否改变决策？
- 设定收集上限：时间/成本预算
- 设计决策规则：何时停止收集？
- 接受不确定性：完美信息不可得

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **信息≠决策质量**：更多信息不必然提高决策质量。原因：信息收集有成本，额外信息可能不改变决策，甚至引入噪声。
2. **决策敏感性是关键**：只有改变决策的信息有价值。原因：不改变决策的信息是沉没成本，不应追求。
3. **完美信息不可得**：追求100%确定性是徒劳的。原因：世界本质不确定，追求完美信息导致决策瘫痪。
4. **设定上限是解药**：设定信息收集时间/成本预算。原因：预算约束防止过度收集，强制在有限信息下决策。

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
- [ ] 是否识别了信息偏差信号？
- [ ] 是否评估了信息价值和收集成本？
- [ ] 是否分析了信息驱动机制？
- [ ] 是否设定了收集上限？
- [ ] 是否计算了信息决策敏感性？
- [ ] 输出具体可执行，不含模糊建议（如"收集更多信息"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [analysis-paralysis](../thinking/analysis-paralysis/SKILL.md) | 并行 | 分析瘫痪使过度分析导致不决策，信息偏差使过度收集导致延迟 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误使寻找支持性信息，信息偏差使追求更多信息 |
| [cost-benefit-analysis](../thinking/cost-benefit-analysis/SKILL.md) | 前置 | 成本效益分析提供信息价值评估框架 |
| [bounded-rationality](../thinking/bounded-rationality/SKILL.md) | 并行 | 有限理性解释为何满意即可，无需完美信息 |

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

1. Baron, J., Beattie, J., & Hershey, J. C. (1988). Heuristics and biases in diagnostic reasoning: II. Congruence, information, and certainty. *Organizational Behavior and Human Decision Processes*, 42(1), 88-110.
2. Tversky, A., & Edwards, W. (1966). Information versus reward in binary choices. *Journal of Experimental Psychology*, 71(5), 680-683.
3. Hilton, D. J., & Fein, S. (1989). The role of typical diagnosticity in expectancy-based reasoning. *Journal of Personality and Social Psychology*, 57(2), 218-227.
4. Gigerenzer, G., & Goldstein, D. G. (1996). Reasoning the fast and frugal way: Models of bounded rationality. *Psychological Review*, 103(4), 650-669.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
