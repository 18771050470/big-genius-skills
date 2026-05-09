---
name: bounded-rationality
description: |
  触发：当需要在信息不完整、时间有限、认知资源受限的情况下做决策时调用；常见信号包括"信息不够但必须决定"、"没有完美方案"、"差不多就行了"。
  不触发：当有充足时间、完整信息和充足计算资源时；当只需理论分析、无需实际决策时；当决策影响极小、可随意选择时。
  Invoke when needing to make decisions under incomplete information, time constraints, or limited cognitive resources.
  Do NOT invoke when there is ample time, complete information, and sufficient computational resources, when only theoretical analysis is needed without actual decision, or when decision impact is minimal.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["satisficing", "dual-process-thinking", "constraint-thinking", "opportunity-cost"]
---

# 有限理性（Bounded Rationality）

## 核心定义

在现实约束下（信息不完整、时间有限、认知能力受限），追求"足够好"的满意解而非理论最优解。Herbert Simon提出：人是"满意者"而非"最优化者"。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充决策约束（时间、信息、资源）
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已找到满足满意标准的方案，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 评估决策约束

- 信息约束：哪些关键信息缺失？获取成本多高？
- 时间约束：决策截止是什么时候？还有多少时间？
- 认知约束：问题的复杂度是否超出个人/团队处理能力？
- 资源约束：可用于决策的预算、人力、工具是否充足？

---

### Step 2: 设定满意标准（Aspiration Level）

- 定义"足够好"的标准：满足哪些条件就接受？
- 满意标准应基于现实约束，而非理想状态
- 参考历史基准或行业标准设定满意阈值
- 标注满意标准的合理性依据

---

### Step 3: 顺序搜索可行方案

- 按可获得性顺序搜索方案（不是穷举所有方案）
- 每找到一个方案，评估是否满足满意标准
- 如果满足，接受该方案并停止搜索
- 如果不满足，继续搜索或调整满意标准

---

### Step 4: 评估搜索成本与收益

- 继续搜索的边际收益是否超过边际成本？
- 时间消耗是否接近决策截止？
- 是否存在"搜索瘫痪"风险（过度搜索导致错过时机）？
- 决定是接受当前最佳方案还是继续搜索

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **满意优于最优**：在约束条件下，满意解比追求最优解更实际。原因：最优解需要无限信息和计算，现实中不存在。
2. **满意标准必须动态调整**：根据搜索结果和环境变化调整标准。原因：固定标准可能导致过早接受差方案或永不满足。
3. **搜索成本是真实成本**：花时间找更好方案的时间也是成本。原因：延迟决策本身可能产生机会成本。
4. **启发式不是缺陷而是适应**：在有限理性下，启发式是高效的适应策略。原因：Gigerenzer证明"少即是多"——简单启发式在不确定环境中常优于复杂模型。

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
- [ ] **有限理性特供**：决策约束是否被完整评估？信息缺口、时间截止、认知复杂度、资源限制是否被逐一量化？
- [ ] **有限理性特供**：满意标准（Aspiration Level）是否有明确依据？标准是否基于现实约束而非理想状态？是否标注了合理性依据？
- [ ] **有限理性特供**：搜索过程是否考虑了边际成本收益？继续搜索的边际收益是否超过边际成本？是否存在"搜索瘫痪"风险？
- [ ] **有限理性特供**：接受的方案是否确实满足满意标准？是否进行了"反向测试"——如果找到更差方案，当前方案是否仍被接受？
- [ ] **有限理性特供**：是否评估了启发式的适用性？简单启发式在当前情境下是否优于复杂模型？是否参考了Gigerenzer的"少即是多"原则？
- [ ] **有限理性特供**：满意标准是否被设计为动态可调？当环境变化或新信息到达时，标准是否允许调整？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"找个差不多的"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 并行 | 双过程思维识别认知模式，有限理性提供决策框架 |
| [constraint-thinking](../thinking/constraint-thinking/SKILL.md) | 前置 | 约束思维识别限制条件，有限理性在约束下做决策 |
| [opportunity-cost](../thinking/opportunity-cost/SKILL.md) | 并行 | 机会成本评估搜索的时间成本 |
| [occams-razor](../thinking/occams-razor/SKILL.md) | 并行 | 奥卡姆剃刀在满意方案中选择最简方案 |

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

1. Simon, H. A. (1957). *Models of Man: Social and Rational*. Wiley.
2. Simon, H. A. (1955). A behavioral model of rational choice. *Quarterly Journal of Economics*, 69(1), 99-118.
3. Gigerenzer, G., & Selten, R. (2002). *Bounded Rationality: The Adaptive Toolbox*. MIT Press.
4. March, J. G. (1994). *A Primer on Decision Making: How Decisions Happen*. Free Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
