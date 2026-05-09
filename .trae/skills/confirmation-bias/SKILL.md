---
name: confirmation-bias
description: |
  触发：当需要评估判断是否受确认偏误影响、需要识别选择性收集支持性证据、需要设计证伪机制时调用；常见信号包括"这证明我是对的"、"你看这个证据"、"所有迹象都表明"。
  不触发：当只需收集支持性证据用于演示时；当已有明确证伪机制和独立评审时；当只需记录已有证据、无需评估偏差时。
  Invoke when needing to evaluate whether judgments are affected by confirmation bias, identify selective collection of supporting evidence, or design falsification mechanisms.
  Do NOT invoke when only collecting supporting evidence for demonstration, when clear falsification mechanisms and independent review exist, or when only recording existing evidence without evaluating bias.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["availability-bias", "narrative-thinking", "scientific-method", "critical-thinking"]
---

# 确认偏误思维（Confirmation Bias Thinking）

## 核心定义

人们倾向于寻找、解释和回忆支持自己已有信念的证据，忽视或贬低反面证据。Wason在1960年通过"2-4-6实验"首次证明：人们倾向于验证而非证伪自己的假设。Nickerson在1998年综述确认偏误是"最普遍且最具破坏性的认知偏差"。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充反面证据、独立评审意见和证伪尝试记录
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别确认偏误影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别确认偏误信号

- 是否只收集支持性证据？
- 是否忽视或贬低反面证据？
- 是否出现"这证明我是对的"、"所有迹象都表明"等表述？
- 是否主动寻找证伪证据？

---

### Step 2: 评估证据收集偏差

- 证据来源是否多样化？还是单一来源？
- 是否主动搜索反面观点？
- 证据解读是否偏向支持已有信念？
- 回忆是否选择性记住支持性证据？

---

### Step 3: 设计证伪机制

- 列出3个为什么可能错的理由
- 寻找最强反面证据
- 邀请独立评审者挑战假设
- 设计可证伪的测试：什么证据能推翻当前结论？

---

### Step 4: 平衡证据评估

- 同等权重评估支持性和反面证据
- 使用盲审：不知道假设的情况下评估证据
- 计算证据强度比：支持证据 / 反面证据
- 考虑替代解释：同一证据能否支持不同结论？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **证伪比证实更有价值**：一个可靠反例足以推翻理论，再多正例也不能证明理论。原因：科学方法通过证伪推进知识，证实只能增加信心不能证明。
2. **大脑是确认机器**：人类天生偏好确认而非证伪，这是进化形成的认知捷径。原因：确认节省认知资源，证伪需要更多思考 effort。
3. **证据多样性是关键**：单一来源的证据即使再多也不如多来源的少量证据。原因：多来源证据减少系统性偏差，提高结论可靠性。
4. **独立评审是防线**：未参与假设形成的人更可能发现确认偏误。原因：独立评审者没有认知承诺，能更客观评估证据。

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
- [ ] **确认偏误特供**：是否识别了确认偏误信号？是否出现"这证明我是对的"、"所有迹象都表明"等表述？是否只收集支持性证据？
- [ ] **确认偏误特供**：是否评估了证据收集偏差？证据来源是否多样化？是否主动搜索反面观点？是否选择性记住支持性证据？
- [ ] **确认偏误特供**：是否设计了证伪机制？是否列出了至少3个为什么可能错的理由？是否寻找了最强反面证据？是否设计了可证伪的测试？
- [ ] **确认偏误特供**：是否同等权重评估支持性和反面证据？是否使用盲审方法？是否计算了证据强度比（支持证据/反面证据）？
- [ ] **确认偏误特供**：是否考虑了替代解释？同一证据能否支持不同结论？是否邀请了独立评审者挑战假设？
- [ ] 输出具体可执行，不含模糊建议（如"客观看待"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差回忆生动证据，确认偏误选择性回忆支持性证据 |
| [narrative-thinking](../thinking/narrative-thinking/SKILL.md) | 并行 | 叙事偏差编织支持性故事，确认偏误收集支持性证据 |
| [scientific-method](../thinking/scientific-method/SKILL.md) | 前置 | 科学方法提供证伪机制 |
| [critical-thinking](../thinking/critical-thinking/SKILL.md) | 前置 | 批判性思维提供客观评估证据的框架 |

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

1. Wason, P. C. (1960). On the failure to eliminate hypotheses in a conceptual task. *Quarterly Journal of Experimental Psychology*, 12(3), 129-140.
2. Nickerson, R. S. (1998). Confirmation bias: A ubiquitous phenomenon in many guises. *Review of General Psychology*, 2(2), 175-220.
3. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 10: The Law of Small Numbers)
4. Stanovich, K. E., & West, R. F. (1997). Reasoning independently of prior belief and individual differences in actively open-minded thinking. *Journal of Educational Psychology*, 89(2), 342-357.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
