---
name: prospect-theory
description: |
  触发：当需要评估风险决策是否受参照点影响、需要识别损失厌恶和概率加权偏差、需要分析框架效应时调用；常见信号包括"亏了不敢卖"、"赚了赶紧跑"、"这个参照点不公平"。
  不触发：当只需描述风险偏好、无需分析参照点影响时；当决策确实基于最终财富而非变化时（经效用函数验证）；当只需定性比较选项、无需量化分析时。
  Invoke when needing to evaluate whether risk decisions are affected by reference points, identify loss aversion and probability weighting bias, or analyze framing effects.
  Do NOT invoke when only describing risk preferences without analyzing reference point impact, when decisions are truly based on final wealth rather than changes (verified by utility function), or when only qualitatively comparing options without quantitative analysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["loss-aversion", "framing-effect", "endowment-effect", "zero-risk-bias"]
---

# 前景理论思维（Prospect Theory Thinking）

## 核心定义

人们基于参照点评估收益和损失，而非最终财富。Kahneman和Tversky在1979年提出：损失厌恶（损失感觉比等量收益强2倍）、确定性偏好（确定性结果被过度加权）、参照点依赖（评估基于变化而非绝对水平）。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充参照点、损失厌恶系数和风险偏好数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别前景理论影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别参照点

- 决策的参照点是什么？（现状、期望、他人）
- 选项如何被框架为收益或损失？
- 参照点变化如何改变偏好？
- 是否存在框架效应？

---

### Step 2: 评估损失厌恶

- 损失厌恶系数是多少？（通常约2.0）
- 损失框架下是否更风险寻求？
- 收益框架下是否更风险规避？
- 处置效应：持有亏损、卖出盈利？

---

### Step 3: 分析概率加权

- 小概率是否被过度加权？（彩票、保险）
- 中等概率是否被低估？
- 确定性是否被过度偏好？
- 概率加权函数形状？

---

### Step 4: 校正偏差

- 重新框架：从最终财富角度评估
- 使用期望值计算替代直觉
- 识别参照点操纵
- 设计决策检查清单：框架≠实质

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **参照点决定感知**：人们感知收益和损失，而非最终财富。原因：大脑适应参照点，变化比绝对水平更容易感知。
2. **损失厌恶普遍**：损失感觉比等量收益强约2倍。原因：进化使避免损失比获取收益更重要，损失激活更强神经反应。
3. **概率加权非线性**：小概率被高估，中等概率被低估，确定性被过度偏好。原因：情感系统对确定性和可能性反应强烈，对概率不敏感。
4. **框架效应强大**：相同问题不同框架导致不同选择。原因：框架改变参照点和收益/损失感知，触发不同心理账户。

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
- [ ] 是否识别了参照点？
- [ ] 是否评估了损失厌恶系数？
- [ ] 是否分析了概率加权偏差？
- [ ] 是否识别了框架效应？
- [ ] 是否设计了校正方案？
- [ ] 输出具体可执行，不含模糊建议（如"避免损失厌恶"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 前置 | 损失厌恶是前景理论的核心组成部分 |
| [framing-effect](../thinking/framing-effect/SKILL.md) | 并行 | 框架效应改变参照点和收益/损失感知 |
| [endowment-effect](../thinking/endowment-effect/SKILL.md) | 并行 | 禀赋效应是损失厌恶的表现形式 |
| [zero-risk-bias](../thinking/zero-risk-bias/SKILL.md) | 并行 | 零风险偏差是确定性偏好的表现 |

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

1. Kahneman, D., & Tversky, A. (1979). Prospect theory: An analysis of decision under risk. *Econometrica*, 47(2), 263-291.
2. Tversky, A., & Kahneman, D. (1992). Advances in prospect theory: Cumulative representation of uncertainty. *Journal of Risk and Uncertainty*, 5(4), 297-323.
3. Thaler, R. H. (2015). *Misbehaving: The Making of Behavioral Economics*. W. W. Norton & Company.
4. Barberis, N. C. (2013). Thirty years of prospect theory in economics: A review and assessment. *Journal of Economic Perspectives*, 27(1), 173-196.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
