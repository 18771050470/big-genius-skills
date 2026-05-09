---
name: root-cause-analysis
description: |
  触发：当需要找到问题的根本原因而非表面症状、需要防止问题重复发生、需要系统性排查故障时调用；常见信号包括"为什么总是发生"、"根本原因是什么"、"如何防止再次发生"。
  不触发：当只需快速修复、无需深入分析时；当问题原因已明确、只需执行修复时；当时间极紧迫、只需应急方案时。
  Invoke when needing to find root causes rather than surface symptoms, prevent recurring problems, or systematically troubleshoot failures.
  Do NOT invoke when only quick fixes are needed without deep analysis, when the cause is already clear and only execution is needed, or when time is extremely tight and only emergency plans are needed.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["causal-thinking", "divide-and-conquer", "inverse-thinking", "system-thinking"]
---

# 根因分析思维（Root Cause Analysis）

## 核心定义

通过系统化方法追溯问题表象到根本原因，区分症状和病因，设计治本而非治标的解决方案。核心工具：5 Whys、鱼骨图、故障树分析。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充问题描述、发生频率、影响范围和已尝试的修复方法
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已找到明确的根本原因且修复方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 定义问题

- 精确描述问题：什么、何时、何地、多大影响
- 区分症状和病因：症状是表象，病因是根源
- 量化问题影响：频率、严重度、影响范围
- 收集问题发生时的上下文信息

---

### Step 2: 追溯因果链（5 Whys）

- 连续问"为什么"，追溯因果链
- 每个"为什么"的答案必须是可验证的事实，不是猜测
- 通常5次足够，但可能更多或更少
- 当答案指向系统性原因（流程、制度、设计）时停止

---

### Step 3: 验证根本原因

- 根本原因必须满足三个条件：
  1. 如果消除这个原因，问题不会再次发生
  2. 这个原因能解释问题的所有症状
  3. 这个原因是可控制的（不是外部不可控因素）
- 用数据或实验验证因果关系
- 排除替代解释

---

### Step 4: 设计治本方案

- 针对根本原因设计解决方案，而非针对症状
- 方案类型：流程改进、制度变更、技术修复、培训
- 评估方案成本 vs 问题持续发生的成本
- 设计验证机制：如何知道问题不再发生？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **症状不是病因**：治疗症状只会暂时缓解，病因会继续产生新症状。原因：症状是病因的表现，消除表现不消除原因。
2. **5 Whys不是魔法数字**：可能需要3次或10次，关键是指向系统性原因。原因：因果链长度因问题而异，5只是经验值。
3. **根本原因必须可控制**：如果原因不可控（如天气、地震），它不是有效的根本原因。原因：不可控原因无法通过干预消除。
4. **多个根本原因可能共存**：复杂问题可能有多个根本原因。原因：系统是多因多果的，不是单因单果。

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
- [ ] 问题定义是否精确（什么、何时、何地、影响）？
- [ ] 因果链是否追溯到系统性原因？
- [ ] 根本原因是否满足三个验证条件？
- [ ] 是否排除了替代解释？
- [ ] 治本方案是否针对根本原因而非症状？
- [ ] 输出具体可执行，不含模糊建议（如"加强管理"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [causal-thinking](../thinking/causal-thinking/SKILL.md) | 前置 | 因果思维识别因果关系，根因分析追溯因果链到根源 |
| [divide-and-conquer](../thinking/divide-and-conquer/SKILL.md) | 并行 | 分治法将复杂问题拆解为可分析的子问题 |
| [inverse-thinking](../thinking/inverse-thinking/SKILL.md) | 并行 | 逆向思维从失败结果倒推原因 |
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 系统思维识别系统性原因 |

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

1. Ohno, T. (1988). *Toyota Production System: Beyond Large-Scale Production*. Productivity Press.
2. Andersen, B., & Fagerhaug, T. (2006). *Root Cause Analysis: Simplified Tools and Techniques*. ASQ Quality Press.
3. Wilson, P. F., Dell, L. D., & Anderson, G. F. (1993). *Root Cause Analysis: A Tool for Total Quality Management*. ASQ Quality Press.
4. Paradies, M. (2002). *Root Cause Analysis for Incident Investigation*. System Safety Society.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
