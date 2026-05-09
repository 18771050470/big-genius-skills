---
name: six-thinking-hats
description: |
  触发：当团队讨论陷入僵局、需要从多个角度审视同一问题、避免思维片面或群体极化时；当个人需要系统性地切换思维模式以全面分析问题时；常见信号包括"我们换个角度想想""不要只关注风险也要看机会""大家争论不下，各执一词"。
  不触发：当问题已有明确答案只需执行时；当时间紧迫无法容忍多角度思考时；当参与者无法理解"平行思考"概念时。
  Invoke when group discussion is stuck, when multiple perspectives are needed, or when avoiding one-sided thinking.
  Do NOT invoke when the answer is clear and only execution is needed, when time constraints prohibit multi-angle thinking, or when participants cannot grasp "parallel thinking".
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["lateral-thinking", "creative-thinking", "critical-thinking", "pros-and-cons-analysis"]
---

# 六顶思考帽（Six Thinking Hats）

## 核心定义

由Edward de Bono于1985年提出的平行思维工具，通过强制切换六种思维模式（白帽事实、红帽情感、黑帽风险、黄帽收益、绿帽创意、蓝帽流程），避免争论和思维片面，实现全面而有序的思考。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充问题背景、参与者和时间约束
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某顶帽子已得出明确结论且其他帽子无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 [颜色] Hat"

---

## 思考流程

### Step 1: 白帽思考（事实与数据）

- 我们已知什么？有哪些客观数据和事实？
- 我们还需要什么信息？信息缺口在哪里？
- 区分"已知事实"" believed facts"和"未知"
- 禁止：解读、推测、观点、情感——只陈述客观信息

### Step 2: 红帽思考（情感与直觉）

- 我对这个问题的直觉感受是什么？（不用解释原因）
- 团队成员的情绪反应是什么？
- 是否有" gut feeling "觉得哪里不对？
- 禁止：论证、解释、合理化——只表达感受

### Step 3: 黑帽思考（风险与批判）

- 这个方案哪里可能出错？
- 最坏情况是什么？概率和后果如何？
- 存在什么障碍和限制？
- 为什么这个方案可能行不通？
- 禁止：只找茬不建设——批判是为了改进，不是否定

### Step 4: 黄帽思考（收益与乐观）

- 这个方案的价值和好处是什么？
- 为什么这个方案值得做？
- 有哪些被忽略的机会和积极面？
- 即使困难，哪些部分仍然可行？
- 禁止：盲目乐观——收益必须基于事实，不是幻想

### Step 5: 绿帽思考（创意与替代）

- 还有什么完全不同的方法？
- 如何绕过黑帽识别的障碍？
- 能否修改方案以保留黄帽收益同时消除黑帽风险？
- 引入随机刺激：如果必须用一个荒谬的方法，会是什么？
- 禁止：过早评判——创意阶段只发散不收敛

### Step 6: 蓝帽思考（流程与总结）

- 我们覆盖了所有帽子吗？有没有遗漏的角度？
- 各帽子的结论如何整合？
- 决策标准是什么？如何权衡收益与风险？
- 下一步行动：谁、做什么、何时完成？
- 标注每顶帽子的关键产出和优先级

### Step 7: 总结输出

- 整合六顶帽子的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **平行思维，不是辩论**：同一时刻所有人都戴同一顶帽子，不是有人支持有人反对。原因：辩论模式下人们捍卫立场而非寻找最佳方案，平行思维确保每个角度都被充分探索。
2. **帽子是角色，不是人**：一个人可以戴所有帽子，一个帽子可以被所有人戴。原因：避免"黑帽人总是唱反调"的标签化，让思考聚焦于角度而非个人。
3. **红帽给予情感合法性**：直觉和情感是有效信息，不需要立即合理化。原因：很多决策受情感驱动，压抑情感会导致隐性偏见；给情感表达空间反而能让后续思考更理性。
4. **绿帽需要荒谬的许可**：创意阶段必须允许看似愚蠢的想法，因为突破常来自荒谬。原因：大脑对合理陈述自动归类，只有荒谬才能迫使建立新连接（与水平思考的"Po"技术同源）。

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
- [ ] 白帽：是否区分了"已知事实"" believed facts"和"未知"？
- [ ] 红帽：是否允许了无需解释的情感表达？
- [ ] 黑帽：批判是否建设性？是否识别了具体风险而非笼统否定？
- [ ] 黄帽：收益是否基于事实？是否避免了盲目乐观？
- [ ] 绿帽：是否产生了至少一个突破性创意？是否允许了荒谬想法？
- [ ] 蓝帽：是否整合了所有帽子的结论？决策标准是否清晰？
- [ ] 是否避免了"帽子混淆"——在同一阶段混用不同思维模式？
- [ ] 输出具体可执行，不含模糊建议（如"综合考虑"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [lateral-thinking](../thinking/lateral-thinking/SKILL.md) | 关联 | 绿帽思考时调用水平思考技术生成创意 |
| [creative-thinking](../thinking/creative-thinking/SKILL.md) | 关联 | 绿帽阶段需要创造性思维发散 |
| [critical-thinking](../thinking/critical-thinking/SKILL.md) | 关联 | 黑帽阶段需要批判性思维识别风险 |
| [pros-and-cons-analysis](../thinking/pros-and-cons-analysis/SKILL.md) | 关联 | 黄帽+黑帽的组合类似于利弊分析，但六顶思考帽更全面 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | 思维模型的理论背景（可选） |

---

## 参考文献

1. de Bono, E. (1985). *Six Thinking Hats*. Little, Brown and Company.
2. de Bono, E. (1992). *Serious Creativity: Using the Power of Lateral Thinking to Create New Ideas*. Harper Business.
3. de Bono, E. (1999). *New Thinking for the New Millennium*. Viking.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
