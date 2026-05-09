---
name: projection-bias
description: |
  触发：当需要评估预测是否将当前状态投射到未来、需要识别"我现在这样未来也会这样"偏差、需要校正跨期偏好预测时调用；常见信号包括"我一直都会这样想"、"以后也会喜欢"、"我现在不饿所以以后也不饿"。
  不触发：当只需描述当前状态、无需预测未来时；当偏好确实稳定、无显著变化时（经历史数据验证）；当只需分析当前决策、无需跨期预测时。
  Invoke when needing to evaluate whether predictions project current state to future, identify "I'm like this now so I'll be like this later" bias, or correct intertemporal preference predictions.
  Do NOT invoke when only describing current state without predicting future, when preferences are truly stable without significant changes (verified by historical data), or when only analyzing current decisions without intertemporal prediction.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["empathy-gap", "status-quo-bias", "affect-heuristic", "planning-fallacy"]
---

# 投射偏差思维（Projection Bias Thinking）

## 核心定义

人们将当前偏好、信念和情绪状态投射到未来，低估变化可能性。Loewenstein等人在2003年提出：投射偏差使人们高估未来与现在的相似度，导致跨期决策系统性错误。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充历史偏好变化数据、状态转换记录和跨期决策案例
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别投射偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别投射信号

- 是否出现"我一直都会这样想"、"以后也会喜欢"、"我现在不饿所以以后也不饿"等表述？
- 是否将当前偏好投射到未来？
- 是否低估了偏好变化可能性？
- 是否假设未来与现在相同？

---

### Step 2: 评估状态差异

- 当前状态是什么？（情绪、生理、环境）
- 未来状态可能是什么？
- 状态变化如何影响偏好？
- 历史数据：过去偏好变化频率和幅度

---

### Step 3: 分析投射机制

- 当前状态作为锚点：未来偏好=当前偏好+小调整
- 调整不足：低估状态变化影响
- 情感状态投射：当前情绪影响未来情绪预测
- 生理状态投射：当前饥饿/饱腹影响未来食欲预测

---

### Step 4: 校正投射偏差

- 使用历史数据：过去偏好变化记录
- 场景模拟：不同状态下的偏好差异
- 预设承诺：当前状态设置未来约束
- 双状态规划：为不同状态制定不同计划

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **现在≠未来**：当前状态不能准确预测未来偏好。原因：状态变化（情绪、生理、环境）改变偏好，投射偏差低估变化幅度。
2. **锚定调整不足**：人们以当前状态为锚点，但调整幅度不足。原因：当前状态太强烈，难以想象不同状态下的偏好，导致调整不足。
3. **历史数据优于直觉**：过去偏好变化记录比当前直觉更可靠。原因：历史数据包含真实变化，直觉受当前状态影响。
4. **预设承诺是解药**：当前状态设置未来约束，绕过投射偏差。原因：预设承诺不依赖未来状态下的自控力，在当前理性状态下生效。

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
- [ ] 是否识别了投射信号？
- [ ] 是否评估了当前vs未来状态差异？
- [ ] 是否分析了投射驱动机制？
- [ ] 是否使用历史数据校正？
- [ ] 是否设计了预设承诺机制？
- [ ] 输出具体可执行，不含模糊建议（如"考虑变化"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [empathy-gap](../thinking/empathy-gap/SKILL.md) | 并行 | 共情差距使预测不同状态行为困难，投射偏差将当前状态投射到未来 |
| [status-quo-bias](../thinking/status-quo-bias/SKILL.md) | 并行 | 现状偏差偏好当前状态，投射偏差假设未来保持当前状态 |
| [affect-heuristic](../thinking/affect-heuristic/SKILL.md) | 并行 | 情感启发式用当前情感判断，投射偏差将当前情感投射到未来 |
| [planning-fallacy](../thinking/planning-fallacy/SKILL.md) | 并行 | 规划谬误低估未来时间，投射偏差低估未来偏好变化 |

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

1. Loewenstein, G., O'Donoghue, T., & Rabin, M. (2003). Projection bias in predicting future utility. *Quarterly Journal of Economics*, 118(4), 1209-1248.
2. Loewenstein, G. (1996). Out of control: Visceral influences on behavior. *Organizational Behavior and Human Decision Processes*, 65(3), 272-292.
3. Read, D., & van Leeuwen, B. (1998). Predicting hunger: The effects of appetite and delay on choice. *Organizational Behavior and Human Decision Processes*, 76(3), 267-275.
4. Van Boven, L., & Loewenstein, G. (2003). Projection of transient drive states. *Personality and Social Psychology Bulletin*, 29(9), 1159-1168.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
