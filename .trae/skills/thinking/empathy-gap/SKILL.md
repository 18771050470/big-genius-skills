---
name: empathy-gap
description: |
  触发：当需要评估是否低估情绪状态对行为的影响、需要预测不同情绪状态下的决策差异、需要识别冷热共情差距时调用；常见信号包括"我当时怎么会那样"、"冷静时觉得简单"、"无法理解他为什么那样做"。
  不触发：当只需描述情绪状态、无需预测行为时；当决策者情绪状态稳定、无显著变化时；当只需分析理性决策、无需考虑情绪因素时。
  Invoke when needing to evaluate whether emotional state impact on behavior is underestimated, predict decision differences across emotional states, or identify hot-cold empathy gaps.
  Do NOT invoke when only describing emotional states without predicting behavior, when decision maker emotional state is stable without significant changes, or when only analyzing rational decisions without considering emotional factors.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["affect-heuristic", "projection-bias", "dual-process-thinking", "framing-effect"]
---

# 共情差距思维（Empathy Gap Thinking）

## 核心定义

人们低估情绪状态对行为和决策的影响。Loewenstein在1996年提出"冷热共情差距"：冷静状态时难以想象热状态（愤怒、饥饿、性冲动）下的行为，热状态时难以回忆冷静状态下的理性判断。这导致预测自己和他人行为时系统性偏差。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充当前情绪状态、历史情绪变化数据和行为记录
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别共情差距影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别共情差距信号

- 是否出现"我当时怎么会那样"、"冷静时觉得简单"、"无法理解他为什么那样做"等表述？
- 是否在冷静状态下预测热状态行为？
- 是否在热状态下回忆冷静状态判断？
- 是否低估了情绪对行为的影响？

---

### Step 2: 评估情绪状态影响

- 当前情绪状态是什么？（冷静/热）
- 情绪强度如何？（1-10评分）
- 情绪如何影响风险偏好？
- 情绪如何影响时间偏好？（即时满足 vs 延迟满足）

---

### Step 3: 分析冷热状态差异

- 冷静状态：理性、长远、自控力强
- 热状态：冲动、即时、自控力弱
- 两种状态下的偏好差异有多大？
- 历史数据：冷静时承诺 vs 热状态行为

---

### Step 4: 设计共情校正

- 使用历史数据：过去热状态下的实际行为
- 预设承诺：冷静时设置热状态约束（如自动储蓄）
- 情绪标记：识别情绪变化信号，提前干预
- 双状态规划：为冷静和热状态分别制定计划

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **冷热状态是不同人**：冷静和热状态下的偏好和行为差异巨大，如同两个人。原因：情绪状态改变大脑激活区域，热状态激活边缘系统，冷静状态激活前额叶。
2. **冷静时过度自信**：冷静时高估自己在热状态下的自控力。原因：冷静状态无法模拟热状态的情绪强度，导致"我不会那样"的错觉。
3. **热状态遗忘理性**：热状态下难以回忆冷静状态下的理性判断。原因：情绪主导时，理性记忆被抑制，即时满足成为唯一焦点。
4. **预设承诺是解药**：冷静时设置热状态约束，绕过共情差距。原因：预设承诺在冷静时生效，不依赖热状态下的自控力。

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
- [ ] 是否识别了共情差距信号？
- [ ] 是否评估了当前情绪状态影响？
- [ ] 是否分析了冷热状态差异？
- [ ] 是否设计了共情校正方案？
- [ ] 是否使用预设承诺机制？
- [ ] 输出具体可执行，不含模糊建议（如"控制情绪"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [affect-heuristic](../thinking/affect-heuristic/SKILL.md) | 前置 | 情感启发式解释情绪如何替代理性判断 |
| [projection-bias](../thinking/projection-bias/SKILL.md) | 并行 | 投射偏差将自己的当前状态投射到未来 |
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 前置 | 双系统理论解释冷热状态的认知机制 |
| [framing-effect](../thinking/framing-effect/SKILL.md) | 并行 | 框架效应与情绪状态都影响决策 |

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

1. Loewenstein, G. (1996). Out of control: Visceral influences on behavior. *Organizational Behavior and Human Decision Processes*, 65(3), 272-292.
2. Loewenstein, G., Nagin, D., & Paternoster, R. (1997). The effect of sexual arousal on men's willingness to engage in risky sexual behavior. *Journal of Research in Crime and Delinquency*, 34(3), 291-318.
3. Nordgren, L. F., van der Pligt, J., & van den Bos, K. (2007). The hot-cold empathy gap: The role of visceral states in social judgment. *Psychological Science*, 18(10), 873-878.
4. Sayette, M. A., et al. (2000). Effects of alcohol on cigarette craving: The role of the hot-cold empathy gap. *Experimental and Clinical Psychopharmacology*, 8(4), 445-453.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
