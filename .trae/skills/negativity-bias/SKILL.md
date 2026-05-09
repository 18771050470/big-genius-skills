---
name: negativity-bias
description: |
  触发：当需要评估是否过度关注负面信息、需要识别"一件坏事毁所有"偏差、需要校正风险感知时调用；常见信号包括"全完了"、"这一个错误毁了一切"、"太糟糕了"。
  不触发：当只需描述负面事件、无需评估整体影响时；当负面信息确实主导时（经权重分析验证）；当只需记录问题、无需分析偏差时。
  Invoke when needing to evaluate whether negative information is over-focused, identify "one bad thing ruins everything" bias, or correct risk perception.
  Do NOT invoke when only describing negative events without evaluating overall impact, when negative information truly dominates (verified by weight analysis), or when only recording problems without analyzing bias.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["loss-aversion", "availability-bias", "affect-heuristic", "peak-end-rule"]
---

# 负面偏差思维（Negativity Bias Thinking）

## 核心定义

负面信息比正面信息有更强心理影响。Baumeister等人在2001年综述证明：坏印象比好印象形成更快、更难改变；坏情绪比好情绪影响更大。进化使大脑对威胁更敏感。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充正负面信息比例、权重分配和历史恢复案例
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别负面偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别负面信号

- 是否出现"全完了"、"这一个错误毁了一切"、"太糟糕了"等表述？
- 是否过度关注负面信息？
- 是否一件坏事掩盖所有好事？
- 是否高估负面事件影响？

---

### Step 2: 评估信息权重

- 正面信息有多少？负面信息有多少？
- 负面信息权重是否过高？（通常5:1比例）
- 负面信息是否可逆/可修复？
- 整体评估是否被单一负面主导？

---

### Step 3: 分析负面机制

- 进化适应：威胁检测提高生存率
- 情绪放大：负面情绪比正面更强烈
- 记忆优先：负面事件记忆更深刻
- 社会传播：负面新闻传播更快

---

### Step 4: 校正负面偏差

- 正负面比例：计算实际正负面信息比例
- 权重调整：负面信息权重不应过高
- 恢复案例：寻找类似情况恢复案例
- 设计平衡检查清单：负面≠全部

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **负面权重过高**：一件坏事抵消多件好事。原因：进化使大脑对威胁更敏感，负面信息处理优先级更高。
2. **坏印象形成快**：负面评价比正面评价形成更快。原因：威胁检测需要快速反应，正面评价需要长期积累。
3. **情绪放大效应**：负面情绪比正面情绪更强烈持久。原因：负面情绪触发应激反应，生理反应增强记忆。
4. **比例平衡是解药**：计算实际正负面比例。原因：比例分析揭示负面信息实际权重，纠正过度关注。

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
- [ ] 是否识别了负面偏差信号？
- [ ] 是否评估了正负面信息权重？
- [ ] 是否分析了负面驱动机制？
- [ ] 是否计算了正负面比例？
- [ ] 是否寻找了恢复案例？
- [ ] 输出具体可执行，不含模糊建议（如"看开点"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 并行 | 损失厌恶使损失比收益感觉更强，负面偏差使负面比正面影响更大 |
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差使负面事件更容易回忆 |
| [affect-heuristic](../thinking/affect-heuristic/SKILL.md) | 并行 | 情感启发使负面情绪主导整体评价 |
| [peak-end-rule](../thinking/peak-end-rule/SKILL.md) | 并行 | 峰终定律使负面峰值主导整体记忆 |

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

1. Baumeister, R. F., Bratslavsky, E., Finkenauer, C., & Vohs, K. D. (2001). Bad is stronger than good. *Review of General Psychology*, 5(4), 323-370.
2. Rozin, P., & Royzman, E. B. (2001). Negativity bias, negativity dominance, and contagion. *Personality and Social Psychology Review*, 5(4), 296-320.
3. Ito, T. A., Larsen, J. T., Smith, N. K., & Cacioppo, J. T. (1998). Negative information weighs more heavily on the brain: The negativity bias in evaluative judgments. *Journal of Personality and Social Psychology*, 75(4), 887-900.
4. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
