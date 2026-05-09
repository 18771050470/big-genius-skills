---
name: counterfactual-thinking
description: |
  触发：当需要评估决策质量、分析历史事件的替代可能性、理解因果关系时调用；常见信号包括"如果当初选了另一个方案会怎样"、"这个结果是因为决策好还是运气好"、"有没有其他可能导致同样结果"。
  不触发：当只需关注当前最优决策、无需回顾历史时；当反事实场景纯属臆想、无实际分析价值时；当时间极紧迫、只需向前看时。
  Invoke when evaluating decision quality, analyzing alternative possibilities of historical events, or understanding causal relationships.
  Do NOT invoke when only the current optimal decision matters without historical review, when counterfactual scenarios are pure speculation without analytical value, or when time is extremely tight and only forward-looking is needed.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["causal-thinking", "bayesian-updating", "hindsight-bias", "probabilistic-thinking"]
---

# 反事实思维（Counterfactual Thinking）

## 核心定义

通过构建"如果X没有发生/发生了会怎样"的替代场景，评估真实事件中的因果关系和决策质量，区分结果好坏与决策质量。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充历史事件的背景信息和决策时的可用信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若反事实分析已清晰区分运气与决策质量，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 锚定真实事件

- 明确实际发生的事件和结果
- 记录决策时的可用信息（不是事后才知道的信息）
- 标注决策时间点和结果时间点
- 区分决策质量和结果质量：好决策可能产生坏结果，坏决策可能产生好结果

---

### Step 2: 构建反事实场景

- 选择关键变量：如果改变哪个因素，结果会不同？
- 构建合理的替代场景：改变的因素必须在当时是可行的
- 避免"上帝视角"：只能用决策时已知的信息构建反事实
- 生成2-3个最可能的替代场景

---

### Step 3: 推演替代结果

- 对每个反事实场景，推演可能的结果分布
- 使用概率思维：反事实结果不是确定的，而是概率分布
- 比较真实结果与反事实结果的期望值
- 识别哪些结果差异来自运气，哪些来自决策

---

### Step 4: 提取学习

- 从反事实分析中提取可操作的教训
- 区分"决策过程错误"和"运气不好"
- 识别决策时的认知偏差（过度自信、确认偏误等）
- 形成决策改进清单：下次如何做得更好

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **区分决策质量与结果质量**：好结果不等于好决策。原因：运气在短期起决定作用，只有长期期望值才能评估决策质量。
2. **只用决策时信息**：反事实分析不能用事后才知道的信息。原因：用上帝视角评估历史决策会产生后见之明偏误。
3. **反事实必须合理**：替代场景必须在当时是可行的。原因：构建不可能的反事实（如"如果当时发明了时光机"）没有分析价值。
4. **关注可学习的教训**：反事实不是为了后悔，而是为了改进。原因：沉溺于"如果当初"会消耗精力，提取可操作教训才有价值。

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
- [ ] **反事实特供**：是否区分了决策质量和结果质量？好结果是否被误认为等于好决策？坏结果是否被误认为等于坏决策？
- [ ] **反事实特供**：反事实场景是否只用决策时信息构建？是否避免了"上帝视角"（使用事后才知道的信息）？
- [ ] **反事实特供**：反事实场景是否合理可行？替代场景是否在决策时确实可行？是否排除了不可能的反事实（如"如果发明了时光机"）？
- [ ] **反事实特供**：是否用概率分布而非确定值描述替代结果？反事实结果是否被量化为概率分布而非单一确定值？
- [ ] **反事实特供**：是否识别了运气 vs 决策的贡献比例？结果差异中多少来自运气，多少来自决策质量？是否形成了决策改进清单？
- [ ] 输出具体可执行，不含模糊建议（如"下次注意"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [causal-thinking](../thinking/causal-thinking/SKILL.md) | 前置 | 因果思维识别因果关系，反事实思维验证因果强度 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 后置 | 反事实分析后，用贝叶斯更新调整先验信念 |
| [hindsight-bias](../thinking/hindsight-bias/SKILL.md) | 并行 | 后见之明偏误是反事实分析需要警惕的陷阱 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维量化反事实结果的不确定性 |

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

1. Kahneman, D., & Tversky, A. (1982). The simulation heuristic. In *Judgment Under Uncertainty: Heuristics and Biases*. Cambridge University Press.
2. Roese, N. J. (1997). Counterfactual thinking. *Psychological Bulletin*, 121(1), 133-148.
3. Tetlock, P. E., & Gardner, D. (2015). *Superforecasting: The Art and Science of Prediction*. Crown.
4. Mauboussin, M. J. (2012). *The Success Equation: Untangling Skill and Luck in Business, Sports, and Investing*. Harvard Business Review Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
