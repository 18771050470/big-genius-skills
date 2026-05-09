---
name: hindsight-bias
description: |
  触发：当需要评估事后判断是否受结果知识影响、需要防止"我早就知道"错觉、需要客观复盘历史决策时调用；常见信号包括"我早就知道会这样"、"这很明显"、"当初就不该"。
  不触发：当只需记录历史事实、无需评估判断准确性时；当事件因果关系确实明确、无争议时；当只需总结经验教训、无需还原决策时情境时。
  Invoke when needing to evaluate whether post-hoc judgments are affected by outcome knowledge, prevent "I knew it all along" illusion, or objectively review historical decisions.
  Do NOT invoke when only recording historical facts without evaluating judgment accuracy, when event causality is truly clear and undisputed, or when only extracting lessons without reconstructing the decision-time context.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["overconfidence-effect", "confirmation-bias", "dual-process-thinking", "counterfactual-thinking"]
---

# 后见之明偏差思维（Hindsight Bias Thinking）

## 核心定义

当事件结果已知时，人们会高估自己在事件发生前对结果的预测能力，认为"我早就知道会这样"。Fischhoff在1975年提出：结果知识会不可逆地改变人们对事件事前概率的判断，导致" creeping determinism"（渐进决定论）——认为结果注定会发生。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充决策时可获得的信息、当时的不确定性和决策者的真实判断
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别后见之明偏差影响且还原方案明确，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别后见之明信号

- 是否出现"我早就知道"、"这很明显"、"当初就不该"等表述？
- 是否用结果反推原因，认为结果"注定"会发生？
- 是否忽视决策时存在的不确定性？
- 是否对决策者过于苛责，忽略决策时信息有限？

---

### Step 2: 还原决策时情境

- 决策时可获得哪些信息？哪些信息是事后才知道的？
- 决策时存在哪些不确定性？
- 决策者的真实判断是什么？（如果有记录）
- 区分"决策质量"和"结果质量"：好决策可能产生坏结果，坏决策可能产生好结果

---

### Step 3: 评估偏差程度

- 对比事前判断和事后判断的差异
- 结果知识是否改变了人们对事件概率的估计？
- 是否将复杂因果链简化为单因单果？
- 是否忽视了其他可能的结果路径？

---

### Step 4: 设计防偏差机制

- 决策日志：记录决策时的判断、理由和不确定性
- 事前概率估计：在结果未知时记录概率估计
- 独立复盘：由未参与决策的人进行复盘
- 多结果思维：考虑其他可能的结果路径，不只关注实际发生的结果

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **结果知识不可逆地改变记忆**：知道结果后，你无法"忘记"结果来还原事前判断。原因：Fischhoff实验证明，即使要求被试忽略结果信息，他们仍然受其影响。
2. **好决策≠好结果**：决策质量应该基于决策过程，而非结果。原因：不确定性世界中，好决策可能产生坏结果（概率事件）。
3. **"我早就知道"是错觉**：大多数"我早就知道"的判断是事后重构的记忆。原因：事前概率估计记录显示，人们实际预测准确度远低于事后声称。
4. **决策日志是最强防御**：记录决策时的判断和理由，防止事后重构。原因：书面记录不可篡改，是还原决策时情境的唯一可靠方式。

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
- [ ] 是否识别了后见之明信号？
- [ ] 是否还原了决策时可获得的信息和不确定性？
- [ ] 是否区分了决策质量和结果质量？
- [ ] 是否考虑了其他可能的结果路径？
- [ ] 是否设计了防偏差机制（决策日志、事前概率估计）？
- [ ] 输出具体可执行，不含模糊建议（如"客观复盘"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 前置 | 双过程思维识别系统1记忆重构，后见之明是系统1的典型偏差 |
| [counterfactual-thinking](../thinking/counterfactual-thinking/SKILL.md) | 并行 | 反事实思维考虑其他可能结果，对抗后见之明的单结果思维 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误选择性回忆支持性证据，后见之明重构记忆支持已知结果 |
| [overconfidence-effect](../thinking/overconfidence-effect/SKILL.md) | 并行 | 过度自信是后见之明的结果，后见之明导致过度自信 |

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

1. Fischhoff, B. (1975). Hindsight ≠ foresight: The effect of outcome knowledge on judgment under uncertainty. *Journal of Experimental Psychology: Human Perception and Performance*, 1(3), 288-299.
2. Roese, N. J., & Voth, K. D. (2010). Hindsight bias. In *Social Judgment and Decision Making* (pp. 171-184). Psychology Press.
3. Blank, H., Musch, J., & Pohl, R. F. (2007). Hindsight bias: On being wise after the event. *Social Cognition*, 25(1), 1-9.
4. Arkes, H. R., Wortmann, R. L., Saville, P. D., & Harkness, A. R. (1981). Hindsight bias among physicians weighing the likelihood of diagnosis. *Journal of Applied Psychology*, 66(2), 252-254.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
