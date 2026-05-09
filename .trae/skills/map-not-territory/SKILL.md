---
name: map-not-territory
description: |
  触发：当过度依赖模型/理论做决策、将指标当作目标、混淆抽象和现实时调用；常见信号包括"模型说一定对"、"数据好就是真的好"、"按理论应该这样"。
  不触发：当仅需使用模型做工具、不涉及模型与现实混淆风险、不需要评估模型局限性时，不要调用此 Skill。
  Invoke when over-relying on models, confusing metrics with reality, or mistaking abstractions for reality.
  Do NOT invoke when simply using models as tools without reality confusion risk.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["abstract-thinking", "model-thinking", "critical-thinking"]
---

# 地图不是疆域思维

## 核心定义

模型/理论只是现实的简化表示，不要把模型和现实混为一谈。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充现实数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告模型与现实的矛盾点
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别模型依赖

- 要点1：识别当前决策基于什么模型/理论/指标（如KPI、用户画像、架构模型）
- 要点2：评估模型的简化程度（省略了什么现实复杂性）
- 要点3：注意模型创建时的假设和边界条件是否仍适用

---

### Step 2: 评估模型-现实差距

- 要点1：对比模型预测和实际观察的差异
- 要点2：识别模型未覆盖的现实因素（如人的行为复杂性、环境变化）
- 要点3：保持客观，避免确认偏误（只找支持模型的证据）

---

### Step 3: 分析模型局限

- 要点1：明确模型的适用范围和失效边界
- 要点2：评估过度依赖模型的风险（如Goodhart定律：指标变目标后失效）
- 要点3：标注模型结论的置信度，标注反证可能性

---

### Step 4: 校正模型偏差

- 要点1：用现实数据校准模型，而非用模型裁剪现实
- 要点2：建立模型更新机制，定期验证模型有效性
- 要点3：保留对模型说不的勇气，当现实与模型冲突时相信现实

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步

---

## 关键原则

1. **模型是工具不是真理**：说明。原因：所有模型都是错的，但有些是有用的（George Box）。模型的价值在于实用性而非绝对正确。
2. **现实优先于模型**：说明。原因：当模型预测与现实冲突时，现实永远是对的，模型需要修正。
3. **模型需要定期校准**：说明。原因：环境变化使模型过时，不校准的模型会产生系统性偏差。

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
| [model-thinking](../thinking/model-thinking/SKILL.md) | 前置 | 先理解模型的作用 |
| [critical-thinking](../thinking/critical-thinking/SKILL.md) | 并行 | 质疑模型假设 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 后置 | 用新证据校准模型 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Korzybski, A. (1933). *Science and Sanity: An Introduction to Non-Aristotelian Systems and General Semantics*. International Non-Aristotelian Library.
2. Box, G. E. P. (1976). "Science and Statistics". *Journal of the American Statistical Association*, 71(356), 791-799.
3. Goodhart, C. A. (1984). "Problems of Monetary Management: The UK Experience". In *Inflation, Depression, and Economic Policy in the Postwar Era*.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
