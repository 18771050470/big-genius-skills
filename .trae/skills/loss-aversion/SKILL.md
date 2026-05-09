---
name: loss-aversion
description: |
  触发：当需要评估决策是否受损失厌恶影响、需要比较损失和收益的不对称权重、需要设计激励机制时调用；常见信号包括"亏了不想卖"、"宁可不错也不愿冒险"、"保住已有的比获得新的更重要"。
  不触发：当损失和收益权重确实相等时（经实验验证）；当只需纯数学计算、无需考虑心理因素时；当决策者是专业交易员且经过严格训练时。
  Invoke when needing to evaluate whether decisions are affected by loss aversion, compare asymmetric weighting of losses vs gains, or design incentive mechanisms.
  Do NOT invoke when loss and gain weights are truly equal (experimentally verified), when only pure mathematical calculation is needed without psychological factors, or when the decision maker is a professional trader with rigorous training.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["prospect-theory", "sunk-cost-fallacy", "endowment-effect", "dual-process-thinking"]
---

# 损失厌恶思维（Loss Aversion Thinking）

## 核心定义

人们对损失的敏感度远高于对等量收益的敏感度。Kahneman和Tversky在1979年前景理论中证明：损失的心理影响约为等量收益的2-2.5倍。Thaler进一步提出"禀赋效应"：人们对自己拥有的物品估值高于未拥有时。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充决策的潜在损失和收益金额、决策者风险偏好和参考点
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确损失厌恶影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别参考点

- 决策者的参考点是什么？（现状、期望、历史高点）
- 参考点决定了什么是"损失"、什么是"收益"
- 参考点可能被操纵：框架效应改变参考点
- 标注当前参考点和可能的替代参考点

---

### Step 2: 评估损失厌恶程度

- 潜在损失金额 vs 潜在收益金额
- 损失的心理权重约为收益的2-2.5倍
- 计算损失厌恶比率：损失心理影响 / 收益心理影响
- 评估是否因过度规避损失而错失正向预期机会

---

### Step 3: 识别损失厌恶偏差

- 处置效应：亏损股票持有过久，盈利股票卖出过早
- 现状偏差：偏好维持现状，即使改变有正向预期
- 禀赋效应：对自己拥有的物品估值过高
- 检查当前决策是否受这些偏差影响

---

### Step 4: 校正决策框架

- 用期望值替代直觉判断：概率 × 金额
- 改变参考点：从"避免损失"转向"最大化期望收益"
- 设计自动决策规则：预设止损/止盈点，减少情绪干预
- 考虑组合视角：单个决策的损失在组合中可能被抵消

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **损失痛感是收益快感的2倍**：前景理论核心发现，损失100元的痛苦需要获得200-250元才能抵消。原因：进化偏好风险规避，错过收益的代价小于遭受损失的代价。
2. **参考点决定一切**：同一结果在不同参考点下被感知为损失或收益。原因：人们评估相对变化而非绝对水平，参考点是评估的锚。
3. **禀赋效应扭曲估值**：拥有某物后对其估值立即上升。原因：损失厌恶使人们将放弃拥有物感知为损失，要求更高补偿。
4. **组合视角对抗损失厌恶**：单个决策的损失在组合视角下被平滑。原因：关注整体组合而非单个决策，减少单次损失的心理冲击。

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
- [ ] 参考点是否被准确识别？
- [ ] 损失厌恶比率是否被量化？
- [ ] 是否识别了处置效应、现状偏差、禀赋效应？
- [ ] 是否因过度规避损失而错失正向预期机会？
- [ ] 是否设计了自动决策规则减少情绪干预？
- [ ] 输出具体可执行，不含模糊建议（如"克服恐惧"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [prospect-theory](../thinking/prospect-theory/SKILL.md) | 前置 | 前景理论提供损失厌恶的理论框架和数学模型 |
| [sunk-cost-fallacy](../thinking/sunk-cost-fallacy/SKILL.md) | 并行 | 损失厌恶是沉没成本谬误的心理根源 |
| [endowment-effect](../thinking/endowment-effect/SKILL.md) | 并行 | 禀赋效应是损失厌恶在所有权场景的表现 |
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 前置 | 双过程思维识别系统1情绪反应，损失厌恶是系统1的典型偏差 |

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

1. Kahneman, D., & Tversky, A. (1979). Prospect theory: An analysis of decision under risk. *Econometrica*, 47(2), 263-291.
2. Tversky, A., & Kahneman, D. (1991). Loss aversion in riskless choice: A reference-dependent model. *Quarterly Journal of Economics*, 106(4), 1039-1061.
3. Thaler, R. H. (1980). Toward a positive theory of consumer choice. *Journal of Economic Behavior & Organization*, 1(1), 39-60.
4. Odean, T. (1998). Are investors reluctant to realize their losses? *Journal of Finance*, 53(5), 1775-1798.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
