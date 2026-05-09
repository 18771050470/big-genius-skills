---
name: abductive-thinking
description: |
  触发：当面对 "为什么会出现这种情况？"、"是什么原因导致了这个结果？"、"从已知线索中推理最可能的解释" 等逆向归因场景时调用；常见信号包括 异常现象分析、故障排查、诊断推理、线索整合。
  不触发：当目标是从一般原理推导具体结论时（应使用演绎思维）；当需要从大量案例中总结普遍规律时（应使用归纳思维）；当问题是在没有观察结果的情况下纯粹猜测时（缺乏推理起点）。
  Invoke when: facing an observed outcome and needing to infer the most plausible cause; common signals include anomaly analysis, fault diagnosis, detective reasoning, evidence integration.
  Do NOT invoke when: deriving specific conclusions from general principles (use deductive thinking); when summarizing general patterns from many cases (use inductive thinking); when purely guessing without observed outcomes.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["deductive-thinking", "inductive-thinking", "system-thinking", "first-principles"]
---

# 溯因思维（Abductive Thinking）

## 核心定义

从已知结果反推最可能的原因，是"最佳解释推理"。不追求绝对真理，而是寻找最合理、解释力最强的候选假设。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 明确观察结果

- 将模糊描述转化为精确的、可重复的观察事实清单
- 去除噪音，区分直接观察与推测
- 标注每个观察的时间、类型、信度

---

### Step 2: 生成候选假设

- 基于领域知识和类比经验，列出所有可能解释该观察的原因
- 鼓励发散，至少 3 个假设，避免过早锁定
- 每个假设用一句话说明核心逻辑

---

### Step 3: 评估解释力

- 对每个假设，检查其能否预测观察结果，以及是否有反证
- 使用标准：覆盖度（能解释多少观察）、简洁性（是否符合奥卡姆剃刀）、一致性（是否与已有知识矛盾）
- 保持客观，避免确认偏误

---

### Step 4: 选择最佳解释

- 选择评分最高的假设
- 若有两个等分，则根据上下文（风险偏好、验证成本）和用户偏好决定
- 明确备选假设，以防首选被证伪

---

### Step 5: 生成验证方案

- 设计一组可执行的验证步骤
- 确保方案能够确认或否定该假设
- 明确什么结果支持假设，什么结果否定假设

---

### Step 6: 输出结论与信度

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **最佳解释优先**：选择解释力最强、最连贯的假设，而非任意假设。原因：溯因的核心是"最佳解释"，不是概率最大或最简单（但简洁是加分项）。
2. **假设开放**：鼓励产生多种不同方向的假设，防止过早锁定。原因：人类认知倾向于确认偏误，开放假设是唯一对抗手段。
3. **可证伪性基础**：假设必须能被事实推翻，否则不是科学解释。原因：不可证伪的假设应被排除，因为它们无法指导验证。
4. **知识驱动**：利用领域知识缩小因果空间。原因：没有专业知识，溯因会退化为随机猜测。
5. **迭代验证**：结论不是终点，验证才能确认或推翻假设。原因：溯因产生的是暂时性解释，必须经过验证才能成为可靠知识。

---

## 自检清单

> 聚焦溯因思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**溯因思维特有关键检查项**：

- [ ] **是否生成了至少3个不同的候选假设？** 还是过早锁定到单一解释？
- [ ] **每个假设是否都是可证伪的？** 是否存在无法被任何观察推翻的"万能解释"？
- [ ] **是否用覆盖度、简洁性、一致性三个标准评估了解释力？** 而非仅凭直觉选择"最合理"的？
- [ ] **是否设计了明确的验证方案？** 验证结果能否真正区分各假设的真伪？
- [ ] **是否区分了"最佳解释"与"最希望为真的解释"？** 情感偏好是否影响了假设选择？
- [ ] **是否考虑了替代假设被证伪后的备选方案？** 首选假设被推翻时是否有退路？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [deductive-thinking](../thinking/deductive-thinking/SKILL.md) | 互补 | 当需要从选定假设推导可验证的预测时 |
| [inductive-thinking](../thinking/inductive-thinking/SKILL.md) | 对比 | 当需要从大量历史案例中提取一般规律来辅助生成假设时 |
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 当观察结果涉及复杂系统的多个相互作用部分时 |
| [first-principles](../thinking/first-principles/SKILL.md) | 后置 | 当评估假设的合理性遇到知识盲区时 |

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

1. Peirce, C. S. (1903). *Lectures on Pragmatism*. Harvard University.
2. Magnani, L. (2001). *Abduction, Reason, and Science: Processes of Discovery and Explanation*. Kluwer Academic Press.
3. Josephson, J. R., & Josephson, S. G. (1994). *Abductive Inference: Computation, Philosophy, Technology*. Cambridge University Press.
4. Flach, P., & Kakas, A. (2000). *Abduction and Induction: Essays on Their Relation and Integration*. Kluwer Academic Publishers.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
