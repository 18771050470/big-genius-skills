---
name: pessimism-bias
description: |
  触发：当需要评估是否过度悲观估计结果、需要识别"一切都会变糟"偏差、需要校正风险感知时调用；常见信号包括"肯定不行"、"太悲观了"、"迟早会出事"。
  不触发：当只需描述悲观态度、无需评估概率时；当悲观确实有数据支持时（经基准率验证）；当只需记录担忧、无需分析偏差时。
  Invoke when needing to evaluate whether outcomes are overestimated pessimistically, identify "everything will go wrong" bias, or correct risk perception.
  Do NOT invoke when only describing pessimistic attitude without evaluating probability, when pessimism truly has data support (verified by base rate), or when only recording worries without analyzing bias.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["negativity-bias", "loss-aversion", "availability-bias", "catastrophizing"]
---

# 悲观偏差思维（Pessimism Bias Thinking）

## 核心定义

人们系统性地高估坏结果概率、低估好结果概率。Beck在1976年抑郁症认知模型证明：抑郁倾向者对未来事件概率估计系统偏向负面。这导致"一切都会变糟"的错觉。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充基准率数据、历史统计和正面案例
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别悲观偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别悲观信号

- 是否出现"肯定不行"、"太悲观了"、"迟早会出事"等表述？
- 是否高估坏结果概率？
- 是否低估好结果概率？
- 是否将最坏情况视为最可能？

---

### Step 2: 评估概率估计

- 基准率是多少？（统计数据）
- 自己的估计 vs 基准率差异？
- 是否有支持悲观的证据？（还是只是恐惧）
- 正面案例有多少？（忽视成功）

---

### Step 3: 分析悲观机制

- 恐惧思维：害怕成真影响概率估计
- 负面可得性：负面案例更容易回忆
- 控制缺失感：低估自己对结果的影响
- 灾难化：将小风险放大为确定性

---

### Step 4: 校正悲观偏差

- 基准率比较：用统计数据替代直觉
- 正面案例收集：主动寻找成功案例
- 控制感评估：识别自己可影响的因素
- 设计概率检查清单：恐惧≠概率

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **恐惧≠概率**：害怕某事发生不提高其概率。原因：大脑将恐惧误认为证据，导致概率估计偏离基准率。
2. **负面可得性放大**：负面案例更容易回忆和想象。原因：媒体偏好报道负面事件，使负面案例在记忆中更突出。
3. **灾难化扭曲**：将小风险放大为确定性。原因：焦虑触发灾难化思维，使概率估计极端化。
4. **基准率是解药**：用统计数据替代直觉估计。原因：基准率提供客观概率，纠正恐惧思维导致的偏差。

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
- [ ] 是否识别了悲观信号？
- [ ] 是否评估了概率估计和基准率？
- [ ] 是否分析了悲观驱动机制？
- [ ] 是否使用基准率校正？
- [ ] 是否收集了正面案例？
- [ ] 输出具体可执行，不含模糊建议（如"别太悲观"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [negativity-bias](../thinking/negativity-bias/SKILL.md) | 并行 | 负面偏差使负面信息影响更大，悲观偏差使负面结果概率被高估 |
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 并行 | 损失厌恶使损失感觉比收益强，悲观偏差使损失概率被高估 |
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差使负面案例更容易回忆 |
| [catastrophizing](../thinking/catastrophizing/SKILL.md) | 前置 | 灾难化思维是悲观偏差的极端表现 |

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

1. Beck, A. T. (1976). *Cognitive Therapy and the Emotional Disorders*. International Universities Press.
2. Alloy, L. B., & Ahrens, A. H. (1987). Depression and pessimism for the future: Biased use of statistically relevant information in predictions for self and others. *Journal of Personality and Social Psychology*, 52(2), 366-378.
3. Seligman, M. E. P. (1975). *Helplessness: On Depression, Development, and Death*. W.H. Freeman.
4. Nolen-Hoeksema, S. (2000). The role of rumination in depressive disorders and mixed anxiety/depressive symptoms. *Journal of Abnormal Psychology*, 109(3), 504-511.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
