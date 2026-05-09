---
name: growth-mindset
description: |
  触发：当需要评估能力发展可能性、需要识别固定型思维陷阱、需要设计学习/改进策略时调用；常见信号包括"我天生不擅长这个"、"失败了说明我不行"、"已经够好了不用改"。
  不触发：当只需描述当前能力水平、无需评估成长潜力时；当涉及生理极限或不可改变的身体条件时；当只需记录失败、无需分析学习机会时。
  Invoke when needing to evaluate ability development potential, identify fixed-mindset traps, or design learning/improvement strategies.
  Do NOT invoke when only describing current ability level without evaluating growth potential, when involving physiological limits or unchangeable physical conditions, or when only recording failures without analyzing learning opportunities.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["fixed-mindset", "effort-justification", "feedback-loop", "self-efficacy"]
---

# 成长型思维（Growth Mindset Thinking）

## 核心定义

能力可以通过努力、学习和策略调整而发展，而非固定不变。Carol Dweck 在 2006 年提出：固定型思维者相信能力天生注定，成长型思维者相信能力可以培养。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充当前能力基线、学习资源可用性和时间约束
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别固定型思维陷阱且成长策略清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别思维模式信号

- 是否出现"我天生不擅长这个"、"失败了说明我不行"、"已经够好了不用改"等表述？
- 是否将失败归因于能力而非努力或策略？
- 是否回避挑战以避免暴露不足？
- 是否对反馈感到威胁而非机会？

---

### Step 2: 评估能力可塑性

- 该能力是否可通过练习提升？（技能 vs 天赋）
- 当前水平与目标水平的差距？
- 需要多长时间的学习曲线？
- 是否存在有效的学习路径和方法？

---

### Step 3: 分析固定型思维机制

- 能力实体观：认为能力是固定实体，非增即减
- 表现目标导向：追求证明能力，回避可能失败的任务
- 努力悖论：认为需要努力说明能力不足
- 失败定义：将失败视为能力不足的证明

---

### Step 4: 设计成长策略

- 设定学习目标：关注进步而非证明
- 设计刻意练习：聚焦薄弱环节，获取即时反馈
- 建立过程评价：奖励努力和策略，而非仅结果
- 重构失败：将失败视为学习数据而非能力判决

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **能力可塑**：大多数能力可通过刻意练习提升。原因：神经可塑性证明大脑结构和功能可随经验改变，技能学习是神经连接重组的过程。
2. **努力是路径**：需要努力不代表能力不足，而是能力正在构建。原因：成长型思维将努力视为发展信号，固定型思维将努力视为能力不足的证明。
3. **失败是数据**：失败提供关于策略有效性的信息，而非关于能力的天判决。原因：将失败重新定义为学习机会，维持动机并促进策略调整。
4. **过程优先**：关注学习过程和策略改进，而非仅关注结果表现。原因：过程导向维持长期动机，结果导向导致回避挑战和过早放弃。

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

**成长型思维特有关键检查项**：

- [ ] **成长型思维特供**：是否识别了固定型思维信号？是否出现能力实体观的表述？
- [ ] **成长型思维特供**：是否评估了能力的可塑性？该能力是否属于可通过练习提升的技能？
- [ ] **成长型思维特供**：是否分析了固定型思维的驱动机制？表现目标导向、努力悖论是否被识别？
- [ ] **成长型思维特供**：是否设计了刻意练习策略？练习是否聚焦薄弱环节并包含即时反馈？
- [ ] **成长型思维特供**：是否重构了失败的意义？失败是否被定义为学习数据而非能力判决？
- [ ] **成长型思维特供**：是否区分了天赋型任务和努力型任务？是否避免了"天赋决定论"的隐含假设？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"努力一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [effort-justification](../thinking/effort-justification/SKILL.md) | 并行 | 努力正当化解释为何投入后更坚持，成长型思维解释为何投入能提升能力 |
| [feedback-loop](../thinking/feedback-loop/SKILL.md) | 前置 | 反馈回路提供刻意练习的即时反馈机制 |
| [self-efficacy](../thinking/self-efficacy/SKILL.md) | 并行 | 自我效能感影响对能力的信念，成长型思维重塑这种信念 |
| [fixed-mindset](../thinking/fixed-mindset/SKILL.md) | 对立 | 固定型思维是成长型思维的对立面，识别固定型思维是应用成长型思维的前提 |

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

1. Dweck, C. S. (2006). *Mindset: The New Psychology of Success*. Random House.
2. Dweck, C. S., & Leggett, E. L. (1988). A social-cognitive approach to motivation and personality. *Psychological Review*, 95(2), 256-273.
3. Blackwell, L. S., Trzesniewski, K. H., & Dweck, C. S. (2007). Implicit theories of intelligence predict achievement across an adolescent transition: A longitudinal study and an intervention. *Child Development*, 78(1), 246-263.
4. Yeager, D. S., et al. (2019). A national experiment reveals where a growth mindset improves achievement. *Nature*, 573(7774), 364-369.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
