---
name: omission-bias
description: |
  触发：当需要评估是否偏好不作为而非作为、需要比较作为和不作为的道德权重、需要识别"不作为无害"偏差时调用；常见信号包括"至少我没动手"、"顺其自然最安全"、"不做比做错好"。
  不触发：当作为和不作为确实有明确道德差异时；当只需记录行为选择、无需道德评估时；当不作为确实优于作为时（经客观评估）。
  Invoke when needing to evaluate whether inaction is preferred over action, compare moral weight of action vs inaction, or identify "inaction is harmless" bias.
  Do NOT invoke when action and inaction truly have clear moral differences, when only recording behavioral choices without moral evaluation, or when inaction is truly superior to action (objectively evaluated).
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["status-quo-bias", "loss-aversion", "regret-aversion", "moral-foundations"]
---

# 不作为偏差思维（Omission Bias Thinking）

## 核心定义

人们认为不作为导致的伤害比作为导致的伤害更可接受，即使不作为伤害更大。Ritov和Baron在1990年疫苗实验证明：即使疫苗风险远低于疾病风险，父母仍偏好不接种，因为"不作为"导致的疾病感觉比"作为"导致的疫苗副作用更可接受。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充作为和不作为的预期伤害数据、历史案例和道德框架
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别不作为偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别不作为信号

- 是否出现"至少我没动手"、"顺其自然最安全"、"不做比做错好"等表述？
- 是否偏好不作为，即使不作为伤害更大？
- 是否认为"不作为"导致的伤害比"作为"导致的伤害更可接受？
- 是否将"不作为"视为无责任选择？

---

### Step 2: 评估作为vs不作为

- 作为的预期伤害是多少？（概率 × 严重程度）
- 不作为的预期伤害是多少？
- 作为的预期收益是多少？
- 不作为的预期收益是多少？

---

### Step 3: 分析心理机制

- 责任归属：作为导致的伤害感觉更"负责"
- 后悔模式：作为后后悔比不作为后后悔更强烈
- 社会规范：社会更谴责"作为"导致的伤害
- 控制错觉：不作为感觉"自然"，作为感觉"干预"

---

### Step 4: 校正偏差

- 同等评估作为和不作为的预期后果
- 使用期望值计算替代直觉判断
- 考虑"不作为也是选择"
- 设计决策框架：如果选择不作为，等于选择接受不作为后果

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **不作为也是选择**：选择不作为等于选择接受不作为的后果。原因：不选择本身就是一种选择，放弃干预导致可预防的伤害同样有责任。
2. **预期后果同等重要**：作为和不作为的伤害应该用相同期望值标准评估。原因：伤害的来源（作为vs不作为）不影响伤害本身的大小。
3. **后悔不对称是偏差**：作为后后悔更强烈，但不作为后悔同样真实。原因：大脑对"主动犯错"的记忆更深刻，但"被动错过"的累积后悔同样严重。
4. **期望值计算是解药**：用数学期望值替代直觉判断。原因：期望值同等对待作为和不作为，消除道德权重偏差。

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
- [ ] 是否识别了不作为信号？
- [ ] 是否评估了作为vs不作为的预期后果？
- [ ] 是否分析了心理驱动机制？
- [ ] 是否使用期望值计算校正？
- [ ] 是否考虑了"不作为也是选择"？
- [ ] 输出具体可执行，不含模糊建议（如"积极行动"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [status-quo-bias](../thinking/status-quo-bias/SKILL.md) | 并行 | 现状偏差偏好当前状态，不作为偏差偏好不干预 |
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 前置 | 损失厌恶使作为导致的损失感觉更严重 |
| [regret-aversion](../thinking/regret-aversion/SKILL.md) | 前置 | 后悔规避解释为何害怕作为后后悔 |
| [moral-foundations](../thinking/moral-foundations/SKILL.md) | 并行 | 道德基础理论解释作为vs不作为的道德权重差异 |

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

1. Ritov, I., & Baron, J. (1990). Reluctance to vaccinate: Omission bias and vaccine structure. *Journal of Behavioral Decision Making*, 3(4), 263-277.
2. Baron, J., & Ritov, I. (1994). Reference points and omission bias. *Organizational Behavior and Human Decision Processes*, 59(3), 475-498.
3. Spranca, M., Minsk, E., & Baron, J. (1991). Omission and commission in judgment and choice. *Journal of Experimental Social Psychology*, 27(1), 76-105.
4. Asch, D. A., Baron, J., Hershey, J. C., Kunreuther, H., Meszaros, J., & Ubel, P. (1998). Omission bias and influenza vaccination. *JAMA*, 279(4), 287-288.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
