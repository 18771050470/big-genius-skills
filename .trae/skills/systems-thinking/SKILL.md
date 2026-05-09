---
name: systems-thinking
description: |
  触发：当问题涉及多个相互关联的组件、存在反馈循环、局部优化导致全局恶化、需要识别杠杆点时调用；常见信号包括"为什么越修越糟"、"各部分都对了但整体不行"、"有没有牵一发而动全身的解决方案"。
  不触发：当问题是孤立的、线性因果关系明确时；当只需优化单一组件且不影响其他部分时；当时间极紧迫、只需应急修复时。
  Invoke when facing problems involving multiple interconnected components, feedback loops, local optimization causing global degradation, or when leverage points need identification.
  Do NOT invoke when problems are isolated with clear linear causality, when only a single component needs optimization without affecting others, or when time is extremely tight and only emergency fixes are needed.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["second-order-thinking", "holism", "causal-thinking", "leverage-thinking"]
---

# 系统思维（Systems Thinking）

## 核心定义

将问题视为由相互关联的组件构成的整体，识别反馈回路、延迟效应和涌现行为，寻找改变系统行为的高杠杆点。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统组件和连接关系
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别出明确的高杠杆点且干预方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 界定系统边界

- 明确系统的范围：什么在系统内，什么在系统外
- 识别系统的关键利益相关者和受影响方
- 定义系统的目标或功能（系统存在的目的是什么）
- 警惕边界划定过窄（遗漏关键组件）或过宽（分析瘫痪）

---

### Step 2: 识别系统组件和连接

- 列出系统内的关键元素（变量、实体、角色）
- 绘制元素之间的因果关系：A 增加导致 B 增加/减少
- 区分物质流（资金、人员、数据）和信息流（信号、反馈）
- 标注连接的强度和方向性

---

### Step 3: 发现反馈回路

- 识别增强回路（正反馈）：自我强化的循环，导致指数增长或崩溃
- 识别调节回路（负反馈）：自我纠正的循环，维持稳定或振荡
- 标注回路中的延迟：因果之间的时间差
- 判断主导回路：哪个回路在当前阶段起决定作用

---

### Step 4: 识别系统原型和杠杆点

- 匹配常见系统原型：饮鸩止渴、舍本逐末、目标侵蚀、增长上限等
- 寻找杠杆点：小的干预能产生大的系统行为改变
- 杠杆点优先级（从低到高）：参数 → 缓冲 → 结构 → 信息流 → 规则 → 目标 → 范式
- 评估干预的副作用和延迟效应

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **整体大于部分之和**：系统行为不能通过单独分析组件来预测。原因：涌现行为来自组件间的互动，而非组件本身。
2. **反馈决定行为**：系统的动态行为主要由反馈回路结构决定，而非外部冲击。原因：理解反馈结构才能预测系统如何响应干预。
3. **延迟导致振荡**：因果之间的时间差是系统不稳定和过度反应的根源。原因：决策者基于过时信息行动，导致矫枉过正。
4. **杠杆点在高阶**：改变系统规则、目标或范式比调整参数效果更大。原因：参数只影响系统运行方式，规则决定系统如何运行。

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
- [ ] 系统边界是否合理划定？是否遗漏关键组件？
- [ ] 反馈回路是否被完整识别？增强回路和调节回路是否区分？
- [ ] 延迟效应是否被标注？延迟时间是否被估计？
- [ ] 杠杆点是否按 Meadows 层级排序？
- [ ] 干预方案的副作用和延迟后果是否被评估？
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [second-order-thinking](../thinking/second-order-thinking/SKILL.md) | 并行 | 二阶思维专注后果推演，系统思维提供全局结构视角 |
| [causal-thinking](../thinking/causal-thinking/SKILL.md) | 前置 | 因果思维识别单条因果链，系统思维整合为网络 |
| [leverage-thinking](../thinking/leverage-thinking/SKILL.md) | 后置 | 系统思维识别杠杆点，杠杆思维评估干预效果 |
| [holism](../thinking/holism/SKILL.md) | 并行 | 整体论强调不可分割性，系统思维强调组件互动 |

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

1. Meadows, D. H. (2008). *Thinking in Systems: A Primer*. Chelsea Green Publishing.
2. Senge, P. M. (1990). *The Fifth Discipline: The Art and Practice of the Learning Organization*. Doubleday.
3. Forrester, J. W. (1961). *Industrial Dynamics*. MIT Press.
4. Sterman, J. D. (2000). *Business Dynamics: Systems Thinking and Modeling for a Complex World*. McGraw-Hill.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
