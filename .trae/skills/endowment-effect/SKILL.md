---
name: endowment-effect
description: |
  触发：当需要评估是否因拥有某物而高估其价值、需要设计交易或激励机制、需要识别所有权偏差时调用；常见信号包括"我的东西更值钱"、"卖了太可惜"、"给我多少都不换"。
  不触发：当只需评估市场公允价值、无需考虑心理因素时；当决策者是专业交易员且经过严格训练时；当物品对决策者无情感依附时。
  Invoke when needing to evaluate whether ownership inflates perceived value, design transaction or incentive mechanisms, or identify ownership bias.
  Do NOT invoke when only assessing market fair value without psychological factors, when the decision maker is a professional trader with rigorous training, or when the item has no emotional attachment.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["loss-aversion", "prospect-theory", "status-quo-bias", "sunk-cost-fallacy"]
---

# 禀赋效应思维（Endowment Effect Thinking）

## 核心定义

人们对自己拥有的物品估值高于未拥有时。Thaler在1980年提出：一旦拥有某物，放弃它就被感知为损失，而损失的心理影响是等量收益的2倍。Kahneman、Knetsch和Thaler在1990年通过咖啡杯实验证明：拥有者要价是中位数的2倍以上。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充物品市场价值、拥有时长和情感依附程度
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别禀赋效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别所有权影响

- 是否拥有该物品？拥有多久了？
- 对物品的情感依附程度？
- 是否出现"我的东西更值钱"、"卖了太可惜"等表述？
- 估值是否显著高于市场公允价值？

---

### Step 2: 评估禀赋效应程度

- 拥有者要价 vs 非拥有者愿付价格
- 禀赋效应比率 = 拥有者估值 / 市场公允价值
- 实验显示比率通常为1.5-2.5倍
- 评估是否因禀赋效应错失交易机会

---

### Step 3: 分析心理机制

- 损失厌恶：放弃拥有物被感知为损失
- 自我关联：物品成为自我身份的一部分
- 熟悉偏好：拥有的物品更熟悉，熟悉产生偏好
- 标注主要驱动因素

---

### Step 4: 校正估值

- 使用市场公允价值替代主观估值
- 考虑替代成本：如果现在没有，愿意花多少钱买？
- 考虑机会成本：持有该物品放弃的其他价值
- 设计客观评估流程：第三方评估、市场比较

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **拥有即增值**：一旦拥有某物，大脑自动提高其估值。原因：损失厌恶使放弃被感知为损失，损失痛感是收益快感的2倍，要求更高补偿才愿放弃。
2. **情感依附放大效应**：对物品的情感依附越强，禀赋效应越大。原因：物品成为自我身份的一部分，放弃物品被感知为自我损失。
3. **市场价值是锚**：客观市场价值是校正禀赋效应的最佳参照。原因：市场价格反映供需平衡，不受个人所有权偏差影响。
4. **替代思维对抗禀赋**：问自己"如果现在没有，愿意花多少钱买？"。原因：这个问题绕过了所有权框架，直接评估物品真实价值。

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
- [ ] 是否识别了所有权影响？
- [ ] 是否评估了禀赋效应程度？
- [ ] 是否分析了心理驱动因素？
- [ ] 是否使用市场公允价值校正？
- [ ] 是否考虑了替代成本和机会成本？
- [ ] 输出具体可执行，不含模糊建议（如"客观估值"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 前置 | 损失厌恶是禀赋效应的心理根源 |
| [prospect-theory](../thinking/prospect-theory/SKILL.md) | 前置 | 前景理论提供损失厌恶的理论框架 |
| [status-quo-bias](../thinking/status-quo-bias/SKILL.md) | 并行 | 现状偏差与禀赋效应都偏好当前状态 |
| [sunk-cost-fallacy](../thinking/sunk-cost-fallacy/SKILL.md) | 并行 | 沉没成本与禀赋效应都导致非理性坚持 |

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

1. Thaler, R. H. (1980). Toward a positive theory of consumer choice. *Journal of Economic Behavior & Organization*, 1(1), 39-60.
2. Kahneman, D., Knetsch, J. L., & Thaler, R. H. (1990). Experimental tests of the endowment effect and the Coase theorem. *Journal of Political Economy*, 98(6), 1325-1348.
3. Morewedge, C. K., et al. (2009). Selling one's good: Memory, evaluation, and the endowment effect. *Journal of Consumer Research*, 36(3), 443-455.
4. Ariely, D., Huber, J., & Wertenbroch, K. (2005). When do losses loom larger than gains? *Journal of Marketing Research*, 42(2), 134-138.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
