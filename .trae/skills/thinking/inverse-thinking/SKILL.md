---
name: inverse-thinking
description: |
  触发：当需要识别失败路径、规避风险、从反面解决问题时调用；常见信号包括"怎样会搞砸"、"如何避免失败"、"反过来想会怎样"。
  不触发：当只需正向规划成功路径时；当问题本身已是从反面定义（如"如何防止X"）时；当时间极紧迫、只需应急方案时。
  Invoke when needing to identify failure paths, avoid risks, or solve problems from the opposite direction.
  Do NOT invoke when only forward planning for success is needed, when the problem is already defined inversely, or when time is extremely tight and only emergency plans are needed.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["red-team-thinking", "second-order-thinking", "premortem", "boundary-thinking"]
---

# 逆向思维（Inverse Thinking）

## 核心定义

不直接思考"如何成功"，而是思考"什么会导致失败"，然后避免这些失败路径。Carl Jacobi名言："反过来想，总是反过来想。"

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充目标、约束和历史失败案例
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别关键失败路径且规避方案明确，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 定义成功目标

- 明确要达成的目标或要解决的问题
- 定义成功的标准：什么算"成功"？
- 标注约束条件：时间、资源、法规等
- 这是逆向思维的起点，知道正向目标才能反向推导

---

### Step 2: 逆向推导失败路径

- 什么会导致目标无法达成？
- 列出所有可能的失败模式：技术失败、市场失败、团队失败、资金断裂等
- 使用"事前验尸"方法：假设项目已失败，倒推失败原因
- 标注每条失败路径的可能性和影响程度

---

### Step 3: 识别关键失败因素

- 哪些失败路径可能性最高？
- 哪些失败路径影响最严重？
- 是否存在"一票否决"因素（一旦发生即致命）？
- 按可能性和影响程度排序失败因素

---

### Step 4: 设计规避策略

- 对每个关键失败因素，设计预防措施
- 预防措施的成本 vs 失败损失的期望值
- 识别"不做清单"：哪些行为必须禁止
- 设计早期预警信号：如何知道失败路径正在被触发

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **避免愚蠢比追求聪明更可靠**：Charlie Munger说"我只想知道我会死在哪里，这样我就永远不去那里"。原因：避免已知失败路径的确定性高于找到成功路径的确定性。
2. **事前验尸优于事后复盘**：在决策前假设失败并倒推原因。原因：事前没有沉没成本偏见，能更客观识别风险。
3. **逆向不是悲观**：逆向思维是风险识别工具，不是消极态度。原因：识别风险后才能有针对性地管理风险，而非回避所有行动。
4. **正向和逆向结合**：逆向识别失败路径，正向规划成功路径。原因：只做逆向会过度保守，只做正向会忽视风险。

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
- [ ] 失败路径是否被穷举？是否有遗漏的关键失败模式？
- [ ] 是否使用了"事前验尸"方法？
- [ ] 失败因素是否按可能性和影响排序？
- [ ] 规避策略的成本是否被量化？
- [ ] 是否设计了早期预警信号？
- [ ] 输出具体可执行，不含模糊建议（如"注意风险"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [red-team-thinking](../thinking/red-team-thinking/SKILL.md) | 并行 | 红队思维模拟攻击者视角，逆向思维从失败路径倒推 |
| [second-order-thinking](../thinking/second-order-thinking/SKILL.md) | 并行 | 二阶思维推演后果，逆向思维从失败后果倒推原因 |
| [boundary-thinking](../thinking/boundary-thinking/SKILL.md) | 并行 | 边界思维识别系统极限，逆向思维识别超越极限的后果 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维量化失败可能性 |

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

1. Jacobi, C. G. J. (19th century). "Man muss immer umkehren." (Attributed)
2. Munger, C. T. (1994). *The Worldly Wisdom Speech*. USC Law School.
3. Klein, G. (2007). Performing a project premortem. *Harvard Business Review*, 85(9), 18-19.
4. Taleb, N. N. (2007). *The Black Swan*. Random House.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
