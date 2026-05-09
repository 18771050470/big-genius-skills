---
name: just-world-hypothesis
description: |
  触发：当需要评估是否相信"善有善报恶有恶报"、需要识别"受害者肯定有错"偏差、需要分析公正世界信念时调用；常见信号包括"可怜之人必有可恨之处"、"因果报应"、"他肯定做错了什么"。
  不触发：当只需描述道德观念、无需评估归因偏差时；当因果关系确实存在、经实证验证时；当只需记录信念、无需分析偏差时。
  Invoke when needing to evaluate whether "good gets rewarded bad gets punished" belief is held, identify "victim must be at fault" bias, or analyze just-world belief.
  Do NOT invoke when only describing moral concepts without evaluating attribution bias, when causal relationship truly exists (verified by empirical evidence), or when only recording beliefs without analyzing bias.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["fundamental-attribution-error", "hindsight-bias", "self-serving-bias", "survivorship-bias"]
---

# 公正世界假设思维（Just-World Hypothesis Thinking）

## 核心定义

人们相信世界是公正的，善有善报恶有恶报。Lerner在1980年证明：人们倾向于责备受害者，以维持"世界公正"的信念。这使将不幸归因于受害者自身问题。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充受害者实际情况、随机因素证据和系统性原因
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别公正世界假设影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别公正世界信号

- 是否出现"可怜之人必有可恨之处"、"因果报应"、"他肯定做错了什么"等表述？
- 是否倾向于责备受害者？
- 是否相信不幸是自身原因导致？
- 是否忽视随机因素和系统性原因？

---

### Step 2: 评估归因模式

- 不幸的原因是什么？（个人、系统、随机）
- 受害者是否有控制力？
- 是否存在系统性不公？
- 随机因素是否被忽视？

---

### Step 3: 分析公正世界机制

- 控制需求：相信世界公正提供安全感
- 认知失调：不公正现实与公正信念冲突
- 恐惧管理：责备受害者使自己感觉安全
- 道德合理化：将不幸解释为道德后果

---

### Step 4: 校正公正世界偏差

- 多因素归因：考虑个人、系统、随机因素
- 随机性认知：接受世界不总是公正
- 同理心培养：理解受害者处境
- 设计归因检查清单：不幸≠过错

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **世界不总是公正**：不幸不一定是受害者过错。原因：随机因素、系统性不公、运气差异都可能导致不幸，与个人行为无关。
2. **责备受害者是防御**：责备受害者使自己感觉安全。原因：相信"受害者有错"使认为只要不犯同样错就不会受害，提供虚假安全感。
3. **控制错觉驱动**：相信公正世界提供控制感。原因：公正世界信念使认为行为控制结果，减少不确定焦虑。
4. **多因素归因是解药**：考虑个人、系统、随机因素。原因：多因素归因揭示不幸复杂性，避免简单责备受害者。

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
- [ ] 是否识别了公正世界信号？
- [ ] 是否评估了归因模式和多因素？
- [ ] 是否分析了公正世界驱动机制？
- [ ] 是否考虑了随机因素和系统性原因？
- [ ] 是否使用多因素归因校正？
- [ ] 输出具体可执行，不含模糊建议（如"同情受害者"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [fundamental-attribution-error](../thinking/fundamental-attribution-error/SKILL.md) | 并行 | 基本归因错误使高估个人因素，公正世界假设使责备受害者 |
| [hindsight-bias](../thinking/hindsight-bias/SKILL.md) | 并行 | 后见之明使结果看起来可预测，公正世界使不幸看起来应得 |
| [self-serving-bias](../thinking/self-serving-bias/SKILL.md) | 并行 | 自利偏差使成功归自己失败归外部，公正世界使他人失败归他人 |
| [survivorship-bias](../thinking/survivorship-bias/SKILL.md) | 并行 | 幸存者偏差使只看到成功者，公正世界使认为失败者有问题 |

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

1. Lerner, M. J. (1980). *The Belief in a Just World: A Fundamental Delusion*. Plenum Press.
2. Furnham, A. (2003). Belief in a just world: Research progress over the past decade. *Personality and Individual Differences*, 34(5), 795-817.
3. Hafer, C. L., & Bègue, L. (2005). Experimental research on just-world theory: Problems, developments, and future challenges. *Psychological Bulletin*, 131(1), 128-167.
4. Rubin, Z., & Peplau, L. A. (1975). Who believes in a just world? *Journal of Social Issues*, 31(3), 65-89.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
