---
name: anchoring-adjustment
description: |
  触发：当需要评估判断是否受初始锚点影响、需要识别锚定效应、需要校正数值估计时调用；常见信号包括"从X开始调整"、"大概X左右"、"先猜一个数再调整"。
  不触发：当只需描述初始值、无需评估调整充分性时；当锚点确实提供有效信息时（经数据验证）；当只需定性排序、无需精确数值估计时。
  Invoke when needing to evaluate whether judgments are affected by initial anchors, identify anchoring effect, or correct numerical estimates.
  Do NOT invoke when only describing initial values without evaluating adjustment sufficiency, when anchors truly provide valid information (verified by data), or when only qualitative ranking is needed without precise numerical estimation.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["anchoring-effect", "availability-bias", "overconfidence-effect", "regression-to-mean"]
---

# 锚定调整思维（Anchoring and Adjustment Thinking）

## 核心定义

人们从初始锚点开始调整，但调整不足。Tversky和Kahneman在1974年证明：锚点显著影响最终估计，即使锚点明显随机。调整过程过早停止，导致估计偏向锚点。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充锚点来源、调整依据和历史估计数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别锚定影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别锚点

- 初始锚点是什么？（数字、建议、第一印象）
- 锚点来源是否相关？（专家意见 vs 随机数字）
- 锚点是否被有意设置？（谈判策略、营销手段）
- 锚点对估计的影响程度？

---

### Step 2: 评估调整过程

- 从锚点调整了多少？
- 调整方向是否正确？（远离锚点）
- 调整幅度是否充分？（通常不足）
- 调整停止过早？（锚点仍影响最终估计）

---

### Step 3: 分析锚定机制

- 锚点作为起点：估计=锚点+调整
- 调整不足原因：锚点太强烈，调整需要认知努力
- 确认偏误：寻找支持锚点的证据
- 锚点可及性：锚点激活相关记忆，影响估计

---

### Step 4: 校正锚定偏差

- 使用外部视角：同类项目的历史数据
- 多锚点平均：使用多个不同锚点
- 反锚点思考：从相反方向开始估计
- 设计决策检查清单：锚点≠真实值

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **锚点影响持久**：即使知道锚点随机，仍被影响。原因：锚点自动激活相关记忆和知识，调整需要认知努力，系统2懒惰。
2. **调整不足普遍**：人们从锚点调整，但调整幅度不足。原因：调整是逐步过程，人们在"足够接近"时停止，而非"正确"时停止。
3. **多锚点优于单锚点**：使用多个不同锚点减少单一锚点影响。原因：多锚点平均化，减少单一锚点的极端影响。
4. **外部视角是解药**：使用同类项目历史数据替代锚点调整。原因：历史数据提供客观基准，不受锚点影响。

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
- [ ] **锚定调整特供**：是否明确识别了初始锚点（数字、建议、第一印象）？锚点来源是否被追溯？
- [ ] **锚定调整特供**：是否评估了调整幅度和充分性？调整是否过早停止？
- [ ] **锚定调整特供**：是否分析了锚定机制（选择性可及性、确认偏误、认知吝啬）？
- [ ] **锚定调整特供**：是否使用了多锚点平均或外部视角进行校正？单一锚点是否被依赖？
- [ ] **锚定调整特供**：是否实施了反锚点思考？从相反方向开始估计是否能大幅改变结果？
- [ ] **锚定调整特供**：是否区分了"有效锚点"（经数据验证）和"随机锚点"？有效锚点不应被过度校正
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"避免锚定"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [anchoring-effect](../thinking/anchoring-effect/SKILL.md) | 并行 | 锚定效应是锚定调整的基础理论 |
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差使生动信息成为锚点 |
| [overconfidence-effect](../thinking/overconfidence-effect/SKILL.md) | 并行 | 过度自信使调整过早停止 |
| [regression-to-mean](../thinking/regression-to-mean/SKILL.md) | 并行 | 回归均值提供外部视角基准 |

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

1. Tversky, A., & Kahneman, D. (1974). Judgment under uncertainty: Heuristics and biases. *Science*, 185(4157), 1124-1131.
2. Epley, N., & Gilovich, T. (2006). The anchoring-and-adjustment heuristic: Why the adjustments are insufficient. *Psychological Science*, 17(4), 311-318.
3. Mussweiler, T., & Strack, F. (1999). Hypothesis-consistent testing and semantic priming in the anchoring paradigm: A selective accessibility model. *Journal of Experimental Social Psychology*, 35(2), 136-164.
4. Furnham, A., & Boo, H. C. (2011). A literature review of the anchoring effect. *The Journal of Socio-Economics*, 40(1), 35-42.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
