---
name: affect-heuristic
description: |
  触发：当需要评估判断是否受情感反应影响、需要识别情感替代理性分析的偏差、需要纠正风险-收益评估时调用；常见信号包括"感觉不对"、"直觉告诉我"、"这个让我很不舒服"。
  不触发：当只需描述情感反应、无需理性分析时；当情感反应确实提供有效信号时（经实证验证）；当只需定性评估、无需量化分析时。
  Invoke when needing to evaluate whether judgments are affected by affective responses, identify affect replacing rational analysis, or correct risk-benefit assessments.
  Do NOT invoke when only describing affective responses without rational analysis, when affective responses truly provide valid signals (empirically verified), or when only qualitative assessment is needed without quantitative analysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["availability-bias", "empathy-gap", "dual-process-thinking", "framing-effect"]
---

# 情感启发式思维（Affect Heuristic Thinking）

## 核心定义

人们用情感反应（好感/恶感）替代理性分析来评估风险和收益。Slovic等人在2002年提出：情感标记使人们快速判断，但导致风险-收益负相关偏差（高好感=低风险高收益，高恶感=高风险低收益）。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充客观风险-收益数据、历史案例和理性分析框架
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别情感启发式影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别情感信号

- 是否出现"感觉不对"、"直觉告诉我"、"这个让我很不舒服"等表述？
- 是否用情感反应替代理性分析？
- 是否出现风险-收益负相关？（好感=低风险高收益，恶感=高风险低收益）
- 情感反应强度如何？（1-10评分）

---

### Step 2: 评估情感影响

- 情感反应来自什么？（外观、名称、过往经验、他人影响）
- 情感反应是否合理？（有客观依据 vs 纯粹情绪）
- 情感如何影响风险感知？（放大/缩小）
- 情感如何影响收益预期？（放大/缩小）

---

### Step 3: 分析风险-收益偏差

- 客观风险是多少？（数据支持）
- 客观收益是多少？（数据支持）
- 情感标记如何扭曲风险-收益评估？
- 风险-收益是否真的负相关？（客观分析）

---

### Step 4: 校正情感偏差

- 分离情感和理性分析
- 使用客观数据替代情感判断
- 计算风险-收益期望值
- 设计决策检查清单：情感反应≠理性结论

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **情感≠理性**：情感反应快速但常错，理性分析慢但准确。原因：情感系统进化用于快速威胁检测，不适合复杂风险评估。
2. **风险-收益负相关是偏差**：客观世界中风险和收益常正相关（高风险高收益）。原因：情感标记使好感事物被低估风险高估收益，恶感事物被高估风险低估收益。
3. **情感标记持久**：一旦形成情感标记，很难被新证据改变。原因：情感记忆比理性记忆更持久，确认偏误强化情感标记。
4. **分离分析是解药**：先识别情感反应，再用客观数据重新评估。原因：分离使情感不污染理性分析，客观数据校正情感偏差。

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
- [ ] **情感启发式特供**：是否识别了"感觉不对"、"直觉告诉我"等情感信号？情感强度是否被量化（1-10评分）？
- [ ] **情感启发式特供**：是否追溯了情感反应的真实来源（外观、名称、过往经验、他人影响）？而非简单接受"直觉"？
- [ ] **情感启发式特供**：是否检测了风险-收益负相关偏差？好感事物是否被系统性地低估风险/高估收益？
- [ ] **情感启发式特供**：是否用客观数据替代了情感判断？分离情感和理性分析的操作是否具体可执行？
- [ ] **情感启发式特供**：是否评估了情感标记的持久性？是否设计了打破情感标记固化的机制？
- [ ] **情感启发式特供**：是否区分了"有效情感信号"（经实证验证）和"噪声情感反应"？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"理性分析"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差回忆生动事件，情感启发式用情感评估风险 |
| [empathy-gap](../thinking/empathy-gap/SKILL.md) | 并行 | 共情差距使预测情感反应困难，情感启发式用当前情感判断 |
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 前置 | 双系统理论解释情感（系统1）vs理性（系统2） |
| [framing-effect](../thinking/framing-effect/SKILL.md) | 并行 | 框架效应影响情感反应，情感启发式用情感判断 |

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

1. Slovic, P., Finucane, M. L., Peters, E., & MacGregor, D. G. (2002). The affect heuristic. In *Heuristics and Biases: The Psychology of Intuitive Judgment* (pp. 397-420). Cambridge University Press.
2. Finucane, M. L., Alhakami, A., Slovic, P., & Johnson, S. M. (2000). Risk as feelings: A test of the affect heuristic. *Journal of Behavioral Decision Making*, 13(1), 1-17.
3. Alhakami, A. S., & Slovic, P. (1994). A psychological study of the inverse relationship between perceived risk and perceived benefit. *Risk Analysis*, 14(6), 1085-1096.
4. Västfjäll, D., Slovic, P., Mayorga, M., & Peters, E. (2014). Affect is the key: The role of affective responses in the affect heuristic. *Judgment and Decision Making*, 9(4), 345-363.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
