---
name: hyperbolic-discounting
description: |
  触发：当需要评估跨期选择是否受双曲贴现影响、需要识别"现在就要"vs"以后更多"偏好反转、需要优化长期决策时调用；常见信号包括"先拿到手再说"、"现在享受最重要"、"以后的事以后再说"。
  不触发：当只需描述时间偏好、无需分析偏好反转时；当贴现率确实恒定、无时间不一致时（经指数贴现验证）；当只需比较即时选项、无需跨期分析时。
  Invoke when needing to evaluate whether intertemporal choices are affected by hyperbolic discounting, identify "now vs later more" preference reversal, or optimize long-term decisions.
  Do NOT invoke when only describing time preferences without analyzing preference reversal, when discount rate is truly constant without time inconsistency (verified by exponential discounting), or when only comparing immediate options without intertemporal analysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["present-bias", "sunk-cost-fallacy", "empathy-gap", "commitment-device"]
---

# 双曲贴现思维（Hyperbolic Discounting Thinking）

## 核心定义

人们对近期未来贴现率远高于远期未来，导致偏好反转。Ainslie在1975年提出：今天拿$100 vs 明天拿$120选今天，但30天后拿$100 vs 31天后拿$120选31天。时间不一致性使长期计划被短期冲动破坏。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充时间偏好数据、历史选择记录和承诺机制
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别双曲贴现影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别双曲信号

- 是否出现"先拿到手再说"、"现在享受最重要"、"以后的事以后再说"等表述？
- 是否偏好即时小奖励胜过延迟大奖励？
- 是否出现偏好反转？（远期选大奖励，近期选小奖励）
- 是否长期计划被短期冲动破坏？

---

### Step 2: 评估贴现模式

- 即时选项的贴现率？（通常极高）
- 远期选项的贴现率？（通常较低）
- 贴现率随时间如何变化？（双曲vs指数）
- 偏好反转点在哪里？

---

### Step 3: 分析时间不一致性

- 今天的偏好 vs 明天的偏好是否一致？
- 长期计划执行率如何？
- 什么触发短期冲动？（情绪、环境、诱惑）
- 自控力消耗如何影响选择？

---

### Step 4: 设计承诺机制

- 预设承诺：当前理性状态设置未来约束
- 自动执行：减少未来选择自由度
- 增加即时成本：使短期冲动代价更高
- 分解长期目标：使远期奖励更具体可感

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **贴现率不恒定**：近期贴现率远高于远期。原因：大脑对即时奖励反应强烈，对延迟奖励折扣过度，导致时间不一致性。
2. **偏好反转普遍**：远期选大奖励，近期选小奖励。原因：随时间接近，即时选项的吸引力急剧增加，超过理性计算。
3. **长期计划易被破坏**：今天制定的计划明天被冲动破坏。原因：计划时是理性状态，执行时是冲动状态，状态变化导致偏好变化。
4. **承诺机制是解药**：当前理性状态设置未来约束。原因：承诺机制减少未来选择自由度，使短期冲动无法执行。

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
- [ ] 是否识别了双曲信号？
- [ ] 是否评估了贴现模式和时间不一致性？
- [ ] 是否分析了偏好反转机制？
- [ ] 是否设计了承诺机制？
- [ ] 是否考虑了自控力消耗影响？
- [ ] 输出具体可执行，不含模糊建议（如"延迟满足"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [present-bias](../thinking/present-bias/SKILL.md) | 前置 | 现时偏差是双曲贴现的表现形式 |
| [sunk-cost-fallacy](../thinking/sunk-cost-fallacy/SKILL.md) | 并行 | 沉没成本谬误因已投入而继续，双曲贴现因即时诱惑而放弃 |
| [empathy-gap](../thinking/empathy-gap/SKILL.md) | 并行 | 共情差距使预测未来冲动困难 |
| [commitment-device](../thinking/commitment-device/SKILL.md) | 前置 | 承诺机制提供双曲贴现的解决方案 |

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

1. Ainslie, G. (1975). Specious reward: A behavioral theory of impulsiveness and impulse control. *Psychological Bulletin*, 82(4), 463-496.
2. Laibson, D. (1997). Golden eggs and hyperbolic discounting. *Quarterly Journal of Economics*, 112(2), 443-477.
3. O'Donoghue, T., & Rabin, M. (1999). Doing it now or later. *American Economic Review*, 89(1), 103-124.
4. Thaler, R. H., & Shefrin, H. M. (1981). An economic theory of self-control. *Journal of Political Economy*, 89(2), 392-406.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
