---
name: reactance
description: |
  触发：当需要评估是否因自由受限而产生抗拒、需要识别"你越说我越不做"偏差、需要设计说服策略时调用；常见信号包括"别告诉我该怎么做"、"我偏不"、"这是我的选择"。
  不触发：当只需描述抗拒行为、无需分析自由威胁时；当限制确实合理、抗拒非理性时（经自主性验证）；当只需记录反应、无需设计策略时。
  Invoke when needing to evaluate whether resistance is caused by freedom restriction, identify "the more you tell me the less I'll do" bias, or design persuasion strategies.
  Do NOT invoke when only describing resistance behavior without analyzing freedom threat, when restriction is truly reasonable and resistance is irrational (verified by autonomy assessment), or when only recording reactions without designing strategies.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["autonomy", "persuasion", "status-quo-bias", "action-bias"]
---

# 心理抗拒思维（Reactance Thinking）

## 核心定义

人们因感知自由受威胁而产生抗拒，做相反行为。Brehm在1966年提出：当自由被限制或威胁时，人们产生心理抗拒，动机恢复自由。这使禁止增加吸引力，强制产生反效果。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充自由威胁感知、历史抗拒反应和替代选择可用性
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别心理抗拒影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别抗拒信号

- 是否出现"别告诉我该怎么做"、"我偏不"、"这是我的选择"等表述？
- 是否因被要求而做相反行为？
- 是否感知自由受威胁？
- 禁止是否增加吸引力？

---

### Step 2: 评估自由威胁

- 哪些自由被威胁？（选择、行动、表达）
- 威胁程度如何？（强制vs建议）
- 替代选择是否可用？
- 抗拒强度与威胁程度关系？

---

### Step 3: 分析抗拒机制

- 自由威胁：感知选择权被限制
- 动机恢复：产生恢复自由的动机
- 反向行为：做被禁止的事
- 态度极化：对被禁止事物评价更高

---

### Step 4: 校正抗拒反应

- 提供选择：保留自主决策空间
- 框架转换：从"必须"到"可以选择"
- 减少强制：用建议替代命令
- 预先警告：告知可能被操纵

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **自由威胁触发抗拒**：感知选择权被限制产生抗拒。原因：人类有自主需求，自由受威胁时产生恢复动机。
2. **禁止增加吸引力**：被禁止的事物更有吸引力。原因：禁止使事物成为自由象征，抗拒使评价更高。
3. **强制产生反效果**：强制使人们做相反行为。原因：强制触发抗拒动机，人们通过反向行为证明自主。
4. **提供选择是解药**：保留自主决策空间。原因：选择满足自主需求，减少抗拒，增加合作。

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
- [ ] 是否识别了心理抗拒信号？
- [ ] 是否评估了自由威胁程度？
- [ ] 是否分析了抗拒驱动机制？
- [ ] 是否提供了选择空间？
- [ ] 是否使用建议替代命令？
- [ ] 输出具体可执行，不含模糊建议（如"减少强制"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [autonomy](../thinking/autonomy/SKILL.md) | 前置 | 自主性解释为何自由威胁触发抗拒 |
| [persuasion](../thinking/persuasion/SKILL.md) | 并行 | 说服策略需要考虑抗拒反应 |
| [status-quo-bias](../thinking/status-quo-bias/SKILL.md) | 并行 | 现状偏差偏好当前状态，抗拒使反对改变 |
| [action-bias](../thinking/action-bias/SKILL.md) | 并行 | 行动偏差偏好行动，抗拒使做相反行动 |

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

1. Brehm, J. W. (1966). *A Theory of Psychological Reactance*. Academic Press.
2. Brehm, S. S., & Brehm, J. W. (1981). *Psychological Reactance: A Theory of Freedom and Control*. Academic Press.
3. Miron, A. M., & Brehm, J. W. (2006). Reactance theory - 40 years later. *Zeitschrift für Sozialpsychologie*, 37(1), 9-18.
4. Rains, S. A. (2013). Psychological reactance and persuasive health communication: A meta-analysis. *Human Communication Research*, 39(2), 133-160.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
