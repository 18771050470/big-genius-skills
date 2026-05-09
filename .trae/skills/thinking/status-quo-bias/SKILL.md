---
name: status-quo-bias
description: |
  触发：当需要评估是否因偏好现状而拒绝改变、需要分析维持现状的真实成本、需要识别不作为偏差时调用；常见信号包括"现在这样挺好"、"别折腾了"、"维持现状最安全"、"改变风险太大"。
  不触发：当现状确实是最优选择时（经客观评估）；当只需评估改变风险、无需评估维持现状成本时；当改变成本确实高于收益时。
  Invoke when needing to evaluate whether preference for status quo is driving decisions, analyze true cost of maintaining status quo, or identify omission bias.
  Do NOT invoke when status quo is objectively optimal after evaluation, when only assessing change risks without evaluating status quo costs, or when change costs truly exceed benefits.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["loss-aversion", "endowment-effect", "sunk-cost-fallacy", "opportunity-cost"]
---

# 现状偏差思维（Status Quo Bias Thinking）

## 核心定义

人们倾向于维持当前状态，即使改变能带来更好结果。Samuelson和Zeckhauser在1988年提出：现状偏差源于损失厌恶、沉没成本、选择成本和后悔规避。不作为偏差（omission bias）是其表现：人们认为不作为导致的伤害比作为导致的伤害更可接受。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充改变的成本收益分析、现状维持成本和替代选项数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别现状偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别现状偏差信号

- 是否出现"现在这样挺好"、"别折腾了"、"维持现状最安全"等表述？
- 是否高估改变风险、低估维持现状风险？
- 是否将"不作为"视为无风险选择？
- 是否因害怕后悔而拒绝改变？

---

### Step 2: 评估现状真实成本

- 维持现状的显性成本（直接支出）
- 维持现状的隐性成本（机会成本、效率损失）
- 维持现状的时间成本（延迟收益）
- 计算现状总成本 vs 改变总成本

---

### Step 3: 分析偏差驱动因素

- 损失厌恶：改变可能带来损失，现状感觉安全
- 沉没成本：已投入资源不愿放弃
- 选择成本：改变需要决策 effort，现状无需决策
- 后悔规避：害怕改变后后悔，不作为后悔感觉较轻

---

### Step 4: 设计改变评估框架

- 使用零基思维：如果现在没有这个选择，会重新选择吗？
- 计算改变 vs 不改变的期望值
- 考虑小步试错：最小可行性改变降低风险
- 设置改变触发条件：什么情况下必须改变？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **不作为也有成本**：维持现状不是无风险选择，机会成本和效率损失是隐性成本。原因：大脑将"不作为"视为默认选项，忽视其持续消耗。
2. **损失厌恶驱动现状偏好**：改变可能带来损失，现状感觉安全，即使现状实际在恶化。原因：损失痛感是收益快感的2倍，人们宁愿忍受已知痛苦也不愿冒险。
3. **零基思维破除现状锁定**：问"如果现在没有这个选择，会重新选择吗？"。原因：这个问题绕过了现状框架，直接评估选项真实价值。
4. **小步试错降低改变门槛**：最小可行性改变比全面变革更容易接受。原因：小步改变降低感知风险，提供快速反馈，减少后悔可能。

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
- [ ] 是否识别了现状偏差信号？
- [ ] 是否评估了现状真实成本（显性+隐性+时间）？
- [ ] 是否分析了偏差驱动因素（损失厌恶/沉没成本/选择成本/后悔规避）？
- [ ] 是否使用零基思维评估？
- [ ] 是否考虑了小步试错方案？
- [ ] 输出具体可执行，不含模糊建议（如"考虑改变"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 前置 | 损失厌恶是现状偏差的心理根源 |
| [endowment-effect](../thinking/endowment-effect/SKILL.md) | 并行 | 禀赋效应偏好拥有物，现状偏差偏好现状 |
| [sunk-cost-fallacy](../thinking/sunk-cost-fallacy/SKILL.md) | 并行 | 沉没成本导致不愿放弃现状 |
| [opportunity-cost](../thinking/opportunity-cost/SKILL.md) | 并行 | 机会成本揭示维持现状的真实代价 |

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

1. Samuelson, W., & Zeckhauser, R. (1988). Status quo bias in decision making. *Journal of Risk and Uncertainty*, 1(1), 7-59.
2. Kahneman, D., Knetsch, J. L., & Thaler, R. H. (1991). Anomalies: The endowment effect, loss aversion, and status quo bias. *Journal of Economic Perspectives*, 5(1), 193-206.
3. Ritov, I., & Baron, J. (1990). Reluctance to vaccinate: Omission bias and vaccine structure. *Journal of Behavioral Decision Making*, 3(4), 263-277.
4. Anderson, E. W., & Sullivan, M. W. (1993). The antecedents and consequences of customer satisfaction for firms. *Marketing Science*, 12(2), 125-143.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
