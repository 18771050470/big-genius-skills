---
name: reference-class-forecasting
description: |
  触发：当需要基于同类项目历史数据校准预测、需要使用外部视角估算时间和成本、需要纠正内部视角偏差时调用；常见信号包括"这个项目需要多久"、"类似项目花了多少"、"行业平均是多少"。
  不触发：当项目完全新颖、无同类参考时；当只需粗略估算、无需精确校准时；当有详细历史数据支持估算时（已使用此方法）。
  Invoke when needing to calibrate predictions based on historical data of similar projects, use outside view for time and cost estimation, or correct inside view bias.
  Do NOT invoke when the project is completely novel without similar reference, when only rough estimates are needed without precise calibration, or when detailed historical data supports estimation (already using this method).
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["planning-fallacy", "base-rate-fallacy", "bayesian-updating", "statistical-thinking"]
---

# 参考类别预测思维（Reference Class Forecasting Thinking）

## 核心定义

使用同类项目的历史数据（外部视角）校准当前项目预测，而非仅基于当前计划细节（内部视角）。Kahneman和Tversky在1979年提出，Flyvbjerg在2006年应用于大型项目管理：参考类别预测是纠正规划谬误最有效的方法。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充同类项目历史数据、项目特征匹配度和行业基准
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别参考类别预测方法且应用方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 定义参考类别

- 什么项目与当前项目类似？（规模、复杂度、技术栈、团队）
- 参考类别的边界是什么？（太宽=不相关，太窄=样本不足）
- 需要多少样本量？（至少10-30个同类项目）
- 数据来源是否可靠？

---

### Step 2: 收集历史数据

- 同类项目的实际耗时分布（平均值、中位数、标准差）
- 同类项目的成本超支比例
- 同类项目的风险发生率
- 最佳情况、最可能情况、最坏情况

---

### Step 3: 匹配当前项目

- 当前项目与参考类别的相似度？
- 哪些因素使当前项目不同于平均？（更复杂/更简单）
- 调整系数：基于差异调整预测
- 计算：参考类别平均 × 调整系数 = 校准预测

---

### Step 4: 整合内外视角

- 内部视角：基于当前计划的估算
- 外部视角：基于参考类别的估算
- 贝叶斯整合：外部视角为先验，内部视角为证据
- 最终预测 = 外部视角 + (内部视角 - 外部视角) × 权重

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **外部视角优于内部视角**：同类项目历史数据比当前计划更可靠。原因：历史数据包含所有意外和风险，反映真实情况；内部视角忽略未知未知。
2. **参考类别定义是关键**：太宽不相关，太窄样本不足。原因：参考类别必须平衡相关性和样本量，找到最佳匹配。
3. **调整必须有依据**：基于具体差异调整预测，而非直觉。原因：无依据调整引入新偏差，抵消外部视角优势。
4. **贝叶斯整合最优**：外部视角为先验，内部视角为证据。原因：贝叶斯框架数学上最优整合两种信息源。

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
- [ ] 是否正确定义了参考类别？
- [ ] 是否收集了足够历史数据（≥10样本）？
- [ ] 是否评估了当前项目与参考类别的相似度？
- [ ] 是否使用贝叶斯整合内外视角？
- [ ] 调整是否有具体依据？
- [ ] 输出具体可执行，不含模糊建议（如"参考历史"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [planning-fallacy](../thinking/planning-fallacy/SKILL.md) | 前置 | 规划谬误解释为何需要外部视角 |
| [base-rate-fallacy](../thinking/base-rate-fallacy/SKILL.md) | 前置 | 基础概率谬误解释为何忽视历史数据 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 贝叶斯更新提供内外视角整合框架 |
| [statistical-thinking](../thinking/statistical-thinking/SKILL.md) | 前置 | 统计思维提供数据收集和分析方法 |

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
2. Flyvbjerg, B. (2006). From Nobel Prize to project management: Getting risks right. *Project Management Journal*, 37(3), 5-15.
3. Lovallo, D., & Kahneman, D. (2003). Delusions of success: How optimism undermines executives' decisions. *Harvard Business Review*, 81(7), 56-63.
4. Buehler, R., Griffin, D., & Ross, M. (1994). Exploring the "planning fallacy": Why people underestimate their task completion times. *Journal of Personality and Social Psychology*, 67(3), 366-381.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
