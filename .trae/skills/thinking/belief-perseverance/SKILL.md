---
name: belief-perseverance
description: |
  触发：当需要评估信念是否在面对反面证据时仍坚持、需要识别"即使证据相反也不改变"偏差、需要分析信念更新阻力时调用；常见信号包括"我就是不信"、"证据可能是错的"、"这不可能"。
  不触发：当只需描述信念、无需评估证据响应时；当反面证据确实不可靠时（经方法学验证）；当只需记录观点、无需分析更新机制时。
  Invoke when needing to evaluate whether beliefs persist despite contrary evidence, identify "even if evidence is contrary I won't change" bias, or analyze belief update resistance.
  Do NOT invoke when only describing beliefs without evaluating evidence response, when contrary evidence is truly unreliable (verified by methodology), or when only recording opinions without analyzing update mechanism.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["confirmation-bias", "backfire-effect", "cognitive-dissonance", "bayesian-updating"]
---

# 信念坚持思维（Belief Perseverance Thinking）

## 核心定义

人们面对反面证据时仍坚持原有信念。Anderson等人在1980年证明：即使解释信念形成的证据被证明是虚假的，人们仍坚持信念。信念一旦形成，具有自我维持性。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充反面证据质量、信念形成历史和更新阻力数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别信念坚持影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别坚持信号

- 是否出现"我就是不信"、"证据可能是错的"、"这不可能"等表述？
- 是否拒绝接受反面证据？
- 是否寻找理由解释反面证据？
- 是否坚持信念即使基础被推翻？

---

### Step 2: 评估证据质量

- 反面证据的方法学质量？（样本、设计、统计）
- 证据是否可重复？（独立验证）
- 证据是否直接反驳信念？（针对性）
- 证据强度如何？（效应量、置信区间）

---

### Step 3: 分析坚持机制

- 认知失调：改变信念产生心理不适
- 身份绑定：信念与自我身份关联
- 沉没成本：投入时间精力维护信念
- 社会压力：改变信念面临群体压力

---

### Step 4: 校正信念坚持

- 证据分级：按方法学质量评估证据
- 贝叶斯更新：根据证据强度调整信念
- 分离身份：信念≠身份，改变信念不否定自我
- 设计更新规则：何时应该改变信念？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **信念具有惯性**：一旦形成，难以改变。原因：信念与认知结构、身份、社会关系绑定，改变成本高。
2. **反面证据被折扣**：人们寻找理由拒绝反面证据。原因：认知失调产生不适，拒绝证据比改变信念更容易。
3. **证据被推翻仍坚持**：即使基础证据被证明虚假，信念仍持续。原因：信念已形成独立认知结构，不依赖原始证据。
4. **贝叶斯更新是解药**：根据证据强度系统调整信念。原因：贝叶斯方法提供客观更新规则，避免情感阻力。

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
- [ ] **信念坚持特供**：是否识别了"我就是不信"、"证据可能是错的"、"这不可能"等信念坚持信号？这些信号是理性怀疑还是认知防御？
- [ ] **信念坚持特供**：是否评估了反面证据的方法学质量？证据的可重复性、针对性和效应量是否被审查？
- [ ] **信念坚持特供**：是否分析了信念坚持的驱动机制？认知失调、身份绑定、沉没成本和社会压力是否被逐一排查？
- [ ] **信念坚持特供**：是否使用贝叶斯更新进行信念调整？调整幅度是否与证据强度匹配？是否存在"逆火效应"（反面证据强化原有信念）？
- [ ] **信念坚持特供**：是否分离了信念与身份？是否明确"改变信念≠否定自我"？
- [ ] **信念坚持特供**：是否设计了明确的信念更新规则？在什么条件下应该改变信念？阈值是否被量化？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"改变信念"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误使寻找支持性证据，信念坚持使拒绝反面证据 |
| [backfire-effect](../thinking/backfire-effect/SKILL.md) | 并行 | 逆火效应使反面证据强化原有信念 |
| [cognitive-dissonance](../thinking/cognitive-dissonance/SKILL.md) | 前置 | 认知失调解释为何改变信念产生不适 |
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 前置 | 贝叶斯更新提供信念更新的客观方法 |

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

1. Anderson, C. A., Lepper, M. R., & Ross, L. (1980). Perseverance of social theories: The role of explanation in the persistence of discredited information. *Journal of Personality and Social Psychology*, 39(6), 1037-1049.
2. Ross, L., Lepper, M. R., & Hubbard, M. (1975). Perseverance in self-perception and social perception: Biased attributional processes in the debriefing paradigm. *Journal of Personality and Social Psychology*, 32(5), 880-892.
3. Plous, S. (1993). *The Psychology of Judgment and Decision Making*. McGraw-Hill.
4. Nickerson, R. S. (1998). Confirmation bias: A ubiquitous phenomenon in many guises. *Review of General Psychology*, 2(2), 175-220.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
