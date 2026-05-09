---
name: regret-aversion
description: |
  触发：当需要评估决策是否受预期后悔影响、需要识别"害怕后悔而不行动"偏差、需要优化风险决策时调用；常见信号包括"万一后悔怎么办"、"不敢选怕后悔"、"选了错的会后悔一辈子"。
  不触发：当只需描述后悔情绪、无需决策优化时；当后悔确实是最重要决策因素时（经多维权衡验证）；当只需记录情感反应、无需理性分析时。
  Invoke when needing to evaluate whether decisions are affected by anticipated regret, identify "afraid to act due to regret fear" bias, or optimize risk decisions.
  Do NOT invoke when only describing regret emotion without decision optimization, when regret is truly the most important decision factor (verified by multi-criteria evaluation), or when only recording emotional responses without rational analysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["loss-aversion", "status-quo-bias", "omission-bias", "outcome-bias"]
---

# 后悔规避思维（Regret Aversion Thinking）

## 核心定义

人们为避免预期后悔而改变决策，即使期望值更优。Bell和Loomes&Sugden在1982年同时提出后悔理论：决策者预期如果选错会后悔，这种预期后悔被纳入决策函数，导致风险规避和现状偏好。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充各选项期望值、历史后悔记录和风险偏好数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别后悔规避影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别后悔信号

- 是否出现"万一后悔怎么办"、"不敢选怕后悔"、"选了错的会后悔一辈子"等表述？
- 是否因害怕后悔而避免决策？
- 是否偏好不作为以避免后悔？
- 是否高估后悔强度和持续时间？

---

### Step 2: 评估后悔影响

- 预期后悔强度是多少？（1-10评分）
- 预期后悔持续时间？（实际通常短于预期）
- 后悔对决策的影响权重？
- 历史数据：过去后悔强度和持续时间

---

### Step 3: 分析后悔机制

- 作为后悔 vs 不作为后悔：哪个更强烈？
- 反事实比较：与未选选项比较产生后悔
- 责任归属：作为导致的后悔感觉更"负责"
- 影响偏差：高估后悔强度和持续时间

---

### Step 4: 校正后悔规避

- 计算期望值：忽略后悔情绪，只看数学期望
- 使用历史数据：过去后悔实际强度 vs 预期
- 设计决策框架：如果后悔，能否逆转决策？
- 比较作为vs不作为后悔：哪个更可能？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **后悔≠决策标准**：后悔是情绪反应，不应主导决策。原因：后悔基于反事实比较，但反事实不可知，用不可知信息决策不理性。
2. **影响偏差普遍**：人们高估后悔强度和持续时间。原因：情感预测不准确，实际后悔强度通常远低于预期，恢复速度快于预期。
3. **作为vs不对称**：作为后后悔比不作为后后悔更强烈，但不作为后悔累积更严重。原因：大脑对"主动犯错"记忆深刻，但"被动错过"的累积后悔同样真实。
4. **期望值是解药**：用数学期望值替代后悔情绪。原因：期望值客观比较选项真实价值，不受情绪偏差影响。

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
- [ ] 是否识别了后悔信号？
- [ ] 是否评估了后悔强度和持续时间？
- [ ] 是否分析了后悔驱动机制？
- [ ] 是否使用期望值计算校正？
- [ ] 是否比较了作为vs不作为后悔？
- [ ] 输出具体可执行，不含模糊建议（如"不要后悔"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 前置 | 损失厌恶使损失感觉更严重，后悔规避害怕损失后后悔 |
| [status-quo-bias](../thinking/status-quo-bias/SKILL.md) | 并行 | 现状偏差偏好当前状态，后悔规避害怕改变后后悔 |
| [omission-bias](../thinking/omission-bias/SKILL.md) | 并行 | 不作为偏差偏好不作为，后悔规避害怕作为后后悔 |
| [outcome-bias](../thinking/outcome-bias/SKILL.md) | 并行 | 结果偏差用结果评价决策，后悔规避用预期结果影响决策 |

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

1. Bell, D. E. (1982). Regret in decision making under uncertainty. *Operations Research*, 30(5), 961-981.
2. Loomes, G., & Sugden, R. (1982). Regret theory: An alternative theory of rational choice under uncertainty. *Economic Journal*, 92(368), 805-824.
3. Zeelenberg, M. (1999). Anticipated regret, expected feedback and behavioral decision making. *Journal of Behavioral Decision Making*, 12(2), 93-106.
4. Gilovich, T., & Medvec, V. H. (1995). The experience of regret: What, when, and why. *Psychological Review*, 102(2), 379-395.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
