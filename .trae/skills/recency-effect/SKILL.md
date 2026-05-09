---
name: recency-effect
description: |
  触发：当需要评估判断是否受最近信息过度影响、需要识别"最新的就是最重要的"偏差、需要校正时间权重时调用；常见信号包括"最近表现不好"、"刚出的消息"、"最新趋势"。
  不触发：当只需描述时间序列、无需评估权重偏差时；当最近信息确实更重要时（经时效性验证）；当只需记录事件、无需分析偏差时。
  Invoke when needing to evaluate whether judgments are over-affected by recent information, identify "latest is most important" bias, or correct time weighting.
  Do NOT invoke when only describing time series without evaluating weight bias, when recent information truly is more important (verified by timeliness), or when only recording events without analyzing bias.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["primacy-effect", "availability-bias", "peak-end-rule", "anchoring-effect"]
---

# 近因效应思维（Recency Effect Thinking）

## 核心定义

人们过度重视最近发生的信息。Murdock在1962年系列位置实验证明：列表末尾项目回忆率最高。最近信息更容易回忆，被误认为更重要。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充历史数据、时间序列完整信息和长期趋势
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别近因效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别近因信号

- 是否出现"最近表现不好"、"刚出的消息"、"最新趋势"等表述？
- 是否过度重视最近信息？
- 是否忽视历史数据？
- 是否将近期趋势外推长期？

---

### Step 2: 评估时间权重

- 最近信息的时间范围？（天、周、月）
- 历史数据的完整性和代表性？
- 信息重要性是否与时间相关？
- 长期趋势 vs 短期波动？

---

### Step 3: 分析近因机制

- 记忆可得性：最近信息更容易回忆
- 注意力偏向：新信息吸引更多注意力
- 情绪放大：最近事件情绪反应更强
- 外推倾向：将近期趋势视为长期

---

### Step 4: 校正近因效应

- 时间序列分析：查看完整历史数据
- 权重调整：按重要性而非时间加权
- 长期趋势识别：区分信号和噪声
- 设计时间检查清单：新≠重要

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **新≠重要**：最近信息不必然更重要。原因：记忆可得性使最近信息更容易回忆，但不代表其预测价值更高。
2. **短期波动≠长期趋势**：近期变化可能是噪声。原因：随机波动被误认为趋势，外推导致错误预测。
3. **注意力偏向新信息**：新信息自然吸引注意力。原因：大脑对新刺激敏感，但注意力分配不应等同于重要性分配。
4. **时间序列分析是解药**：查看完整历史数据。原因：完整时间序列揭示真实趋势，纠正近期信息过度加权。

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
- [ ] 是否识别了近因信号？
- [ ] 是否评估了时间权重和历史数据？
- [ ] 是否分析了近因驱动机制？
- [ ] 是否使用完整时间序列校正？
- [ ] 是否区分了短期波动和长期趋势？
- [ ] 输出具体可执行，不含模糊建议（如"看长期"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [primacy-effect](../thinking/primacy-effect/SKILL.md) | 并行 | 首因效应使最早信息影响大，近因效应使最近信息影响大 |
| [availability-bias](../thinking/availability-bias/SKILL.md) | 前置 | 可得性偏差解释为何最近信息更容易回忆 |
| [peak-end-rule](../thinking/peak-end-rule/SKILL.md) | 并行 | 峰终定律使结尾体验主导记忆，近因效应使最近信息主导判断 |
| [anchoring-effect](../thinking/anchoring-effect/SKILL.md) | 并行 | 锚定效应使初始值影响估计，近因效应使最新值影响估计 |

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

1. Murdock, B. B. (1962). The serial position effect of free recall. *Journal of Experimental Psychology*, 64(5), 482-488.
2. Hogarth, R. M., & Einhorn, H. J. (1992). Order effects in belief updating: The belief-adjustment model. *Cognitive Psychology*, 24(1), 1-55.
3. Schwarz, N., & Xu, J. (2011). Why don't we learn from poor choices? The consistency of expectation, choice, and memory coils the curse of experience. *Journal of Consumer Psychology*, 21(2), 139-145.
4. Weber, E. U., & Johnson, E. J. (2009). Mindful judgment and decision making. *Annual Review of Psychology*, 60, 53-85.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
