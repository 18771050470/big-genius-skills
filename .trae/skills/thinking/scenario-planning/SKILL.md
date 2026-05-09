---
name: scenario-planning
description: |
  触发：当需要为不确定的未来做规划、需要识别关键不确定性因素、需要设计多路径应对方案时调用；常见信号包括"未来会怎样"、"如果X发生我们怎么办"、"如何为不确定性做准备"。
  不触发：当未来高度可预测时；当只需单一方案、无需备选时；当时间极紧迫、只需应急计划时。
  Invoke when needing to plan for uncertain futures, identify key uncertainty factors, or design multi-path response strategies.
  Do NOT invoke when the future is highly predictable, when only a single plan is needed without alternatives, or when time is extremely tight and only contingency plans are needed.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["probabilistic-thinking", "second-order-thinking", "counterfactual-thinking", "margin-of-safety"]
---

# 情景规划思维（Scenario Planning）

## 核心定义

构建多个合理的未来情景（不是预测），为每个情景设计应对策略，提高组织在不确定环境中的适应力。核心不是预测哪个情景会发生，而是让组织准备好应对多种可能。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充关键不确定性因素、时间跨度和决策灵活性
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已构建2-3个核心情景且应对策略清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别关键驱动因素

- 列出影响未来的关键因素：技术、市场、法规、社会、经济
- 区分确定因素（高概率发生）和不确定因素（可能发生也可能不发生）
- 确定因素作为情景的共同背景，不确定因素作为情景的区分维度
- 选择2个最关键的不确定因素作为情景矩阵的轴

---

### Step 2: 构建情景矩阵

- 用2个关键不确定因素构建2×2矩阵，产生4个情景
- 每个情景应该是合理的（不是极端假设）、有区分度的
- 为每个情景命名并描述核心特征
- 避免"好/中/差"三情景模式（太线性），追求真正不同的未来

---

### Step 3: 描述每个情景

- 每个情景的故事线：从现状到该情景的演变路径
- 情景中的关键事件和转折点
- 每个情景对组织的影响：机会和威胁
- 标注每个情景的触发信号：如何知道这个情景正在成为现实？

---

### Step 4: 设计应对策略

- 通用策略：在所有情景下都有效的策略（无悔策略）
- 情景专属策略：只在特定情景下有效的策略
- 期权策略：保持灵活性，等情景明朗后再决定
- 评估每种策略的成本、收益和灵活性

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **情景不是预测**：情景规划的目的是准备，不是预测。原因：未来不可预测，但可以被准备。
2. **2×2矩阵是最优结构**：2个不确定因素产生4个情景，足够覆盖不确定性又不至于过多。原因：超过4个情景会导致分析瘫痪，少于4个情景覆盖不足。
3. **触发信号比概率更重要**：关注如何识别情景正在成为现实，而非估计概率。原因：概率估计在高度不确定时不可靠，触发信号可操作。
4. **无悔策略是核心**：在所有情景下都有效的策略是最有价值的。原因：无论未来如何，这些策略都产生正向回报。

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
- [ ] 关键驱动因素是否区分了确定和不确定？
- [ ] 情景矩阵是否基于2个最关键的不确定因素？
- [ ] 每个情景是否合理且有区分度？
- [ ] 是否为每个情景设计了触发信号？
- [ ] 是否识别了无悔策略？
- [ ] 输出具体可执行，不含模糊建议（如"做好准备"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维量化情景可能性，情景规划构建情景框架 |
| [second-order-thinking](../thinking/second-order-thinking/SKILL.md) | 并行 | 二阶思维推演情景中的连锁反应 |
| [counterfactual-thinking](../thinking/counterfactual-thinking/SKILL.md) | 并行 | 反事实思维评估历史决策在不同情景下的表现 |
| [margin-of-safety](../thinking/margin-of-safety/SKILL.md) | 并行 | 安全边际为最坏情景提供缓冲 |

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

1. Schoemaker, P. J. H. (1995). Scenario planning: A tool for strategic thinking. *Sloan Management Review*, 36(2), 25-40.
2. Schwartz, P. (1991). *The Art of the Long View: Planning for the Future in an Uncertain World*. Wiley.
3. Wack, P. (1985). Scenarios: Uncharted waters ahead. *Harvard Business Review*, 63(5), 72-89.
4. Ringland, G. (2006). *Scenario Planning: Managing for the Future* (2nd ed.). Wiley.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
