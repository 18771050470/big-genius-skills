---
name: circle-of-influence-vs-concern
description: |
  触发：当需要区分可控与不可控因素、评估精力分配是否合理、识别被动反应模式时调用；常见信号包括"担心但无能为力"、"想改变但不知从何入手"、"被外部事件牵着走"、"焦虑但无行动"。
  不触发：当问题完全在可控范围内且无需区分时；当只需执行具体任务、无需精力分配思考时；当问题完全不可控且只需接受时。
  Invoke when needing to distinguish controllable from uncontrollable factors, evaluate energy allocation, or identify reactive patterns.
  Do NOT invoke when the problem is fully controllable, when only task execution is needed, or when the situation is entirely uncontrollable and only acceptance is required.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["proactive-thinking", "stoicism", "locus-of-control", "constraint-thinking"]
---

# 影响圈与关注圈思维（Circle of Influence vs. Concern Thinking）

## 核心定义

将关注点分为"影响圈"（可控）和"关注圈"（不可控），主动将精力聚焦于影响圈以扩大控制力，减少在关注圈中的被动消耗—— proactive 的人聚焦影响圈，reactive 的人被困在关注圈。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充当前焦虑/担忧的具体事项清单
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确所有事项的分类且行动方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 列出所有关注事项

- 将当前所有担忧、焦虑、关注的事项全部列出
- 不筛选、不评判，包括工作、健康、人际关系、社会事件等
- 标注每个事项的情绪强度（1-10分）
- 标注每个事项当前消耗的时间/精力比例

---

### Step 2: 分类到两个圈层

- **关注圈（Circle of Concern）**：你关心但无法控制的事项
  - 他人行为、天气、经济环境、过去的事件、他人的看法
- **影响圈（Circle of Influence）**：你可以直接或间接影响的事项
  - 自己的行为、思维方式、沟通方式、技能提升、习惯养成
- 对模糊事项进行追问："我能为此做什么具体行动？"

---

### Step 3: 评估精力分配比例

- 计算当前精力在关注圈 vs 影响圈的分配比例
- 识别"关注圈陷阱"：是否将 >50% 精力花在不可控事项上？
- 评估情绪成本：关注圈事项是否引发焦虑、愤怒、无力感？
- 评估机会成本：这些精力如果投入影响圈，可能产生什么收益？

---

### Step 4: 设计精力转移策略

- 对关注圈事项：练习接受、放下或设定" worry time"限制
- 对影响圈事项：制定具体行动计划
- 将"可间接影响"的事项从关注圈移至影响圈（通过改变自身行为影响他人）
- 设定每日/每周的"影响圈时间块"

---

### Step 5: 执行与反馈

- 执行影响圈内的行动计划
- 观察影响圈是否扩大（ proactive 行为自然扩大影响圈）
- 记录情绪变化：精力转移后焦虑水平是否下降？
- 定期重新评估分类（影响圈和关注圈是动态的）

---

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **影响圈是 proactive 的阵地**：将精力投入影响圈会产生正向循环，能力增强→影响扩大→更多掌控感。原因：关注自身行为是唯一能直接控制的变量，改变自身行为会间接影响周围环境。
2. **关注圈是 reactive 的陷阱**：过度关注不可控事项会产生负向循环，焦虑增加→判断力下降→影响圈缩小。原因：大脑将注意力资源消耗在无法行动的事项上，导致可用于实际行动的能量枯竭。
3. **影响圈可以扩大**：通过持续在影响圈内行动，个人能力和信誉积累，间接影响力自然扩展。原因：他人会响应你的行为改变，信任建立后你的建议和行动会被更多人接受。
4. **接受不是放弃**：对关注圈事项的接受是主动选择，不是被动认命。原因：接受释放心理能量，这些能量可以重新定向到影响圈的有效行动中。

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
- [ ] **影响圈特供**：是否列出了所有关注事项？是否标注了每个事项的情绪强度和精力消耗？
- [ ] **影响圈特供**：是否正确区分了关注圈（不可控）和影响圈（可控）？模糊事项是否经过"我能做什么？"测试？
- [ ] **影响圈特供**：是否评估了精力分配比例？是否识别了"关注圈陷阱"（>50%精力在不可控事项）？
- [ ] **影响圈特供**：是否为关注圈事项设计了"接受策略"（ worry time、放下练习）？是否为影响圈事项制定了具体行动计划？
- [ ] **影响圈特供**：是否考虑了"间接影响"路径？是否将可通过自身行为影响他人的事项移至影响圈？
- [ ] **影响圈特供**：是否设计了反馈机制？影响圈是否被设定为动态评估（定期重新分类）？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"保持积极"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [stoicism](../stoicism/SKILL.md) | 前置 | 斯多葛哲学提供"控制二分法"的理论基础，区分可控与不可控 |
| [proactive-thinking](../proactive-thinking/SKILL.md) | 并行 | 主动思维强调在影响圈内采取行动，而非被动反应 |
| [locus-of-control](../locus-of-control/SKILL.md) | 并行 | 控制点理论解释为何有人聚焦影响圈（内控型）有人被困关注圈（外控型） |
| [constraint-thinking](../constraint-thinking/SKILL.md) | 后置 | 约束思维帮助在影响圈内识别和利用可用资源 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | Covey的七个习惯理论基础 |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Covey, S. R. (1989). *The 7 Habits of Highly Effective People: Powerful Lessons in Personal Change*. Simon & Schuster.
2. Rotter, J. B. (1966). Generalized expectancies for internal versus external control of reinforcement. *Psychological Monographs: General and Applied*, 80(1), 1-28.
3. Epictetus. (c. 135 A.D.). *Enchiridion* (Handbook). Translated by George Long.
4. Seligman, M. E. P. (2006). *Learned Optimism: How to Change Your Mind and Your Life*. Vintage Books.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
