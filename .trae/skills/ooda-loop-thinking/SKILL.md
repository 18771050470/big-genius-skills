---
name: ooda-loop-thinking
description: |
  触发：当需要在快速变化的对抗性环境中做决策、需要比对手更快适应、需要建立快速迭代决策循环时调用；常见信号包括"情况变化太快"、"我们需要比对手更快"、"如何在不确定中快速行动"。
  不触发：当环境稳定、无需快速迭代时；当只需一次性决策、无需持续调整时；当对抗性不存在、只需优化自身时。
  Invoke when needing to make decisions in rapidly changing adversarial environments, needing to adapt faster than opponents, or needing to establish rapid iterative decision cycles.
  Do NOT invoke when the environment is stable without need for rapid iteration, when only one-time decisions are needed without continuous adjustment, or when no adversarial dynamic exists.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["iteration-thinking", "evolutionary-thinking", "dual-process-thinking", "bounded-rationality"]
---

# OODA循环思维（OODA Loop Thinking）

## 核心定义

通过观察（Observe）→判断（Orient）→决策（Decide）→行动（Act）的快速循环，在对手完成一个循环前完成多个循环，从而获得决策优势。John Boyd提出：速度不是目的，打乱对手的节奏才是。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充环境变化速度、对手信息和可用反馈渠道
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已设计清晰的OODA循环且加速策略明确，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 观察（Observe）

- 收集环境中的关键信息：市场变化、对手行动、用户反馈、技术指标
- 区分信号和噪声：哪些信息真正影响决策？
- 建立信息收集渠道：自动化监控、人工巡检、用户反馈
- 标注信息延迟：从事件发生到被观察到需要多久？

---

### Step 2: 判断（Orient）

- 将观察到的信息与已有知识、经验、文化背景结合
- 识别模式：当前情况与历史场景的相似性
- 更新心智模型：新信息是否挑战了原有假设？
- Orient是OODA的核心：它决定了你如何解读信息

---

### Step 3: 决策（Decide）

- 基于判断生成可行行动方案
- 在有限时间内选择最佳方案（不是最优方案）
- 决策标准：哪个方案能最快进入Act阶段？
- 避免分析瘫痪：决策速度比决策完美更重要

---

### Step 4: 行动（Act）

- 执行决策方案
- 行动本身就是新的观察源：行动会改变环境，产生新信息
- 记录行动结果：成功/失败、意外发现
- 准备进入下一个OODA循环

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **Orient是核心**：Boyd认为Orient占OODA 80%的重要性。原因：你的心智模型决定了你看到什么、如何解读、如何决策。
2. **速度不是目的，节奏才是**：目标不是快，而是比对手快。原因：如果你比对手快2倍，你就能在对手反应前改变局面。
3. **行动即信息**：Act不仅是执行，更是获取新信息的手段。原因：在不确定环境中，行动比分析产生更多信息。
4. **循环必须闭合**：只观察不行动或只行动不观察都无效。原因：OODA的力量来自循环迭代，不是单次执行。

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
- [ ] 观察阶段是否区分了信号和噪声？
- [ ] 判断阶段是否更新了心智模型？
- [ ] 决策阶段是否避免了分析瘫痪？
- [ ] 行动阶段是否设计了反馈机制？
- [ ] OODA循环时间是否被量化？如何加速？
- [ ] 输出具体可执行，不含模糊建议（如"快速反应"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [iteration-thinking](../thinking/iteration-thinking/SKILL.md) | 并行 | 迭代思维关注交付节奏，OODA关注决策循环速度 |
| [evolutionary-thinking](../thinking/evolutionary-thinking/SKILL.md) | 并行 | 进化思维关注适应机制，OODA关注适应速度 |
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 并行 | 双过程思维提供认知框架，OODA提供行动框架 |
| [bounded-rationality](../thinking/bounded-rationality/SKILL.md) | 并行 | 有限理性解释为何满意解优于最优解，OODA在约束下快速决策 |

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

1. Boyd, J. R. (1987). *A Discourse on Winning and Losing*. Air University.
2. Richards, C. (2004). *Certain to Win: The Strategy of John Boyd, Applied to Business*. Xlibris.
3. Coram, R. (2002). *Boyd: The Fighter Pilot Who Changed the Art of War*. Little, Brown.
4. Osinga, F. P. B. (2007). *Science, Strategy and War: The Strategic Theory of John Boyd*. Routledge.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
