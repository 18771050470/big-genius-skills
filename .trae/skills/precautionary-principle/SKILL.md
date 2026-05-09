---
name: precautionary-principle
description: |
  触发：当评估可能造成严重或不可逆损害的行动时；当科学证据不足但潜在风险巨大时；当需要决定是否推迟行动以收集更多证据时；常见信号包括"万一出了大问题怎么办""这个风险虽然不确定但后果太严重""要不要先停下来观察"。
  不触发：当风险已被充分量化且后果可控时；当不行动本身会造成更大伤害时；当需要快速响应的紧急场景时。
  Invoke when evaluating actions with potentially serious or irreversible harm, when scientific evidence is insufficient but potential risks are massive.
  Do NOT invoke when risks are well-quantified and consequences are controllable, when inaction causes greater harm, or in emergency response scenarios.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["risk-assessment", "cost-benefit-analysis", "asymmetric-risk", "regret-aversion"]
---

# 预防原则（Precautionary Principle）

## 核心定义

当行动可能造成严重或不可逆的损害时，即使缺乏充分的科学确定性，也不应以"证据不足"为由推迟采取成本有效的预防措施。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充潜在损害的严重程度、可逆性、科学不确定性范围
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确判断风险严重且不可逆，可提前进入预防措施设计，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别潜在危害

- 该行动可能造成的最坏后果是什么？
- 损害的严重程度分级：轻微/严重/灾难性/生存性
- 损害的可逆性：能否通过后续行动恢复原状？
- 影响范围：局部、系统性还是全球性？
- 时间维度：即时爆发还是延迟显现？

### Step 2: 评估科学不确定性

- 当前科学证据的完整程度如何？（充分/部分/极少）
- 不确定性的来源：数据缺失、模型局限、因果链复杂？
- "等待更多证据"需要多长时间？期间风险是否累积？
- 是否存在"不可逆阈值"——一旦越过就无法挽回？

### Step 3: 分析行动与不行动的权衡

- 预防措施的成本：经济成本、机会成本、时间成本
- 不行动的风险暴露：概率 × 影响 = 预期损失
- 延迟行动的风险：问题是否在等待期间恶化？
- 是否存在"无悔措施"——即使风险未实现也值得做？

### Step 4: 设计分层预防策略

- **第一层：立即措施**——低成本、高确定性的预防行动
- **第二层：监测预警**——建立早期预警系统，设定触发条件
- **第三层：应急准备**——制定最坏情况下的响应预案
- **第四层：知识填补**——投资研究减少不确定性
- 每层措施标注：成本、效果、触发条件、退出条件

### Step 5: 建立动态调整机制

- 设定"重新评估节点"：什么新证据会改变判断？
- 定义"解除预警条件"：什么情况下可以放松预防？
- 建立反馈回路：监测结果如何影响预防强度？
- 避免"预防锁定"：预防措施本身是否有副作用？

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **不确定性不是不行动的理由**：当潜在损害严重且不可逆时，"证据不足"不能成为推迟预防的借口。原因：等待完美证据可能意味着等待灾难发生。
2. **预防成本必须合理**：预防措施本身不应造成与所防风险相当的伤害。原因：过度预防会导致资源错配和机会成本，甚至引发新的风险。
3. **不可逆性是核心判据**：可逆的错误可以事后纠正，不可逆的错误必须事前预防。原因：不可逆性消除了"试错学习"的可能性，使预防成为唯一选择。
4. **动态调整优于静态决策**：预防强度应随证据积累而调整，而非一劳永逸。原因：静态预防可能因新证据而过时，或因过度保守而浪费资源。

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
- [ ] 潜在危害是否被完整识别？严重程度和可逆性是否被评估？
- [ ] 科学不确定性的范围和来源是否被分析？
- [ ] 行动与不行动的权衡是否被量化或结构化比较？
- [ ] 是否设计了分层预防策略（立即措施→监测预警→应急准备→知识填补）？
- [ ] 是否建立了动态调整机制（重新评估节点、解除预警条件）？
- [ ] 是否分析了预防措施本身的副作用和"预防锁定"风险？
- [ ] 输出具体可执行，不含模糊建议（如"谨慎行事"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [risk-assessment](../thinking/risk-assessment/SKILL.md) | 前置 | 在应用预防原则前，先用风险评估量化潜在危害 |
| [cost-benefit-analysis](../thinking/cost-benefit-analysis/SKILL.md) | 并行 | 比较预防措施的成本与不行动的风险暴露 |
| [asymmetric-risk](../thinking/asymmetric-risk/SKILL.md) | 关联 | 分析"下行无限、上行有限"的不对称风险结构 |
| [regret-aversion](../thinking/regret-aversion/SKILL.md) | 后置 | 评估未来是否会因"本可以预防"而后悔 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | 思维模型的理论背景（可选） |

---

## 参考文献

1. United Nations. (1992). *Rio Declaration on Environment and Development*, Principle 15. UN Conference on Environment and Development.
2. O'Riordan, T., & Cameron, J. (1994). *Interpreting the Precautionary Principle*. Cameron May.
3. Sunstein, C. R. (2005). *Laws of Fear: Beyond the Precautionary Principle*. Cambridge University Press.
4. European Commission. (2000). *Communication on the Precautionary Principle*. COM(2000) 1 final.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
