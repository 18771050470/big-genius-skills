---
name: planning-fallacy
description: |
  触发：当需要评估项目计划是否过于乐观、需要校准时间和成本估算、需要识别规划谬误时调用；常见信号包括"这个项目很快就能完成"、"我们之前做过类似的"、"这次不会遇到什么问题"。
  不触发：当有详细历史数据支持估算时；当只需粗略估算、无需精确校准时；当项目完全新颖、无历史参考时。
  Invoke when needing to evaluate whether project plans are overly optimistic, calibrate time and cost estimates, or identify planning fallacy.
  Do NOT invoke when detailed historical data supports estimates, when only rough estimates are needed without precise calibration, or when the project is completely novel without historical reference.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["overconfidence-effect", "base-rate-fallacy", "reference-class-forecasting", "bayesian-updating"]
---

# 规划谬误思维（Planning Fallacy Thinking）

## 核心定义

人们倾向于低估完成任务所需的时间、成本和风险，即使有历史经验表明应该更久。Kahneman和Tversky在1979年提出：规划者采用内部视角（关注当前计划细节），忽视外部视角（同类项目实际耗时）。Buehler等在1994年证明：学生估计论文完成时间平均比实际少30%。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充历史项目数据、同类项目平均耗时和风险清单
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别规划谬误影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别规划谬误信号

- 是否出现"这个项目很快就能完成"、"我们之前做过类似的"等表述？
- 估算是否基于乐观假设？
- 是否考虑了意外情况和风险？
- 历史项目实际耗时 vs 计划耗时？

---

### Step 2: 获取外部视角

- 同类项目平均耗时是多少？（参考类别预测）
- 同类项目平均超支比例是多少？
- 历史数据分布：最佳情况、最可能情况、最坏情况
- 当前项目与同类项目的相似度？

---

### Step 3: 分解任务估算

- 将项目分解为可估算的子任务
- 每个子任务使用三点估算：乐观、最可能、悲观
- 计算期望值：(乐观 + 4×最可能 + 悲观) / 6
- 汇总子任务估算，而非整体估算

---

### Step 4: 添加缓冲和风险管理

- 根据历史超支比例添加缓冲（通常20-50%）
- 识别关键路径和瓶颈任务
- 制定风险应对计划：如果X发生，怎么办？
- 设置里程碑和检查点，持续校准估算

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **内部视角导致乐观**：关注当前计划细节会忽视历史教训。原因：大脑想象顺利完成的场景，不想象意外和阻碍。
2. **外部视角更准确**：同类项目实际数据比当前计划更可靠。原因：历史数据包含所有意外和风险，反映真实情况。
3. **分解估算优于整体估算**：子任务估算汇总比整体估算更准确。原因：分解迫使考虑更多细节和风险，减少乐观偏差。
4. **缓冲是必须不是可选**：根据历史超支比例添加缓冲。原因：规划谬误是系统性偏差，无缓冲必然超期。

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
- [ ] 是否识别了规划谬误信号？
- [ ] 是否获取了外部视角（同类项目数据）？
- [ ] 是否使用三点估算分解任务？
- [ ] 是否添加了缓冲（20-50%）？
- [ ] 是否识别了关键路径和风险？
- [ ] 输出具体可执行，不含模糊建议（如"留点缓冲"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [overconfidence-effect](../thinking/overconfidence-effect/SKILL.md) | 并行 | 过度自信导致乐观估算 |
| [base-rate-fallacy](../thinking/base-rate-fallacy/SKILL.md) | 前置 | 基础概率谬误解释为何忽视历史数据 |
| [reference-class-forecasting](../thinking/reference-class-forecasting/SKILL.md) | 前置 | 参考类别预测提供外部视角方法 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 贝叶斯更新根据里程碑数据校准估算 |

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

1. Kahneman, D., & Tversky, A. (1979). Intuitive prediction: Biases and corrective procedures. *TIMS Studies in Management Science*, 12, 313-327.
2. Buehler, R., Griffin, D., & Ross, M. (1994). Exploring the "planning fallacy": Why people underestimate their task completion times. *Journal of Personality and Social Psychology*, 67(3), 366-381.
3. Flyvbjerg, B. (2006). From Nobel Prize to project management: Getting risks right. *Project Management Journal*, 37(3), 5-15.
4. Lovallo, D., & Kahneman, D. (2003). Delusions of success: How optimism undermines executives' decisions. *Harvard Business Review*, 81(7), 56-63.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
