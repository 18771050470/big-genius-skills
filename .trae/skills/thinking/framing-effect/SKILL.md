---
name: framing-effect
description: |
  触发：当需要评估决策是否受问题表述方式影响、需要识别不同框架下的选择反转、需要设计中性决策框架时调用；常见信号包括"90%存活率 vs 10%死亡率"、"省钱 vs 花钱"、"收益 vs 损失"。
  不触发：当只需理解不同表述方式、无需评估决策影响时；当框架差异不影响实质内容时；当决策者已接受框架效应训练时。
  Invoke when needing to evaluate whether decisions are affected by problem framing, identify preference reversals under different frames, or design neutral decision frames.
  Do NOT invoke when only understanding different表达方式 without evaluating decision impact, when frame differences do not affect substance, or when the decision maker has received framing effect training.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["prospect-theory", "loss-aversion", "anchoring-effect", "dual-process-thinking"]
---

# 框架效应思维（Framing Effect Thinking）

## 核心定义

同一问题的不同表述方式会导致不同的决策。Tversky和Kahneman在1981年亚洲疾病实验证明：当选项表述为"拯救200人"时72%选择确定选项，表述为"400人死亡"时仅22%选择同一选项。框架效应揭示决策受表述方式而非实质内容影响。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充问题的替代表述方式、历史决策数据和独立评估
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别框架效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别框架信号

- 问题如何被表述？收益框架还是损失框架？
- 是否出现"90%存活率 vs 10%死亡率"等表述差异？
- 数字如何呈现？绝对值还是百分比？
- 选项顺序是否影响选择？

---

### Step 2: 评估框架影响

- 用不同框架重新表述同一问题
- 比较不同框架下的选择偏好
- 是否出现选择反转？（同一人在不同框架下选择不同）
- 评估框架对决策的影响程度

---

### Step 3: 分析心理机制

- 损失框架触发风险寻求（宁愿冒险也不接受确定损失）
- 收益框架触发风险规避（宁愿确定收益也不冒险）
- 锚定效应：第一个看到的数字影响后续判断
- 情绪反应：不同框架触发不同情绪，情绪驱动决策

---

### Step 4: 设计中性框架

- 同时呈现收益和损失视角
- 使用绝对值和百分比双重呈现
- 随机化选项顺序
- 提供客观基准：同类决策的平均选择是什么？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **表述即操纵**：如何表述问题比问题本身更影响决策。原因：大脑依赖表述方式快速判断，不深入分析实质内容。
2. **损失框架触发冒险**：当问题表述为损失时，人们宁愿冒险也不接受确定损失。原因：损失厌恶使确定损失感觉更痛苦，冒险提供逃避希望。
3. **收益框架触发保守**：当问题表述为收益时，人们宁愿确定收益也不冒险。原因：确定收益感觉安全，冒险可能失去已获得的收益。
4. **双框架呈现是解药**：同时呈现收益和损失视角，帮助决策者看到完整图景。原因：双框架抵消单一框架偏差，促进理性分析。

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
- [ ] 是否识别了框架信号？
- [ ] 是否评估了框架影响（选择反转）？
- [ ] 是否分析了心理驱动机制？
- [ ] 是否设计了中性框架？
- [ ] 是否同时呈现收益和损失视角？
- [ ] 输出具体可执行，不含模糊建议（如"客观看待"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [prospect-theory](../thinking/prospect-theory/SKILL.md) | 前置 | 前景理论提供框架效应的理论基础 |
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 前置 | 损失厌恶解释为何损失框架触发冒险 |
| [anchoring-effect](../thinking/anchoring-effect/SKILL.md) | 并行 | 锚定效应与框架效应都影响判断起点 |
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 前置 | 双系统理论解释框架效应的认知机制 |

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

1. Tversky, A., & Kahneman, D. (1981). The framing of decisions and the psychology of choice. *Science*, 211(4481), 453-458.
2. Kahneman, D., & Tversky, A. (1979). Prospect theory: An analysis of decision under risk. *Econometrica*, 47(2), 263-291.
3. Levin, I. P., Schneider, S. L., & Gaeth, G. J. (1998). All frames are not created equal: A typology and critical analysis of framing effects. *Organizational Behavior and Human Decision Processes*, 76(2), 149-188.
4. Rothman, A. J., & Salovey, P. (1997). Shaping perceptions to motivate healthy behavior: The role of message framing. *Psychological Bulletin*, 121(1), 3-19.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
