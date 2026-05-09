---
name: identifiable-victim-effect
description: |
  触发：当需要评估决策是否受可识别个体影响、需要比较个体案例与统计数据的权重、需要识别"一个具体人胜过百万统计"偏差时调用；常见信号包括"救救这个孩子"、"想想那个具体的人"、"统计数据冷冰冰"。
  不触发：当只需讲述个体故事、无需资源分配决策时；当个体案例确实代表总体时（经统计验证）；当只需情感共鸣、无需理性分析时。
  Invoke when needing to evaluate whether decisions are affected by identifiable individuals, compare individual cases vs statistical data weight, or identify "one specific person outweighs millions of statistics" bias.
  Do NOT invoke when only telling individual stories without resource allocation decisions, when individual cases truly represent the population (statistically verified), or when only emotional resonance is needed without rational analysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["affect-heuristic", "availability-bias", "scope-neglect", "empathy-gap"]
---

# 可识别受害者效应思维（Identifiable Victim Effect Thinking）

## 核心定义

人们对可识别的具体个体的同情和帮助意愿远高于对统计意义上的群体。Schelling在1968年提出：一个具体、可识别的受害者比百万统计受害者更能激发行动。Small、Loewenstein和Slovic在2007年实验证明：人们为单个具体受害者捐赠远多于为统计群体捐赠。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充统计数据、总体规模和资源分配效率
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别可识别受害者效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别可识别信号

- 是否出现"救救这个孩子"、"想想那个具体的人"、"统计数据冷冰冰"等表述？
- 是否对具体个体的关注远高于统计群体？
- 是否因个体故事而忽视更大规模的统计问题？
- 资源分配是否偏向可识别个体？

---

### Step 2: 评估影响规模

- 个体案例的影响范围？（1人）
- 统计群体的影响范围？（N人）
- 单位资源帮助的人数：个体案例 vs 统计群体
- 总影响：哪个选项帮助更多人？

---

### Step 3: 分析心理机制

- 情感共鸣：具体个体触发情感，统计数据不触发
- 可想象性：具体个体容易被想象，统计群体抽象
- 责任归属：具体个体感觉"可帮助"，统计群体感觉"太庞大"
- 心理麻木：受害者数量增加，情感反应不线性增加

---

### Step 4: 校正资源分配

- 使用成本效益分析：每单位资源帮助多少人
- 比较个体案例和统计群体的总影响
- 设计决策框架：如果资源有限，如何最大化总帮助？
- 平衡情感与理性：承认情感价值，但不让情感主导资源分配

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **具体胜过统计**：一个具体个体比百万统计数字更能激发行动。原因：大脑情感系统对具体个体反应强烈，对抽象数字麻木。
2. **规模忽视是偏差**：帮助1人 vs 帮助100人，情感反应差异远小于100倍。原因：情感系统不处理规模，只处理具体性，导致"范围忽视"。
3. **资源有限需优化**：有限资源下，应最大化总帮助人数。原因：帮助更多人比帮助少数人产生更大总效用，即使情感满足较少。
4. **成本效益是解药**：用每单位资源帮助人数评估选项。原因：成本效益分析客观比较不同选项的真实影响，不受情感偏差影响。

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
- [ ] 是否识别了可识别信号？
- [ ] 是否评估了影响规模（个体vs群体）？
- [ ] 是否分析了心理驱动机制？
- [ ] 是否使用成本效益分析校正？
- [ ] 是否比较了总帮助人数？
- [ ] 输出具体可执行，不含模糊建议（如"帮助更多人"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [affect-heuristic](../thinking/affect-heuristic/SKILL.md) | 前置 | 情感启发式解释为何具体个体触发情感反应 |
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差使具体个体更容易被回忆 |
| [scope-neglect](../thinking/scope-neglect/SKILL.md) | 并行 | 范围忽视解释为何忽视帮助规模差异 |
| [empathy-gap](../thinking/empathy-gap/SKILL.md) | 并行 | 共情差距使预测情感反应困难 |

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

1. Schelling, T. C. (1968). The life you save may be your own. In *Problems in Public Expenditure Analysis*. Brookings Institution.
2. Small, D. A., Loewenstein, G., & Slovic, P. (2007). Sympathy and callousness: The impact of deliberative thought on donations to identifiable and statistical victims. *Organizational Behavior and Human Decision Processes*, 102(2), 143-156.
3. Jenni, K., & Loewenstein, G. (1997). Explaining the identifiable victim effect. *Journal of Risk and Uncertainty*, 14(3), 235-257.
4. Slovic, P. (2007). "If I look at the mass I will never act": Psychic numbing and genocide. *Judgment and Decision Making*, 2(2), 79-95.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
