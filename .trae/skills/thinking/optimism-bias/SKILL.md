---
name: optimism-bias
description: |
  触发：当需要评估是否过度乐观估计结果、需要识别"这事不会发生在我身上"偏差、需要校正风险感知时调用；常见信号包括"肯定没问题"、"我运气好"、"这次不一样"。
  不触发：当只需描述乐观态度、无需评估概率时；当乐观确实有数据支持时（经基准率验证）；当只需记录期望、无需分析偏差时。
  Invoke when needing to evaluate whether outcomes are overestimated optimistically, identify "this won't happen to me" bias, or correct risk perception.
  Do NOT invoke when only describing optimistic attitude without evaluating probability, when optimism truly has data support (verified by base rate), or when only recording expectations without analyzing bias.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["planning-fallacy", "overconfidence-effect", "availability-bias", "reference-class-forecasting"]
---

# 乐观偏差思维（Optimism Bias Thinking）

## 核心定义

人们系统性地高估好结果概率、低估坏结果概率。Sharot在2011年fMRI研究证明：大脑对正面信息更新更快，对负面信息更新更慢。这导致"我不会出事"的错觉。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充基准率数据、历史统计和反面案例
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别乐观偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别乐观信号

- 是否出现"肯定没问题"、"我运气好"、"这次不一样"等表述？
- 是否高估好结果概率？
- 是否低估坏结果概率？
- 是否认为"这事不会发生在我身上"？

---

### Step 2: 评估概率估计

- 基准率是多少？（统计数据）
- 自己的估计 vs 基准率差异？
- 是否有支持乐观的证据？（还是只是愿望）
- 反面案例有多少？（幸存者偏差）

---

### Step 3: 分析乐观机制

- 愿望思维：希望成真影响概率估计
- 控制错觉：高估自己对结果的控制
- 独特性错觉：认为自己比一般人幸运
- 信息过滤：选择性关注正面信息

---

### Step 4: 校正乐观偏差

- 基准率比较：用统计数据替代直觉
- 反面案例收集：主动寻找失败案例
- 外部视角：想象这是别人的项目
- 设计概率检查清单：愿望≠概率

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **愿望≠概率**：希望某事发生不提高其概率。原因：大脑将愿望误认为证据，导致概率估计偏离基准率。
2. **控制错觉放大**：高估自己对结果的控制力。原因：参与感产生控制错觉，使认为结果比实际更可控。
3. **独特性错觉**：认为自己比一般人幸运。原因：自我增强动机使相信自己是例外，忽视统计规律。
4. **基准率是解药**：用统计数据替代直觉估计。原因：基准率提供客观概率，纠正愿望思维导致的偏差。

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
- [ ] 是否识别了乐观信号？
- [ ] 是否评估了概率估计和基准率？
- [ ] 是否分析了乐观驱动机制？
- [ ] 是否使用基准率校正？
- [ ] 是否收集了反面案例？
- [ ] 输出具体可执行，不含模糊建议（如"保持乐观"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [planning-fallacy](../thinking/planning-fallacy/SKILL.md) | 并行 | 规划谬误是乐观偏差在时间估计的表现 |
| [overconfidence-effect](../thinking/overconfidence-effect/SKILL.md) | 并行 | 过度自信高估能力，乐观偏差高估结果 |
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差使正面案例更容易回忆 |
| [reference-class-forecasting](../thinking/reference-class-forecasting/SKILL.md) | 前置 | 参考类预测提供乐观偏差的校正方法 |

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

1. Sharot, T. (2011). The optimism bias. *Current Biology*, 21(23), R941-R945.
2. Weinstein, N. D. (1980). Unrealistic optimism about future life events. *Journal of Personality and Social Psychology*, 39(5), 806-820.
3. Tali Sharot, C. W. K., & Dolan, R. J. (2007). The neural mechanisms underlying optimistic belief updating. *Nature*, 447(7147), 1038-1041.
4. Shepperd, J. A., Klein, W. M., Waters, E. A., & Weinstein, N. D. (2013). Taking stock of unrealistic optimism. *Perspectives on Psychological Science*, 8(4), 395-411.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
