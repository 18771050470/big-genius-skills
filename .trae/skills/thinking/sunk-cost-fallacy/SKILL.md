---
name: sunk-cost-fallacy
description: |
  触发：当需要评估是否因已投入资源而继续不合理行为、需要决定是否放弃已投入项目时调用；常见信号包括"已经投了这么多钱不能停"、"都做了这么多了放弃太可惜"、"再坚持一下"。
  不触发：当继续投入有明确正向预期回报时；当只需评估当前选项未来价值、无需考虑历史投入时；当沉没成本极小、不影响决策时。
  Invoke when needing to evaluate whether to continue unreasonable behavior due to invested resources, or needing to decide whether to abandon invested projects.
  Do NOT invoke when continued investment has clear positive expected returns, when only evaluating future value of current options without considering historical investment, or when sunk costs are minimal and do not affect decisions.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["loss-aversion", "opportunity-cost", "confirmation-bias", "bayesian-updating"]
---

# 沉没成本谬误思维（Sunk Cost Fallacy Thinking）

## 核心定义

人们倾向于因为已经投入的时间、金钱或努力而继续一个不合理的行为，即使未来预期回报为负。Arkes和Blumer在1985年通过实验首次证明：一旦在金钱、努力或时间上进行了投资，人们就会非理性地坚持原有选择。理性决策应该只考虑未来成本和收益，而非历史投入。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充项目未来预期回报、替代选项价值和已投入资源明细
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确沉没成本影响且放弃/继续决策清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别沉没成本

- 已经投入的资源有哪些？（时间、金钱、努力、声誉）
- 这些投入是否可回收？不可回收的部分就是沉没成本
- 区分沉没成本和未来成本：沉没成本是历史投入，未来成本是继续所需的额外投入
- 标注沉没成本金额和占比

---

### Step 2: 评估未来预期回报

- 如果继续投入，未来预期收益是多少？
- 如果现在放弃，可回收的资源有多少？
- 如果将资源投入替代选项，预期收益是多少？
- 计算继续的净现值（NPV）：未来收益 - 未来成本

---

### Step 3: 识别沉没成本谬误

- 决策是否受到已投入资源的影响？
- 如果从未投入过，基于当前信息还会做这个决定吗？
- 是否出现"已经投了这么多不能停"、"放弃太可惜"等表述？
- 是否将沉没成本纳入决策考量？（理性决策不应考虑沉没成本）

---

### Step 4: 设计理性决策框架

- 忽略沉没成本，只考虑未来成本和收益
- 比较继续 vs 放弃 vs 转向的预期收益
- 计算机会成本：继续投入意味着放弃的替代选项价值
- 设定退出标准：什么情况下必须放弃？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **沉没成本不是成本**：经济学定义，沉没成本是已经发生且不可回收的成本，不应影响未来决策。原因：未来决策只应考虑未来成本和收益，历史投入与未来无关。
2. **"已经投入"是陷阱**：Arkes和Blumer实验证明，投入越多越难放弃，即使继续投入预期亏损。原因：损失厌恶和心理账户使人们将沉没成本视为"损失"，不愿承认失败。
3. **机会成本才是真实成本**：继续投入意味着放弃替代选项的价值。原因：资源有限，投入A就不能投入B，B的预期收益是继续A的真实成本。
4. **退出标准必须事前设定**：在投入前设定退出条件，避免被沉没成本绑架。原因：事前没有沉没成本偏见，能更客观设定退出标准。

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
- [ ] 沉没成本是否被准确识别和量化？
- [ ] 未来预期回报是否被独立评估（不考虑沉没成本）？
- [ ] 是否识别了沉没成本谬误信号？
- [ ] 机会成本是否被计算？
- [ ] 是否设定了退出标准？
- [ ] 输出具体可执行，不含模糊建议（如"理性决策"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [loss-aversion](../thinking/loss-aversion/SKILL.md) | 前置 | 损失厌恶是沉没成本谬误的心理根源 |
| [opportunity-cost](../thinking/opportunity-cost/SKILL.md) | 并行 | 机会成本评估继续投入的真实代价 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误寻找支持继续的证据，忽视放弃信号 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 贝叶斯更新根据新信息调整预期，对抗沉没成本偏见 |

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

1. Arkes, H. R., & Blumer, C. (1985). The psychology of sunk cost. *Organizational Behavior and Human Decision Processes*, 35(1), 124-140.
2. Kahneman, D., & Tversky, A. (1979). Prospect theory: An analysis of decision under risk. *Econometrica*, 47(2), 263-291.
3. Thaler, R. H. (1980). Toward a positive theory of consumer choice. *Journal of Economic Behavior & Organization*, 1(1), 39-60.
4. Staw, B. M. (1976). Knee-deep in the big muddy: A study of escalating commitment to a chosen course of action. *Organizational Behavior and Human Performance*, 16(1), 27-44.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
