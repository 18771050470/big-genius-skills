---
name: spotlight-effect
description: |
  触发：当需要评估是否高估他人对自己的关注度、需要识别"所有人都在看我"偏差、需要校正社交焦虑时调用；常见信号包括"大家都在看我"、"这太丢人了"、"别人肯定注意到了"。
  不触发：当只需描述社交场景、无需评估关注度时；当确实处于焦点位置、经客观验证时；当只需记录感受、无需分析实际关注时。
  Invoke when needing to evaluate whether attention from others is overestimated, identify "everyone is looking at me" bias, or correct social anxiety.
  Do NOT invoke when only describing social scenarios without evaluating attention degree, when truly in focal position (verified objectively), or when only recording feelings without analyzing actual attention.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["transparency-illusion", "self-serving-bias", "availability-bias", "anchoring-effect"]
---

# 聚光灯效应思维（Spotlight Effect Thinking）

## 核心定义

人们高估他人对自己的关注程度。Gilovich等人在2000年实验证明：穿尴尬T恤的人估计50%人注意到，实际只有20%。人们自己是自己世界的中心，但他人并非如此。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充实际关注度数据、他人反馈和社交场景客观信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别聚光灯效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别聚光灯信号

- 是否出现"大家都在看我"、"这太丢人了"、"别人肯定注意到了"等表述？
- 是否高估他人对自己的关注？
- 是否过度担心他人评价？
- 是否将自己视为场景中心？

---

### Step 2: 评估关注程度

- 实际有多少人注意到？（客观数据）
- 他人注意力主要在哪里？（他人关注自己事务）
- 关注度是否随时间快速衰减？（注意力转移）
- 自己关注度 vs 他人关注度差异？

---

### Step 3: 分析聚光灯机制

- 自我中心：自己是自己世界的中心
- 锚定调整：从自己视角出发调整不足
- 透明度错觉：高估自己状态的外显程度
- 记忆偏差：高估他人对自己行为的记忆

---

### Step 4: 校正聚光灯效应

- 客观调查：实际有多少人注意到？
- 视角转换：他人也在关注自己事务
- 时间衰减：注意力快速转移
- 设计认知检查清单：我不是世界中心

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **他人关注自己事务**：他人主要关注自己，而非你。原因：每个人都是自己世界的中心，他人注意力有限，不会持续关注你。
2. **注意力快速衰减**：即使被注意到，也会快速被遗忘。原因：新刺激不断出现，注意力快速转移到更新鲜事物。
3. **透明度错觉**：高估自己状态的外显程度。原因：自己清楚内心状态，误以为他人也能看到，实际外显信号很弱。
4. **视角转换是解药**：想象自己是观察者而非被观察者。原因：视角转换揭示他人实际关注度远低于自我估计。

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
- [ ] 是否识别了聚光灯信号？
- [ ] 是否评估了实际关注程度？
- [ ] 是否分析了聚光灯驱动机制？
- [ ] 是否使用视角转换校正？
- [ ] 是否考虑了注意力时间衰减？
- [ ] 输出具体可执行，不含模糊建议（如"别太在意"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [transparency-illusion](../thinking/transparency-illusion/SKILL.md) | 并行 | 透明度错觉高估内心状态外显，聚光灯效应高估他人关注 |
| [self-serving-bias](../thinking/self-serving-bias/SKILL.md) | 并行 | 自利偏差使高估自己重要性 |
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差使自己形象更容易回忆 |
| [anchoring-effect](../thinking/anchoring-effect/SKILL.md) | 并行 | 锚定效应使从自己视角调整不足 |

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

1. Gilovich, T., Medvec, V. H., & Savitsky, K. (2000). The spotlight effect in social judgment: An egocentric bias in estimates of the salience of one's own actions and appearance. *Journal of Personality and Social Psychology*, 78(2), 211-222.
2. Savitsky, K., Medvec, V. H., & Gilovich, T. (1999). The spotlight effect: Egocentric bias in social judgment. *Psychological Science*, 10(4), 337-341.
3. Kruger, J., & Gilovich, T. (2000). The "spotlight effect" and the "illusion of transparency": The egocentric bias in social judgment. *Current Directions in Psychological Science*, 9(5), 173-176.
4. Epley, N., Keysar, B., Van Boven, L., & Gilovich, T. (2004). Perspective taking as egocentric anchoring and adjustment. *Journal of Personality and Social Psychology*, 87(3), 327-339.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
