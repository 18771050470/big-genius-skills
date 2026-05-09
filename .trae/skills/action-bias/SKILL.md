---
name: action-bias
description: |
  触发：当需要评估是否偏好行动而非观望、需要识别"做点什么总比不做强"偏差、需要判断等待是否更优时调用；常见信号包括"必须采取行动"、"做点什么总比不做强"、"不能干等着"。
  不触发：当只需描述行动偏好、无需评估行动价值时；当行动确实优于等待时（经期望值验证）；当只需记录行为、无需分析动机时。
  Invoke when needing to evaluate whether action is preferred over waiting, identify "doing something is better than nothing" bias, or judge whether waiting is superior.
  Do NOT invoke when only describing action preference without evaluating action value, when action is truly superior to waiting (verified by expected value), or when only recording behavior without analyzing motivation.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["omission-bias", "status-quo-bias", "overconfidence-effect", "regret-aversion"]
---

# 行动偏差思维（Action Bias Thinking）

## 核心定义

人们偏好采取行动而非观望，即使等待更优。Bar-Eli等人在2006年足球点球实验证明：守门员94%时间扑向一侧，但最佳策略是留在中间。行动感觉更可控，等待感觉被动。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充行动vs等待的期望值数据、历史案例和不确定性程度
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别行动偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别行动信号

- 是否出现"必须采取行动"、"做点什么总比不做强"、"不能干等着"等表述？
- 是否偏好行动而非等待？
- 是否因不作为感到焦虑？
- 是否高估行动价值低估等待价值？

---

### Step 2: 评估行动vs等待

- 行动的期望值是多少？
- 等待的期望值是多少？
- 不确定性程度如何？（高不确定时等待更有价值）
- 行动是否可逆？（不可逆行动需更谨慎）

---

### Step 3: 分析行动驱动

- 控制错觉：行动感觉更可控
- 社会压力：旁观者期望看到行动
- 后悔规避：不作为后悔更强烈
- 焦虑缓解：行动缓解不确定焦虑

---

### Step 4: 校正行动偏差

- 计算行动vs等待的期望值
- 评估信息价值：等待能否获得更多信息？
- 设计决策规则：何时行动vs何时等待
- 接受"无为"价值：有时不行动是最优策略

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **行动≠价值**：行动不一定创造价值，有时等待更优。原因：高不确定时，等待获得更多信息，减少决策错误。
2. **控制错觉驱动**：行动感觉更可控，但可能只是错觉。原因：大脑偏好确定性和控制感，行动提供虚假控制感。
3. **社会压力放大**：旁观者期望看到行动，即使等待更优。原因：行动被视为"负责任"，等待被视为"不作为"。
4. **期望值计算是解药**：比较行动vs等待的期望值。原因：期望值客观评估两种策略的真实价值，不受情感驱动。

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
- [ ] **行动偏差特供**：是否明确识别了"必须采取行动"、"做点什么总比不做强"等行动偏差信号？还是将正常的行动需求误判为偏差？
- [ ] **行动偏差特供**：是否计算了行动vs等待的期望值？高不确定性环境下等待的信息价值是否被量化？
- [ ] **行动偏差特供**：是否分析了行动背后的真实驱动机制（控制错觉、社会压力、后悔规避、焦虑缓解）？
- [ ] **行动偏差特供**：是否评估了行动的可逆性？不可逆行动是否获得了更严格的审视？
- [ ] **行动偏差特供**：是否设计了明确的"行动vs等待"决策规则？何时行动、何时等待是否有清晰边界？
- [ ] **行动偏差特供**：是否接受了"无为"作为有效策略？是否将"不行动"从道德层面去罪化？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"采取行动"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [omission-bias](../thinking/omission-bias/SKILL.md) | 并行 | 不作为偏差偏好不作为，行动偏差偏好行动 |
| [status-quo-bias](../thinking/status-quo-bias/SKILL.md) | 并行 | 现状偏差偏好当前状态，行动偏差偏好改变 |
| [overconfidence-effect](../thinking/overconfidence-effect/SKILL.md) | 并行 | 过度自信高估行动效果 |
| [regret-aversion](../thinking/regret-aversion/SKILL.md) | 并行 | 后悔规避害怕不作为后悔 |

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

1. Bar-Eli, M., Azar, O. H., Ritov, I., Keidar-Levin, Y., & Schein, G. (2006). Action bias among elite soccer goalkeepers: The case of penalty kicks. *Journal of Economic Psychology*, 27(2), 237-247.
2. Patt, A. G., & Zeckhauser, R. J. (2000). Action bias and environmental decision making: The case of groundwater contamination. *Journal of Risk and Uncertainty*, 20(1), 5-23.
3. Anderson, C. J. (2003). The psychology of doing nothing: Forms of decision avoidance result from reason and emotion. *Psychological Bulletin*, 129(1), 139-167.
4. Samuelson, W., & Zeckhauser, R. (1988). Status quo bias in decision making. *Journal of Risk and Uncertainty*, 1(1), 7-59.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
