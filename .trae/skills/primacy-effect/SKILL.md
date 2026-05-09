---
name: primacy-effect
description: |
  触发：当需要评估判断是否受最早信息过度影响、需要识别"第一印象决定一切"偏差、需要校正印象形成时调用；常见信号包括"第一印象很差"、"一开始就不看好"、"先入为主"。
  不触发：当只需描述第一印象、无需评估后续信息影响时；当最早信息确实最具预测价值时（经数据验证）；当只需记录初始印象、无需分析偏差时。
  Invoke when needing to evaluate whether judgments are over-affected by earliest information, identify "first impression decides everything" bias, or correct impression formation.
  Do NOT invoke when only describing first impression without evaluating subsequent information impact, when earliest information truly has most predictive value (verified by data), or when only recording initial impression without analyzing bias.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["recency-effect", "halo-effect", "anchoring-effect", "confirmation-bias"]
---

# 首因效应思维（Primacy Effect Thinking）

## 核心定义

人们过度重视最早获得的信息。Asch在1946年印象形成实验证明：先听到正面描述的人78%认为吉姆外向，先听负面描述的人只有18%认为外向。第一印象形成后难以改变。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充后续信息质量、第一印象准确性和印象变化数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别首因效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别首因信号

- 是否出现"第一印象很差"、"一开始就不看好"、"先入为主"等表述？
- 是否过度重视最早信息？
- 是否忽视后续矛盾信息？
- 是否第一印象形成后拒绝改变？

---

### Step 2: 评估信息序列

- 最早信息的质量如何？（准确性、代表性）
- 后续信息是否矛盾？（新证据）
- 印象是否随新信息更新？
- 最早信息权重是否过高？

---

### Step 3: 分析首因机制

- 注意力峰值：最早信息获得最多注意力
- 解释框架：第一印象成为后续信息解释框架
- 一致性偏好：维持初始印象一致性
- 确认偏误：寻找支持第一印象的证据

---

### Step 4: 校正首因效应

- 信息重新加权：按质量而非顺序加权
- 后续信息优先：特别关注矛盾信息
- 印象更新规则：设定印象更新触发条件
- 设计序列检查清单：先≠重要

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **先≠重要**：最早信息不必然最重要。原因：注意力峰值使最早信息被过度编码，但不代表其预测价值最高。
2. **解释框架锁定**：第一印象成为后续信息过滤器。原因：一致性偏好使后续信息被解释为支持第一印象，矛盾信息被折扣。
3. **印象更新困难**：改变第一印象需要强证据。原因：初始印象形成认知锚点，后续调整不足，需要更强证据才能改变。
4. **重新加权是解药**：按信息质量而非顺序加权。原因：质量加权揭示信息真实价值，纠正顺序导致的偏差。

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
- [ ] 是否识别了首因信号？
- [ ] 是否评估了信息序列和权重？
- [ ] 是否分析了首因驱动机制？
- [ ] 是否使用信息重新加权校正？
- [ ] 是否特别关注了矛盾信息？
- [ ] 输出具体可执行，不含模糊建议（如"改变第一印象"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [recency-effect](../thinking/recency-effect/SKILL.md) | 并行 | 近因效应使最近信息影响大，首因效应使最早信息影响大 |
| [halo-effect](../thinking/halo-effect/SKILL.md) | 并行 | 晕轮效应使单一特征扩散，首因效应使最早特征主导 |
| [anchoring-effect](../thinking/anchoring-effect/SKILL.md) | 前置 | 锚定效应解释为何第一印象成为认知锚点 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误使寻找支持第一印象的证据 |

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

1. Asch, S. E. (1946). Forming impressions of personality. *Journal of Abnormal and Social Psychology*, 41(3), 258-290.
2. Luchins, A. S. (1957). Order of presentation in persuasion. *Psychological Bulletin*, 54(2), 126-136.
3. Jones, E. E., & Goethals, G. R. (1972). Order effects in impression formation. *Journal of Personality and Social Psychology*, 24(1), 1-10.
4. Nisbett, R. E., & Ross, L. (1980). *Human Inference: Strategies and Shortcomings of Social Judgment*. Prentice-Hall.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
