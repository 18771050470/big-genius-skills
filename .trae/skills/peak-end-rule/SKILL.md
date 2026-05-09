---
name: peak-end-rule
description: |
  触发：当需要评估体验记忆是否受峰值-终值规则影响、需要设计用户体验或服务流程、需要识别记忆与实际的差异时调用；常见信号包括"最后印象很重要"、"高潮部分决定一切"、"结尾不好全毁了"。
  不触发：当只需分析实时体验、无需考虑记忆偏差时；当体验确实由峰值和终值主导时（经实证验证）；当只需记录客观数据、无需评估主观记忆时。
  Invoke when needing to evaluate whether experience memory is affected by peak-end rule, design user experience or service processes, or identify memory-reality discrepancies.
  Do NOT invoke when only analyzing real-time experience without considering memory bias, when experience is truly dominated by peak and end (empirically verified), or when only recording objective data without evaluating subjective memory.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["availability-bias", "narrative-thinking", "empathy-gap", "framing-effect"]
---

# 峰值-终值规则思维（Peak-End Rule Thinking）

## 核心定义

人们对体验的记忆主要由峰值（最强烈时刻）和终值（结束时刻）决定，而非整体平均。Kahneman等在1993年结肠镜检查实验证明：较长但峰值较低、结尾较好的体验，记忆比较短但峰值较高的体验更好。持续时间被忽视（持续时间忽视）。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充体验的峰值时刻、终值时刻和整体分布数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别峰值-终值规则影响且设计方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别峰值-终值信号

- 是否出现"最后印象很重要"、"高潮部分决定一切"、"结尾不好全毁了"等表述？
- 体验记忆是否由峰值和终值主导？
- 是否忽视了体验的整体分布？
- 是否出现持续时间忽视？

---

### Step 2: 分析体验结构

- 峰值时刻是什么？（最强烈正面/负面时刻）
- 终值时刻是什么？（体验结束时的感受）
- 体验的整体分布如何？（平均值、方差）
- 持续时间多长？是否被忽视？

---

### Step 3: 评估记忆偏差

- 记忆评分 vs 实时评分差异
- 峰值和终值权重是否过高？
- 其他时刻是否被遗忘？
- 持续时间是否被忽视？

---

### Step 4: 设计体验优化

- 提升峰值：创造难忘的正面时刻
- 优化终值：确保体验以正面方式结束
- 减少负面峰值：降低最痛苦时刻的强度
- 不必优化每个时刻，聚焦峰值和终值

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **记忆≠体验**：人们对体验的记忆与实际体验不同。原因：记忆系统选择性编码，峰值和终值被过度加权，其他时刻被遗忘。
2. **峰值决定记忆**：最强烈时刻（无论正面负面）主导整体记忆。原因：情绪强度增强记忆编码，峰值时刻最容易被回忆。
3. **终值决定印象**：体验结束时的感受决定最终印象。原因：近因效应使最后时刻最容易被回忆，形成整体判断锚点。
4. **持续时间被忽视**：体验时长不影响记忆评分。原因：记忆系统不记录持续时间，只记录关键时刻，导致"更多痛苦"不等于"更坏记忆"。

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
- [ ] 是否识别了峰值-终值信号？
- [ ] 是否分析了体验结构（峰值、终值、分布）？
- [ ] 是否评估了记忆偏差？
- [ ] 是否设计了体验优化方案（提升峰值、优化终值）？
- [ ] 是否考虑了持续时间忽视？
- [ ] 输出具体可执行，不含模糊建议（如"改善结尾"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差回忆生动时刻，峰值-终值规则记忆峰值和终值 |
| [narrative-thinking](../thinking/narrative-thinking/SKILL.md) | 并行 | 叙事偏差编织体验故事，峰值-终值规则决定故事高潮和结尾 |
| [empathy-gap](../thinking/empathy-gap/SKILL.md) | 并行 | 共情差距使预测体验困难，峰值-终值规则影响体验记忆 |
| [framing-effect](../thinking/framing-effect/SKILL.md) | 并行 | 框架效应影响体验评估，峰值-终值规则影响体验记忆 |

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

1. Kahneman, D., Fredrickson, B. L., Schreiber, C. A., & Redelmeier, D. A. (1993). When more pain is preferred to less: Adding a better end. *Psychological Science*, 4(6), 401-405.
2. Redelmeier, D. A., & Kahneman, D. (1996). Patients' memories of painful medical treatments: Real-time and retrospective evaluations of two minimally invasive procedures. *Pain*, 66(1), 3-8.
3. Fredrickson, B. L. (2000). Extracting meaning from past affective experiences: The importance of peaks, ends, and specific emotions. *Cognition & Emotion*, 14(4), 577-606.
4. Do, A. M., Rupert, A. V., & Wolford, G. (2008). Evaluations of pleasurable experiences: The peak-end rule. *Psychonomic Bulletin & Review*, 15(1), 96-98.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
