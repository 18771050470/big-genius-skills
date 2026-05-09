---
name: second-order-thinking
description: |
  触发：当面临重要决策，需要考虑间接、延迟或非预期的后果时调用；常见信号包括"有没有什么我们没想到的？"、"长期来看会怎样？"、"如果每个人都这么做？"、"那然后呢？"。
  不触发：当日常琐事（如午餐吃什么、选择哪种文具）；当时间极紧迫、且后果可逆性高时；当决策影响范围极小、不影响外部系统或人物时。
  Invoke when facing important decisions where indirect, delayed, or unintended consequences may arise.
  Do NOT invoke when dealing with daily trivial matters, when time is extremely tight with reversible consequences, or when impact scope is minimal.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["system-thinking", "inverse-thinking", "causal-thinking", "probabilistic-thinking"]
---

# 二阶思维（Second-Order Thinking）

## 核心定义

不仅考虑决策的直接后果（一阶效应），还要推演后果的后果（二阶、三阶乃至更高阶效应），识别延迟反馈和非预期后果。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充决策背景、利益相关方和系统环境
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已推演出明确的二阶效应且风险可控，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别一阶效应（直接后果）

- 决策执行后，最直接、最明显的结果是什么？
- 谁会立即受益？谁会立即受损？
- 一阶效应通常在短期内可见
- 列出所有一阶效应，不预设好坏

---

### Step 2: 推演二阶效应（后果的后果）

- 一阶效应发生后，会引发什么连锁反应？
- 受益者/受损者会如何反应？他们的反应会产生什么新后果？
- 如果所有人都采取相同决策，系统会怎样？
- 标注二阶效应的时间延迟：多久后会出现？

---

### Step 3: 推演三阶及更高阶效应

- 二阶效应会进一步引发什么变化？
- 系统是否会达到新的均衡？还是持续振荡？
- 是否存在正反馈循环（自我强化）或负反馈循环（自我纠正）？
- 标注高阶效应的不确定性：越往后不确定性越大

---

### Step 4: 评估净效应

- 综合一阶、二阶、三阶效应，计算净收益/净损失
- 一阶收益是否被二阶损失抵消？（常见陷阱）
- 识别"饮鸩止渴"模式：短期收益、长期损失
- 识别"先苦后甜"模式：短期成本、长期收益

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **一阶效应人人可见，二阶效应才是竞争优势**：Howard Marks指出，超越市场的洞察来自二阶思维。原因：一阶思维是共识，共识已被定价。
2. **延迟效应最危险**：后果与行动之间的时间差导致决策者误判因果。原因：延迟使决策者以为行动无效而加码，或以为行动有效而忽视隐患。
3. **"如果每个人都这么做"是终极测试**：个体理性的行为在集体层面可能灾难性。原因：合成谬误——对个体正确的事对整体不一定正确。
4. **高阶效应不确定性递增**：三阶效应比二阶更难预测。原因：每增加一阶，涉及的变量和互动呈指数增长。

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
- [ ] 一阶效应是否被完整列出？是否区分了受益方和受损方？
- [ ] 二阶效应是否考虑了利益相关方的反应？
- [ ] 是否进行了"如果每个人都这么做"的测试？
- [ ] 高阶效应的时间延迟是否被标注？
- [ ] 净效应是否综合了所有阶次的效应？
- [ ] 是否识别了"饮鸩止渴"或"先苦后甜"模式？
- [ ] 输出具体可执行，不含模糊建议（如"考虑长远"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 系统思维提供全局结构，二阶思维专注后果推演 |
| [inverse-thinking](../thinking/inverse-thinking/SKILL.md) | 并行 | 逆向思维从失败角度思考，二阶思维从后果角度推演 |
| [causal-thinking](../thinking/causal-thinking/SKILL.md) | 前置 | 因果思维识别单条因果链，二阶思维推演因果链的延伸 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维量化高阶效应的不确定性 |

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

1. Marks, H. (2011). *The Most Important Thing Illuminated*. Columbia University Press. Chapter 2: Second-Level Thinking.
2. Merton, R. K. (1936). The unanticipated consequences of purposive social action. *American Sociological Review*, 1(6), 894-904.
3. Senge, P. M. (1990). *The Fifth Discipline*. Doubleday. Chapter 5: A Shift of Mind.
4. Bazerman, M. H. (2006). *Judgment in Managerial Decision Making*. Wiley.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
