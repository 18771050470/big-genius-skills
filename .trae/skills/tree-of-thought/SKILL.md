---
name: tree-of-thought
description: |
  触发：当面对需要探索、战略前瞻或初始决策至关重要的复杂问题时；常见信号包括"多种方案"、"探索可能性"、"最优路径"、"决策树"、"分支分析"、"游戏/搜索问题"。
  不触发：当问题有明确的单一路径解、当探索成本过高、当时间或计算资源受限时。
  Invoke when facing complex problems requiring exploration, strategic lookahead, or where initial decisions are pivotal.
  Do NOT invoke when the problem has a clear single-path solution, when exploration costs are prohibitive, or when time/compute resources are limited.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["chain-of-thought", "probabilistic-thinking", "decision-tree", "second-order-thinking"]
---

# 思维树推理 (Tree-of-Thought)

## 核心定义

将推理过程建模为树状搜索结构，通过主动探索多条思维路径、自我评估中间状态、前瞻与回溯，实现深思熟虑的问题解决范式。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充搜索空间边界或评估标准
- **发现矛盾**：停止当前分支探索，标记矛盾点，尝试其他分支
- **提前终止**：若某分支已找到满意解或确认某分支不可行，可提前终止该分支探索

---

## 思考流程

### Step 1: 问题空间界定

- 明确问题的初始状态和目标状态
- 界定搜索空间的边界（有限 vs 无限）
- 识别可能的行动/决策点（分支节点）
- 确定评估标准（什么算"好"的解）

---

### Step 2: 生成候选思维节点

- 从当前状态出发，生成所有可能的下一步（候选思维）
- 每个候选代表一个潜在的推理方向或决策选择
- 确保候选的多样性和覆盖度
- 标注每个候选的初步可行性

---

### Step 3: 状态评估与选择

- 对每个候选节点进行价值评估
- 使用启发式函数或自我评估判断前景
- 选择最有希望的节点进行深入探索
- 记录选择依据和置信度

---

### Step 4: 前瞻与回溯

- **前瞻（Lookahead）**：模拟多步后的可能结果
- 评估当前路径的长期潜力
- **回溯（Backtrack）**：当路径进入死胡同或价值低于预期
- 返回上一节点，尝试其他分支
- 记录已探索路径和结论

---

### Step 5: 迭代搜索与剪枝

- 持续迭代：生成 → 评估 → 选择 → 前瞻/回溯
- 对明显劣于当前最优解的分支进行剪枝
- 平衡探索（exploration）与利用（exploitation）
- 设置搜索深度和广度限制

---

### Step 6: 最优路径提取

- 从根节点到最优叶节点提取完整路径
- 验证路径的连贯性和正确性
- 总结为什么选择这条路径
- 输出应包含：最优解 + 路径说明 + 被舍弃的备选 + 评估依据

---

## 关键原则

1. **主动探索**：不满足于第一条可行路径，主动寻找更优解。原因：局部最优不等于全局最优，探索可能发现意想不到的更好方案。

2. **价值评估**：每个节点都必须有明确的价值评估。原因：无评估的选择是盲目的，评估使搜索有方向性。

3. **灵活回溯**：当路径前景不佳时果断回溯，不固执。原因：沉没成本谬误会导致在错误路径上浪费资源。

4. **平衡广深**：在广度和深度之间取得平衡。原因：过深可能陷入局部最优，过广可能错过优质深度解。

5. **记录轨迹**：完整记录探索轨迹，包括成功和失败路径。原因：避免重复探索，为后续决策提供参考。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**思维树特有关键检查项**：

- [ ] **是否生成了多个候选节点？** 还是只有单一路径？
- [ ] **每个节点是否有明确的价值评估？** 评估标准是什么？
- [ ] **是否进行了前瞻分析？** 模拟了多步后的结果吗？
- [ ] **是否执行了必要的回溯？** 当路径不佳时是否及时止损？
- [ ] **最终路径是否经过与其他路径的比较？** 为什么是最优？
- [ ] **搜索空间是否被合理界定？** 有无遗漏重要分支？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [chain-of-thought](../thinking/chain-of-thought/SKILL.md) | 基础 | ToT是CoT的扩展，当单一路径不够时使用ToT |
| [decision-tree](../thinking/decision-tree/SKILL.md) | 并行 | 决策树提供结构化框架，ToT增加动态评估和回溯 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 在节点评估时量化各分支的成功概率 |
| [second-order-thinking](../thinking/second-order-thinking/SKILL.md) | 前置 | 前瞻分析时考虑二阶、三阶后果 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Yao, S., Yu, D., Zhao, J., Shafran, I., Griffiths, T. L., Cao, Y., & Narasimhan, K. (2023). Tree of Thoughts: Deliberate Problem Solving with Large Language Models. *Advances in Neural Information Processing Systems*, 36.
2. Long, J. (2023). Large Language Model Guided Tree-of-Thought. *arXiv preprint arXiv:2305.08291*.
3. Hao, S., Gu, Y., Ma, H., Hong, J. J., Wang, Z., Wang, D. Z., & Hu, Z. (2023). Reasoning with Language Model is Planning with World Model. *arXiv preprint arXiv:2305.14992*.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
