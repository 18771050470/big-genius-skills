---
name: game-theory-thinking
description: |
  触发：当决策涉及多个理性参与者、各方利益存在冲突或合作、需要考虑对手反应时调用；常见信号包括"如果对方也这么做会怎样"、"怎么防止被利用"、"什么情况下会达成合作"。
  不触发：当决策只涉及单方、无外部参与者时；当参与者行为完全随机、无策略性时；当只需优化自身收益、无需考虑互动时。
  Invoke when decisions involve multiple rational agents, conflicting or cooperative interests, or when opponent reactions must be considered.
  Do NOT invoke when decisions involve only a single party, when agent behavior is completely random without strategy, or when only self-optimization is needed without considering interactions.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["inverse-thinking", "probabilistic-thinking", "decision-tree", "second-order-thinking"]
---

# 博弈论思维（Game Theory Thinking）

## 核心定义

在多方互动场景中，分析各参与者的策略选择、收益结构和均衡状态，找到最优策略或预测系统走向。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充参与者、收益矩阵或规则信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已找到明确纳什均衡且策略清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别博弈参与者

- 列出所有参与决策的主体（个人、组织、系统）
- 明确每个参与者的目标函数（他们想要什么）
- 判断参与者是否理性（是否会追求自身利益最大化）
- 识别信息不对称：谁知道什么，谁不知道什么

---

### Step 2: 定义策略空间

- 每个参与者有哪些可选策略？
- 策略是离散选择还是连续变量？
- 是否存在占优策略（无论对手怎么做都最优）？
- 策略之间是否存在依赖关系

---

### Step 3: 构建收益矩阵

- 量化每个策略组合下各参与者的收益/损失
- 收益可以是金钱、效用、市场份额等可比较的量
- 标注零和博弈（一方所得即另一方所失）还是非零和博弈
- 识别外部性：某参与者的行为对第三方的影响

---

### Step 4: 求解均衡

- 寻找纳什均衡：每个参与者在给定对手策略下的最优反应
- 检查是否存在多个均衡（协调博弈）或无纯策略均衡
- 分析重复博弈下的合作可能性（触发策略、声誉机制）
- 评估均衡的稳定性：小扰动是否会导致系统偏离

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **理性假设是起点而非终点**：先假设各方理性，再考虑行为偏差。原因：理性模型提供基准，行为偏差在此基础上修正。
2. **均衡不一定是好结果**：纳什均衡可能是帕累托次优（如囚徒困境）。原因：个体理性不等于集体理性，需要机制设计来改善。
3. **信息结构决定博弈类型**：完全信息 vs 不完全信息，同时行动 vs 序贯行动。原因：不同信息结构对应不同的求解方法。
4. **重复博弈改变一切**：单次博弈的均衡在重复博弈中可能不成立。原因：未来收益的贴现使合作成为可能。

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
- [ ] 所有参与者是否被完整识别？是否有隐藏参与者？
- [ ] 收益矩阵是否量化？收益单位是否一致？
- [ ] 均衡是否被验证（每个参与者都在最优反应）？
- [ ] 是否考虑了重复博弈 vs 单次博弈的差异？
- [ ] 是否评估了非理性行为的可能性？
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [inverse-thinking](../thinking/inverse-thinking/SKILL.md) | 并行 | 逆向思维从对手视角思考，博弈论提供结构化分析框架 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 不完全信息博弈需要概率分布描述对手类型 |
| [decision-tree](../thinking/decision-tree/SKILL.md) | 前置 | 序贯博弈可用决策树建模 |
| [second-order-thinking](../thinking/second-order-thinking/SKILL.md) | 并行 | 二阶思维关注间接后果，博弈论关注策略互动 |

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

1. von Neumann, J., & Morgenstern, O. (1944). *Theory of Games and Economic Behavior*. Princeton University Press.
2. Nash, J. F. (1950). Equilibrium points in n-person games. *PNAS*, 36(1), 48-49.
3. Axelrod, R. (1984). *The Evolution of Cooperation*. Basic Books.
4. Osborne, M. J. (2004). *An Introduction to Game Theory*. Oxford University Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
