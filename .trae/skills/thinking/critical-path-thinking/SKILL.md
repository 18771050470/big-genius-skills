---
name: critical-path-thinking
description: |
  触发：当需要识别项目关键路径、优化项目交付时间、分析任务依赖关系时调用；常见信号包括"最短多久能完成"、"哪些任务不能延迟"、"如何加快交付"。
  不触发：当任务间无依赖关系、可并行执行时；当只需估算单个任务时间、无需分析整体时；当项目极小、关键路径显而易见时。
  Invoke when needing to identify project critical paths, optimize delivery time, or analyze task dependencies.
  Do NOT invoke when tasks have no dependencies and can be executed in parallel, when only estimating single task time without overall analysis, or when the project is so small that the critical path is obvious.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["divide-and-conquer", "constraint-thinking", "iteration-thinking", "cost-thinking"]
---

# 关键路径思维（Critical Path Thinking）

## 核心定义

识别项目中最长的任务序列（关键路径），该序列决定了项目的最短完成时间。关键路径上的任何延迟都会直接导致项目整体延迟。核心方法：关键路径法（CPM）、PERT分析。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充任务列表、任务依赖关系和任务时间估算
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确关键路径且优化策略清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 列出所有任务

- 完整列出项目所有任务，不遗漏
- 每个任务标注：名称、前置任务、预估时间、资源需求
- 使用WBS（工作分解结构）确保任务完整性
- 任务粒度应适中：太粗无法分析，太细增加复杂度

---

### Step 2: 构建依赖网络

- 绘制任务依赖图：哪些任务必须在其他任务之前完成？
- 依赖类型：完成-开始（FS）、开始-开始（SS）、完成-完成（FF）、开始-完成（SF）
- 识别并行任务：哪些任务可以同时执行？
- 检查循环依赖：A依赖B、B依赖C、C依赖A（必须打破）

---

### Step 3: 计算关键路径

- 正向计算：每个任务的最早开始时间（ES）和最早完成时间（EF）
- 反向计算：每个任务的最晚开始时间（LS）和最晚完成时间（LF）
- 计算浮动时间（Slack）：LS - ES 或 LF - EF
- 关键路径 = 浮动时间为0的任务序列，即最长路径

---

### Step 4: 分析优化机会

- 压缩关键路径上的任务时间（赶工或快速跟进）
- 评估压缩成本：赶工成本 vs 时间收益
- 注意：压缩关键路径可能导致新的关键路径出现
- 识别资源瓶颈：资源冲突可能创造新的关键路径

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **关键路径决定项目最短时间**：非关键路径的优化不影响整体交付。原因：项目完成时间由最长路径决定，缩短非关键路径不会缩短最长路径。
2. **浮动时间是缓冲**：非关键路径的浮动时间可以吸收延迟。原因：浮动时间是非关键路径可以延迟而不影响整体交付的时间。
3. **压缩关键路径有极限**：过度压缩会导致质量下降或成本激增。原因：任务时间有物理极限，不能无限压缩。
4. **关键路径会变化**：压缩后可能出现新的关键路径。原因：原关键路径缩短后，原非关键路径可能成为新的最长路径。

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
- [ ] **关键路径特供**：任务列表是否完整？是否有遗漏的关键任务？是否使用了WBS确保任务完整性？任务粒度是否适中？
- [ ] **关键路径特供**：依赖关系是否被正确识别？是否有循环依赖？依赖类型（FS/SS/FF/SF）是否被标注？并行任务是否被识别？
- [ ] **关键路径特供**：关键路径计算是否正确？正向计算（ES/EF）和反向计算（LS/LF）是否完整？浮动时间（Slack）是否准确？
- [ ] **关键路径特供**：优化策略是否考虑了压缩成本和收益？赶工成本 vs 时间收益是否被量化？快速跟进的风险是否被评估？
- [ ] **关键路径特供**：是否预警了关键路径可能变化？压缩后是否可能出现新的关键路径？资源冲突是否被考虑？
- [ ] 输出具体可执行，不含模糊建议（如"加快进度"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [divide-and-conquer](../thinking/divide-and-conquer/SKILL.md) | 前置 | 分治法将项目分解为可分析的任务 |
| [constraint-thinking](../thinking/constraint-thinking/SKILL.md) | 并行 | 约束思维识别项目瓶颈，关键路径思维量化瓶颈影响 |
| [iteration-thinking](../thinking/iteration-thinking/SKILL.md) | 并行 | 迭代思维提供敏捷交付替代方案 |
| [cost-thinking](../thinking/cost-thinking/SKILL.md) | 并行 | 成本思维评估赶工成本与时间收益的权衡 |

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

1. Kelley, J. E., & Walker, M. R. (1959). Critical-path planning and scheduling. *Proceedings of the Eastern Joint Computer Conference*, 160-173.
2. Malcolm, D. G., Roseboom, J. H., Clark, C. E., & Fazar, W. (1959). Application of a technique for research and development program evaluation. *Operations Research*, 7(5), 646-669.
3. Leach, L. P. (2005). *Critical Chain Project Management* (2nd ed.). Artech House.
4. Goldratt, E. M. (1997). *Critical Chain*. North River Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
