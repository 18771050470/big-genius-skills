---
name: feedback-loops
description: |
  触发：当需要分析系统中自我强化或自我抑制的动态、理解行为后果的循环影响、设计系统调节机制时调用；常见信号包括"越...越..."、"恶性循环"、"良性循环"、"系统振荡"、"指数增长/衰减"。
  不触发：当系统是简单的线性因果链（A→B→C，无回路）时；当只需分析一次性事件、无持续互动时；当系统处于稳定平衡且无变化趋势时。
  Invoke when analyzing self-reinforcing or self-correcting dynamics in systems, understanding circular impacts of actions, or designing system regulation mechanisms.
  Do NOT invoke when the system is a simple linear causal chain (A→B→C, no loops), when analyzing one-time events without ongoing interaction, or when the system is in stable equilibrium with no change trend.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["system-thinking", "entropy-thinking", "compound-thinking", "critical-mass"]
---

# 反馈回路思维（Feedback Loops Thinking）

## 核心定义

系统中输出反过来影响输入的循环结构。正反馈（增强回路）放大变化，导致指数增长或崩溃；负反馈（调节回路）抵抗变化，维持系统稳定。Forrester 1956年创立系统动力学，Meadows指出"反馈回路是系统思考的基础建筑块"。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统的关键变量、变量间的因果关系和时间延迟
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确反馈回路结构且干预方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别系统中的变量

- 列出系统中的关键存量（Stocks）：累积量，如用户数量、库存、技术债务
- 列出关键流量（Flows）：变化率，如新增用户、消耗速度、Bug产生率
- 区分存量和流量：存量是"有多少"，流量是"变化多快"
- 标注每个变量的当前值和变化趋势

### Step 2: 绘制因果回路图

- 识别变量间的因果关系：A的变化如何影响B？
- 标注因果极性：同向变化（+）或反向变化（-）
- 寻找回路：从某变量出发，经过一系列因果链回到自身
- 判断回路类型：正反馈（偶数个负号）或负反馈（奇数个负号）

### Step 3: 分析反馈回路动态

- 正反馈回路：是否在指数增长？增长极限在哪里？（资源限制、市场饱和）
- 负反馈回路：目标值是什么？当前与目标的差距？调节速度如何？
- 延迟效应：行动到效果之间的时间差？延迟导致振荡还是超调？
- 回路间的互动：多个回路同时作用时，主导回路是什么？

### Step 4: 设计干预策略

- 增强期望的正反馈：降低增长阻力、提供更多资源
- 抑制有害的正反馈：打破循环、引入负反馈调节
- 调整负反馈目标：如果系统稳定在错误水平，改变目标值
- 管理延迟：减少关键延迟以避免振荡，或利用延迟创造缓冲

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **正反馈产生指数，负反馈产生稳定**：正反馈回路导致指数增长或衰减，负反馈回路追求目标并保持稳定。原因：正反馈中变化被放大，负反馈中变化被抵抗。
2. **延迟是振荡的根源**：负反馈回路中的时间延迟导致系统超调和振荡。原因：调节行动基于过时信息，矫枉过正。
3. **主导回路决定系统行为**：多个回路共存时，当前最强的回路决定系统趋势。原因：回路强度随时间变化，系统行为会切换。
4. **改变回路结构比改变变量更有效**：调整回路连接方式比单纯改变参数更有持久影响。原因：结构决定行为，参数只改变行为幅度。

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
- [ ] 系统中的关键变量（存量和流量）是否被识别？
- [ ] 因果回路图是否被绘制？回路类型（正/负）是否被正确判断？
- [ ] 延迟效应是否被分析？
- [ ] 主导回路是否被识别？
- [ ] 干预策略是否针对回路结构而非单一变量？
- [ ] 输出具体可执行，不含模糊建议（如"优化系统"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [system-thinking](../thinking/system-thinking/SKILL.md) | 前置 | 系统思维提供全局视角，反馈回路是系统的动态机制 |
| [entropy-thinking](../thinking/entropy-thinking/SKILL.md) | 并行 | 正反馈加速熵增，负反馈是减熵机制 |
| [compound-thinking](../thinking/compound-thinking/SKILL.md) | 并行 | 正反馈是复利效应的系统动力学解释 |
| [critical-mass](../thinking/critical-mass/SKILL.md) | 并行 | 临界点是正反馈回路从缓慢到爆发的转折点 |

---

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | 系统动力学理论、因果回路图绘制规范 |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Forrester, J. W. (1956). Industrial dynamics: A major breakthrough for decision makers. *Harvard Business Review*, 34(4), 37-66.
2. Meadows, D. H. (2008). *Thinking in Systems: A Primer*. Chelsea Green Publishing.
3. Senge, P. M. (1990). *The Fifth Discipline: The Art and Practice of the Learning Organization*. Doubleday.
4. Sterman, J. D. (2000). *Business Dynamics: Systems Thinking and Modeling for a Complex World*. McGraw-Hill.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
