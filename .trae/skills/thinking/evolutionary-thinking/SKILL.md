---
name: evolutionary-thinking
description: |
  触发：当需要理解系统如何随时间适应环境、设计可演进架构、利用选择压力优化方案时调用；常见信号包括"这个系统会如何进化"、"怎样设计才能适应未来变化"、"如何通过迭代淘汰差方案"。
  不触发：当系统是静态的、无需考虑时间维度时；当只需一次性设计、无需持续迭代时；当环境完全稳定、无选择压力时。
  Invoke when needing to understand how systems adapt to environments over time, designing evolvable architectures, or using selection pressure to optimize solutions.
  Do NOT invoke when systems are static without time dimension considerations, when only one-time design is needed without continuous iteration, or when the environment is completely stable without selection pressure.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["iteration-thinking", "compound-thinking", "system-thinking", "probabilistic-thinking"]
---

# 进化思维（Evolutionary Thinking）

## 核心定义

理解变异、选择和保留三个机制如何驱动系统适应环境变化，设计能够持续演进的架构和流程，而非追求一次性完美方案。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充环境变化趋势、当前变异机制和选择标准
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已设计清晰的演进机制且选择压力合理，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 定义环境和选择压力

- 明确系统所处的环境：市场、技术、用户、法规等
- 识别环境的变化趋势：哪些因素在加速变化？哪些在稳定？
- 定义选择压力：什么决定方案的存活？（用户留存、性能指标、成本等）
- 标注选择压力的强度和变化速度

---

### Step 2: 设计变异机制

- 系统如何产生新方案/新特性？
- 变异来源：内部创新、外部借鉴、随机探索、用户反馈
- 变异率：多久产生一次新方案？变异幅度多大？
- 平衡探索（exploration）和利用（exploitation）：过度探索浪费资源，过度利用陷入局部最优

---

### Step 3: 建立选择机制

- 如何评估和筛选变异方案？
- 选择标准必须与 Step 1 的选择压力对齐
- 选择速度：淘汰差方案的速度多快？
- 避免过早收敛：保留一定多样性，防止陷入局部最优

---

### Step 4: 确保保留和传递

- 好方案如何被保留和放大？
- 知识如何从一次迭代传递到下一次？
- 避免"每次从零开始"：建立累积机制
- 设计反馈循环：选择结果如何影响下一轮变异

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **适应比完美重要**：能持续适应环境的方案胜过一次性完美方案。原因：环境在变，今天的完美方案明天可能完全不适用。
2. **多样性是进化的燃料**：没有变异就没有进化。原因：单一方案无法应对未知环境变化，多样性提供适应潜力。
3. **选择压力必须真实**：虚假的选择标准会导致系统向错误方向进化。原因：如果选择标准与实际生存无关，"优胜劣汰"就失去意义。
4. **进化需要时间**：不能期望一次迭代就达到最优。原因：进化是累积过程，每代只改进一点点，但长期效果显著。

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
- [ ] 环境选择压力是否被清晰定义和量化？
- [ ] 变异机制是否平衡了探索和利用？
- [ ] 选择标准是否与真实生存指标对齐？
- [ ] 是否避免了过早收敛？
- [ ] 知识传递机制是否被设计？
- [ ] 输出具体可执行，不含模糊建议（如"持续改进"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [iteration-thinking](../thinking/iteration-thinking/SKILL.md) | 并行 | 迭代思维关注交付节奏，进化思维关注适应机制 |
| [compound-thinking](../thinking/compound-thinking/SKILL.md) | 后置 | 进化思维设计变异和选择，复利思维评估长期累积效应 |
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 系统思维提供全局结构，进化思维提供时间维度的适应机制 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维量化变异成功率和选择压力 |

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

1. Darwin, C. (1859). *On the Origin of Species*. John Murray.
2. Holland, J. H. (1992). *Adaptation in Natural and Artificial Systems*. MIT Press.
3. Beinhocker, E. D. (2006). *The Origin of Wealth: Evolution, Complexity, and the Radical Remaking of Economics*. Harvard Business Review Press.
4. Taleb, N. N. (2012). *Antifragile: Things That Gain from Disorder*. Random House.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
