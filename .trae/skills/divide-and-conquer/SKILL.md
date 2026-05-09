---
name: divide-and-conquer
description: |
  触发：当面对一个过于庞大或复杂而难以一次性解决的问题、需要将大任务拆解为小任务、需要并行处理或分工协作时调用；常见信号包括"这个任务太大了不知从哪里开始"、"能不能拆开分别做"、"问题太复杂需要分解"、"需求太多需要分批实现"。
  不触发：当问题本身高度耦合无法独立拆解时；当拆解的代价超过直接整体处理的代价时；当子问题之间依赖关系极强、拆解后沟通成本激增时。
  Invoke when facing a problem too large or complex to solve at once, needing to decompose a large task into smaller tasks, or requiring parallel processing or division of labor.
  Do NOT invoke when the problem is highly coupled and cannot be independently decomposed, when decomposition cost exceeds the cost of direct holistic processing, or when sub-problems have such strong dependencies that communication cost explodes after splitting.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["algorithmic-thinking", "system-thinking", "reductionism", "recursive-thinking", "abstraction-layering"]
---

# 分治思维（Divide and Conquer）

## 核心定义

将复杂的大问题递归地拆解为多个结构相同但规模更小的独立子问题，逐个解决后合并结果——分而治之，化大为小，化繁为简。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充问题结构和子问题边界
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告无法拆解的原因，等待决策
- **提前终止**：若问题规模已经足够小、可直接解决，则跳过剩余拆分步骤，直接进入解决阶段，标注"提前终止拆分，问题已达到基础规模"

---

## 思考流程

### Step 1: 界定问题边界

- 明确要解决的原始问题的完整范围和目标
- 识别问题的输入、输出和约束条件
- 判断问题的规模：究竟"大"在哪？哪些部分造成了复杂度？
- 确认问题是否真的需要拆分：如果问题本身可以在合理时间内直接解决，不做过度拆分

---

### Step 2: 确定拆分策略

- 按功能维度拆分：用户模块、订单模块、支付模块
- 按层次维度拆分：数据层、业务层、展示层
- 按数据维度拆分：按地域、按时间、按用户ID范围
- 按阶段维度拆分：数据收集→处理→验证→输出
- 使用MECE原则（Mutually Exclusive, Collectively Exhaustive）：子问题之间互不重叠、合起来完全覆盖原问题
- 选择拆分策略的标准：子问题之间耦合度最低、接口最清晰、能最大化并行处理

---

### Step 3: 定义子问题接口

- 每个子问题的输入是什么？来自哪里？
- 每个子问题的输出是什么？如何合并？
- 子问题之间的依赖关系图：哪些可以并行？哪些必须串行？
- 接口不清晰的子问题说明拆分不够好，需要重新考虑边界
- 定义"基础问题"的终止条件：问题小到什么程度可以直接解决而不再拆分？

---

### Step 4: 逐个解决子问题

- 按依赖关系排序执行：先解决被依赖的子问题，再解决依赖方
- 对每个子问题：规模仍然太大 → 递归拆分；规模可处理 → 直接解决
- 如果某个子问题也需要分治，嵌套应用本思维模型
- 记录每个子问题的解决方案和关键假设

---

### Step 5: 合并子问题结果

- 将各子问题的输出按预定义的接口组合为原问题的解
- 检查合并过程中是否产生新的问题：接口不匹配、边界遗漏、重复计算
- 验证组合结果是否完整覆盖了原始问题的所有需求
- 特别警惕"组合损耗"：子问题单独正确，但组合后出现预期外的交互效应

---

### Step 6: 总结输出

- 整合前面各步的分析结果
- 输出拆分结构图、子问题清单、依赖关系、合并策略
- 标注拆分的前提假设和关键风险
- 输出应包含：结论 + 拆分方案 + 关键假设 + 风险 + 下一步

---

## 关键原则

1. **MECE是拆分的黄金标准**：子问题必须互不重叠且共同穷尽。原因：重叠导致重复工作和冲突；遗漏导致最终方案不完整。
2. **接口先于实现**：在动手解决子问题之前，必须先定义清楚子问题之间的接口。原因：接口不清是拆分失败的第一大原因——各子问题实现完后发现"拼不起来"。
3. **递归终止条件必须有**：明确什么情况下不再拆分。原因：无限递归不仅浪费资源，还会让简单问题被过度设计。
4. **耦合度决定拆分质量**：好的拆分让子问题之间的耦合最小化。原因：高耦合子问题之间的沟通成本会抵消拆分带来的并行收益。
5. **组合不等于相加**：子问题独立正确 ≠ 组合后一定正确。原因：组合过程本身就是复杂度的新来源——接口兼容性、边界情况、时序问题。

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
- [ ] 子问题定义是否满足MECE原则？是否遗漏或重叠？
- [ ] 子问题之间的接口是否被明确定义？接口是否清晰可验证？
- [ ] 递归终止条件是否被设定？是否所有子问题都有终止路径？
- [ ] 依赖关系图是否完整？串行和并行路径是否被正确识别？
- [ ] 组合策略是否被验证？是否考虑了组合损耗？
- [ ] 合并结果是否完整覆盖了原始问题的所有需求？
- [ ] 输出具体可执行，不含模糊建议（如"拆开做"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [reductionism](../reductionism/SKILL.md) | 前置/并行 | 还原论提供"整体可拆为部分"的哲学基础，分治思维提供可操作的拆分方法 |
| [algorithmic-thinking](../algorithmic-thinking/SKILL.md) | 后置 | 分治思维拆问题，算法思维设计解法的精确步骤 |
| [system-thinking](../systems-thinking/SKILL.md) | 互补 | 系统思维关注拆开后子问题之间的交互和涌现，避免分治忽视整体 |
| [recursive-thinking](../recursive-thinking/SKILL.md) | 并行 | 递归是分治的核心实现机制——子问题结构与原问题相同 |

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

1. Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2009). *Introduction to Algorithms* (3rd ed.). MIT Press. Chapter 4: Divide-and-Conquer.
2. Knuth, D. E. (1997). *The Art of Computer Programming, Volume 1: Fundamental Algorithms* (3rd ed.). Addison-Wesley.
3. Pólya, G. (1945). *How to Solve It*. Princeton University Press. (问题分解策略的经典论述)
4. Simon, H. A. (1962). "The architecture of complexity." *Proceedings of the American Philosophical Society*, 106(6), 467-482. (层级分解与复杂系统)
5. Minsky, M. (1986). *The Society of Mind*. Simon & Schuster. (智能系统如何通过分解和协调实现复杂行为)

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
