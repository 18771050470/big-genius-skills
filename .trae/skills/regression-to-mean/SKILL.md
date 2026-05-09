---
name: regression-to-mean
description: |
  触发：当需要评估极端表现后是否预期回归平均、需要识别将随机波动误认为因果效应、需要分析绩效变化时调用；常见信号包括"上次考这么好这次肯定不行"、"惩罚/奖励后表现变了"、"这次太差下次肯定好转"。
  不触发：当只需描述单次事件、无需预测趋势时；当有明确因果机制解释变化时；当样本量过小无法计算平均时。
  Invoke when needing to evaluate whether to expect regression to average after extreme performance, identify misattribution of random fluctuations to causal effects, or analyze performance changes.
  Do NOT invoke when only describing single events without predicting trends, when clear causal mechanisms explain changes, or when sample size is too small to calculate average.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["probabilistic-thinking", "pattern-recognition-thinking", "causal-thinking", "statistical-thinking"]
---

# 回归均值思维（Regression to the Mean Thinking）

## 核心定义

极端表现后倾向于回归平均水平。Galton在1886年发现：极高父母的孩子倾向于比父母矮，极矮父母的孩子倾向于比父母高。极端表现往往包含运气成分，运气不可持续，后续表现回归平均。误将回归均值归因为干预效果是常见错误。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充历史表现数据、样本量和随机因素评估
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别回归均值影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别极端表现

- 当前表现是否极端（远高于或低于平均）？
- 极端程度是多少？（标准差倍数）
- 历史表现数据是什么？平均表现是多少？
- 样本量是否足够判断极端性？

---

### Step 2: 评估运气成分

- 表现中多少是技能，多少是运气？
- 随机因素对结果的影响程度？
- 如果重复同样条件，结果会相似吗？
- 运气是否可能持续？

---

### Step 3: 预测回归趋势

- 极端表现后，下次表现预期更接近平均
- 回归幅度：极端程度越大，回归幅度越大
- 计算预期回归值：平均 + (当前偏离 × 回归系数)
- 回归系数通常0.3-0.7（取决于技能/运气比例）

---

### Step 4: 区分因果与回归

- 干预后表现改善：是干预效果还是回归均值？
- 使用对照组：未干预组是否也回归平均？
- 多次测量：单次测量可能回归，多次测量看趋势
- 避免将回归误认为因果效应

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **极端包含运气**：任何极端表现都包含技能和运气，运气不可持续。原因：随机波动必然回归平均，这是统计规律而非因果效应。
2. **回归是统计必然**：极端值后跟随更接近平均的值，这是数学规律。原因：测量误差和随机因素使单次观测偏离真实值，后续观测更接近真实值。
3. **干预效果需对照验证**：没有对照组，无法区分干预效果和回归均值。原因：极端表现后自然回归，任何干预都会"看起来有效"。
4. **多次测量看趋势**：单次测量可能误导，多次测量揭示真实趋势。原因：多次测量平均掉随机波动，更接近真实能力水平。

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
- [ ] 是否识别了极端表现？
- [ ] 是否评估了运气成分？
- [ ] 是否预测了回归趋势？
- [ ] 是否区分了因果与回归？
- [ ] 是否使用对照组验证？
- [ ] 输出具体可执行，不含模糊建议（如"会回归"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供随机波动概念框架 |
| [pattern-recognition-thinking](../thinking/pattern-recognition-thinking/SKILL.md) | 并行 | 模式识别可能误将回归认为趋势 |
| [causal-thinking](../thinking/causal-thinking/SKILL.md) | 并行 | 因果思维帮助区分真实因果和回归 |
| [statistical-thinking](../thinking/statistical-thinking/SKILL.md) | 前置 | 统计思维提供回归均值的数学基础 |

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

1. Galton, F. (1886). Regression towards mediocrity in hereditary stature. *Journal of the Anthropological Institute*, 15, 246-263.
2. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 17: Regression to the Mean)
3. Barnett, A. G., et al. (2005). Regression to the mean: What it is and how to deal with it. *International Journal of Epidemiology*, 34(1), 215-220.
4. Morton, V., & Torgerson, D. J. (2003). Effect of regression to the mean on decision making in health care. *BMJ*, 326(7398), 1083-1084.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
