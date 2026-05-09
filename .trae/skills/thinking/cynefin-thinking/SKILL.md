---
name: cynefin-thinking
description: |
  触发：当需要判断问题所属域（简单、繁杂、复杂、混乱）、需要选择匹配的决策方法时调用；常见信号包括"这个问题属于什么类型"、"该用什么方法处理"、"为什么之前的方法不管用"。
  不触发：当问题类型已明确、只需执行时；当只需单一方法、无需分类判断时；当问题明显属于某一域、无争议时。
  Invoke when needing to categorize problems into domains (simple, complicated, complex, chaotic) and select matching decision methods.
  Do NOT invoke when problem type is already clear and only execution is needed, when only a single method is needed without categorization, or when the problem clearly belongs to one domain without dispute.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["system-thinking", "bounded-rationality", "evolutionary-thinking", "dual-process-thinking"]
---

# Cynefin框架思维（Cynefin Framework Thinking）

## 核心定义

将问题分类到五个域（简单、繁杂、复杂、混乱、无序），每个域对应不同的决策方法：感知-分类-响应（简单）、感知-分析-响应（繁杂）、探索-感知-响应（复杂）、行动-感知-响应（混乱）。Dave Snowden提出：不同域的问题需要不同的管理方法。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充问题特征、因果关系明确程度和历史数据可用性
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确问题所属域且对应决策方法清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 评估因果关系明确程度

- 因果关系是否清晰可预测？
- 是否有历史数据和最佳实践可参考？
- 专家是否能达成共识？
- 这是判断问题域的核心维度

---

### Step 2: 判定问题所属域

- **简单域（Simple）**：因果关系明确，最佳实践存在，按标准流程处理
- **繁杂域（Complicated）**：因果关系可分析但需专家判断，良好实践存在，需要分析
- **复杂域（Complex）**：因果关系只能事后理解，涌现行为，需要实验探索
- **混乱域（Chaotic）**：因果关系不存在，危机状态，需要立即行动稳定局面
- **无序域（Disorder）**：无法判断属于哪个域，需要更多信息

---

### Step 3: 选择匹配的决策方法

- 简单域：感知 → 分类 → 响应（按最佳实践执行）
- 繁杂域：感知 → 分析 → 响应（请专家分析后决策）
- 复杂域：探索 → 感知 → 响应（小步实验，观察涌现模式）
- 混乱域：行动 → 感知 → 响应（立即行动稳定局面，再评估）
- 错误匹配域和方法是常见失败原因

---

### Step 4: 识别域间迁移

- 问题是否可能从一个域迁移到另一个域？
- 简单域过度简化可能变成复杂域
- 混乱域稳定后可能进入复杂域或繁杂域
- 设计域间迁移的预警和应对策略

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **域匹配比方法优劣更重要**：用错域的方法比方法本身差更致命。原因：在复杂域用最佳实践会忽略涌现行为，在简单域用实验会浪费资源。
2. **复杂域不可预测**：复杂系统的因果关系只能事后理解。原因：涌现行为来自组件互动，无法通过事前分析预测。
3. **混乱域先行动后思考**：危机时刻没有时间分析。原因：混乱域的首要任务是建立秩序，而非理解原因。
4. **警惕域迁移**：问题可能随时间从一个域迁移到另一个域。原因：环境变化、干预效果、新信息都可能改变问题性质。

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
- [ ] **Cynefin特供**：因果关系明确程度是否被准确评估？是否清晰可预测？是否有历史数据和最佳实践？专家是否能达成共识？
- [ ] **Cynefin特供**：问题域判定是否有充分依据？简单域（最佳实践）/繁杂域（良好实践）/复杂域（涌现行为）/混乱域（立即行动）的判定是否基于证据？
- [ ] **Cynefin特供**：决策方法是否与问题域匹配？简单域（感知-分类-响应）/繁杂域（感知-分析-响应）/复杂域（探索-感知-响应）/混乱域（行动-感知-响应）是否正确对应？
- [ ] **Cynefin特供**：是否考虑了域间迁移的可能性？问题是否可能从一个域迁移到另一个域？是否设计了域间迁移的预警和应对策略？
- [ ] **Cynefin特供**：是否警惕了"简单域错觉"（看似简单实际复杂）？是否过度简化导致最佳实践失效？是否准备了复杂域的实验方法作为备选？
- [ ] 输出具体可执行，不含模糊建议（如"灵活应对"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 系统思维分析全局结构，Cynefin判断问题类型 |
| [bounded-rationality](../thinking/bounded-rationality/SKILL.md) | 并行 | 有限理性在复杂域和混乱域特别适用 |
| [evolutionary-thinking](../thinking/evolutionary-thinking/SKILL.md) | 并行 | 进化思维提供复杂域的探索-感知-响应方法 |
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 并行 | 双过程思维在混乱域需要系统1快速反应 |

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

1. Snowden, D. J., & Boone, M. E. (2007). A leader's framework for decision making. *Harvard Business Review*, 85(11), 68-76.
2. Snowden, D. J., & Kurtz, C. F. (2009). The new dynamics of strategy: Sense-making in a complex and complicated world. *IBM Systems Journal*, 48(3), 377-398.
3. Kurtz, C. F., & Snowden, D. J. (2003). The new dynamics of strategy: Sense-making in a complex and complicated world. *Human Systems Management*, 22(3), 195-210.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
