---
name: narrative-thinking
description: |
  触发：当需要评估解释是否受叙事谬误影响、需要识别过度简化的因果故事、需要区分相关性和因果性时调用；常见信号包括"这就是原因"、"故事是这样的"、"一切都有规律"。
  不触发：当因果关系已被实验验证时；当只需讲述故事、无需评估解释准确性时；当叙事仅用于沟通、不用于决策时。
  Invoke when needing to evaluate whether explanations are affected by narrative fallacy, identify oversimplified causal stories, or distinguish correlation from causation.
  Do NOT invoke when causality has been experimentally verified, when only telling stories without evaluating explanation accuracy, or when narrative is only used for communication not decision-making.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["confirmation-bias", "hindsight-bias", "causal-thinking", "probabilistic-thinking"]
---

# 叙事思维（Narrative Thinking）

## 核心定义

人们倾向于将复杂事件编织成简单、连贯的因果故事，即使实际因果关系不存在或更复杂。Taleb提出"叙事谬误"：人类大脑偏好故事而非数据，因为故事更容易理解和记忆。好故事不等于真解释，连贯性不等于准确性。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充原始数据、替代解释和反例证据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别叙事谬误影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别叙事结构

- 当前解释是否呈现为连贯故事？
- 故事是否有清晰的起因、经过、结果？
- 故事是否过于完美、没有例外？
- 故事是否将随机事件解释为必然结果？

---

### Step 2: 评估叙事谬误

- 故事是否忽略了随机性和噪音？
- 是否将相关性误认为因果性？
- 是否选择了支持性证据，忽视反例？
- 故事是否因为"听起来合理"而被接受？

---

### Step 3: 寻找替代解释

- 同一事件能否用不同故事解释？
- 随机性是否能解释观察到的模式？
- 是否有更简单的解释（奥卡姆剃刀）？
- 反例是否存在？是否被合理解释？

---

### Step 4: 验证因果关系

- 因果机制是否可检验？
- 是否有控制实验或自然实验支持？
- 因果方向是否确定？（A→B还是B→A？）
- 是否有混淆变量未被控制？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **好故事≠真解释**：故事连贯性来自叙事技巧，而非事实准确性。原因：人类大脑偏好模式识别，即使模式不存在也会"看到"模式。
2. **随机性被低估**：大多数"模式"是随机波动的产物。原因：小样本中随机性产生看似有意义的模式，人们误认为规律。
3. **因果≠相关**：两个变量相关不等于一个导致另一个。原因：可能有共同原因、反向因果或纯粹巧合。
4. **反例是故事杀手**：一个可靠反例足以推翻完美故事。原因：科学方法通过证伪而非证实推进知识。

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
- [ ] 是否识别了叙事结构和叙事谬误信号？
- [ ] 是否考虑了随机性的作用？
- [ ] 是否区分了相关性和因果性？
- [ ] 是否寻找了替代解释和反例？
- [ ] 因果机制是否可检验？
- [ ] 输出具体可执行，不含模糊建议（如"客观看待"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误选择性回忆支持叙事的证据 |
| [hindsight-bias](../thinking/hindsight-bias/SKILL.md) | 并行 | 后见之明使叙事看起来更必然 |
| [causal-thinking](../thinking/causal-thinking/SKILL.md) | 前置 | 因果思维提供验证因果关系的方法 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维评估随机性解释的可能性 |

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

1. Taleb, N. N. (2007). *The Black Swan: The Impact of the Highly Improbable*. Random House.
2. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 14: Tom W's Specialty)
3. Tetlock, P. E., & Gardner, D. (2015). *Superforecasting: The Art and Science of Prediction*. Crown.
4. Fischhoff, B. (1975). Hindsight ≠ foresight: The effect of outcome knowledge on judgment under uncertainty. *Journal of Experimental Psychology: Human Perception and Performance*, 1(3), 288-299.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
