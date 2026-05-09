---
name: causal-thinking
description: |
  触发：当需要判断两个变量/事件之间是否存在因果关系、分析结果的根本原因、设计需要确保因果链闭环的实验或决策时调用；常见信号包括发现强相关但不确定因果、试图解释现象背后机理、评估干预方案的有效性。
  不触发：当仅需描述现象（如"今天下雨"）、纯描述性统计且不涉及因果解释、或问题明显是简单事实性时，不要调用此 Skill。
  Invoke when reasoning about cause-effect relationships, distinguishing correlation from causation, tracing causal chains/networks. Do NOT invoke for pure descriptive statistics or simple factual questions without causal inquiry.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["first-principles", "system-thinking", "inversion", "second-order-effects"]
---

# 因果思维 (Causal Thinking)

## 核心定义

因果思维是一种系统性地区分相关性与因果性、揭示因果链（A→B→C）及因果网络，并避免"后此谬误"的底层认知模型。它要求我们追问"为什么"，而非仅仅看到"什么"。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 观察与描述

- 描述变量X与变量Y的表面关系（相关性方向、强度、时间先后）
- {X, Y, 相关系数r, 时间顺序, 背景条件}

### Step 2: 区分相关性与可能性因果

- 列举支持因果关系的初步理由（如时间先后、理论支持）与反对理由（如第三方变量）
- 因果假设 H0: X 不导致 Y ; H1: X 导致 Y ; 并列出可能的混淆变量 Z

### Step 3: 构建因果链（A→B→C）

- 绘制最小因果链图，标注X、Y以及中介变量M、混淆变量Z；考虑是否存在反向因果（Y←X）
- 因果链图（DAG）及每条边的方向与证据

### Step 4: 检验因果推断的四大标准

- 逐一检查：时间先后（X先于Y）？强度（相关性是否显著）？一致性（不同条件下是否一致）？特异性（排除其他解释）？
- 每个标准的满足/不满足标记，并记录不确定性等级

### Step 5: 设计"反事实"思维实验

- 想象如果X没有发生，Y会如何？可用自然实验、工具变量、随机对照试验（RCT）等理想方法检验
- 反事实推理结果（"如果X=0，Y的估计值"）

### Step 6: 识别并预防"后此谬误"

- 检查是否存在"因为B在A之后发生，所以A导致B"的逻辑；若有，回溯Step 2-3重新分析
- 后此谬误风险标记（高/中/低）及修正后的因果模型

### Step 7: 综合生成因果解释

- 撰写简洁的因果解释，包含主要因果路径、证据强度、替代假设及不确定度
- 因果分析报告（含DAG、证据表、结论置信度）

### Step 8: 设置监控与验证计划

- 明确下一步验证方法（如A/B测试、追踪数据收集、敏感性分析），以及何时应修正或放弃当前因果假设
- 可执行的验证计划（包含时间点、指标、决策阈值）

## 关键原则

| 原则 | 说明 | 违背原因 |
|------|------|---------|
| **区分相关≠因果** | 相关只是因果的必要非充分条件，需排除混淆变量 | 贸然将相关当作因果导致错误决策 |
| **构建因果链** | 用DAG画出从因到果的中间环节，揭露隐藏路径 | 忽略中介变量或混淆变量，因果链断裂 |
| **反事实思维** | 必须能回答"如果未发生X，Y如何？" | 无法进行反事实推理，因果推断不可靠 |
| **警惕后此谬误** | 时间先后不意味着因果 | 将"之后"等同于"因为"，产生虚假因果 |
| **因果网络视角** | 单一因果链往往不足，需考虑多因多果、反馈回路 | 忽略系统效应，导致因果解释片面 |

## 自检清单

> 聚焦因果思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**因果思维特有关键检查项**：

- [ ] **因果思维特供**：是否区分了相关性与因果性？是否还有其他解释（如第三方变量、巧合）？是否计算了混淆变量的影响？
- [ ] **因果思维特供**：是否考虑了反向因果？Y→X 的可能性是否被排除？是否使用了工具变量或自然实验来排除反向因果？
- [ ] **因果思维特供**：是否识别了所有混淆变量？是否有遗漏的变量同时影响X和Y？是否绘制了因果图（DAG）来可视化变量关系？
- [ ] **因果思维特供**：是否进行了反事实推理？"如果X未发生，Y会怎样？"是否被回答？是否使用了潜在结果框架（Potential Outcomes Framework）？
- [ ] **因果思维特供**：是否陷入了"后此谬误"（post hoc ergo propter hoc）？是否将时间先后等同于因果关系？是否有独立证据支持因果方向？
- [ ] **因果思维特供**：是否量化了不确定性？结论的置信度是否被明确标注？是否进行了敏感性分析检验结论稳健性？

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [first-principles](../thinking/first-principles/SKILL.md) | 前置 | 当需要解构基本事实以构建因果链时，先拆解到不可再分元素 |
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 因果网络中存在反馈回路、动态行为时，需联动系统思维 |
| [inverse-thinking](../thinking/inverse-thinking/SKILL.md) | 后置 | 检验因果假设时，反向思考"如果造成相反结果会如何？" |
| [second-order-effects](../thinking/second-order-effects/SKILL.md) | 后置 | 分析因果链的深层结果（A→B→C中的C往往是二阶效应） |

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Pearl, J. (2009). *Causality: Models, Reasoning, and Inference* (2nd ed.). Cambridge University Press.
2. Pearl, J., & Mackenzie, D. (2018). *The Book of Why: The New Science of Cause and Effect*. Basic Books.
3. VanderWeele, T. J. (2015). *Explanation in Causal Inference: Methods for Mediation and Interaction*. Oxford University Press.
4. Holland, P. W. (1986). Statistics and Causal Inference. *Journal of the American Statistical Association*, 81(396), 945-960.
