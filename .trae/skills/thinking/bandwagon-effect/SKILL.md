---
name: bandwagon-effect
description: |
  触发：当需要评估决策是否受从众心理影响、需要识别"大家都在做所以我也做"偏差、需要分析群体行为时调用；常见信号包括"大家都在买"、"这是趋势"、"别人都这么做"。
  不触发：当只需描述群体行为、无需评估个体决策时；当跟随群体确实是最优策略时（经独立分析验证）；当只需记录现象、无需分析动机时。
  Invoke when needing to evaluate whether decisions are affected by bandwagon psychology, identify "everyone is doing it so I should too" bias, or analyze group behavior.
  Do NOT invoke when only describing group behavior without evaluating individual decisions, when following the crowd is truly the optimal strategy (verified by independent analysis), or when only recording phenomena without analyzing motivation.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["social-proof", "availability-bias", "confirmation-bias", "groupthink"]
---

# 从众效应思维（Bandwagon Effect Thinking）

## 核心定义

人们因他人在做某事而跟随，而非独立评估价值。Leibenstein在1950年提出：从众效应使需求随他人购买增加而增加，形成正反馈循环。这导致泡沫、流行和群体非理性。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充独立评估数据、群体行为动机和历史泡沫案例
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别从众效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别从众信号

- 是否出现"大家都在买"、"这是趋势"、"别人都这么做"等表述？
- 是否因他人行为而跟随？
- 是否独立评估过价值？
- 是否害怕错过（FOMO）？

---

### Step 2: 评估群体行为

- 多少人参与？（规模）
- 参与动机是什么？（价值vs从众）
- 信息 cascade 是否形成？（盲目跟随）
- 正反馈循环强度？

---

### Step 3: 分析从众机制

- 社会认同：他人行为作为质量信号
- 信息 cascade：忽略私人信息跟随他人
- FOMO：害怕错过驱动跟随
- 正反馈：更多人参与吸引更多人

---

### Step 4: 校正从众偏差

- 独立评估：不看他人行为，只评估内在价值
- 反向思考：如果没人做，我还会做吗？
- 历史对比：类似泡沫案例的结果
- 设计决策检查清单：他人行为≠价值信号

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **他人行为≠价值信号**：他人做某事不证明有价值。原因：他人可能也在从众，形成信息 cascade，无人真正评估价值。
2. **正反馈导致泡沫**：从众效应形成正反馈，价格/参与度脱离基本面。原因：更多人参与吸引更多人，直到新参与者不足，泡沫破裂。
3. **FOMO驱动非理性**：害怕错过使人们忽视风险。原因：FOMO触发情感反应，抑制理性分析，导致冲动跟随。
4. **独立评估是解药**：不看他人行为，只评估内在价值。原因：独立评估基于基本面，不受群体情绪影响。

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
- [ ] **从众效应特供**：是否识别了"大家都在做"、"这是趋势"、"害怕错过（FOMO）"等从众信号？这些信号是独立评估的起点还是干扰源？
- [ ] **从众效应特供**：是否评估了群体行为规模、参与动机和信息级联（information cascade）的形成？是否区分了"信息性从众"与"规范性从众"？
- [ ] **从众效应特供**：是否分析了从众的正反馈机制？是否评估了泡沫形成和破裂的临界点？
- [ ] **从众效应特供**：是否使用独立评估进行校正？是否执行了"如果没人做，我还会做吗？"的反向测试？
- [ ] **从众效应特供**：是否对比了历史泡沫案例（如郁金香泡沫、互联网泡沫）？案例与当前情境的相似性和差异性是否被分析？
- [ ] **从众效应特供**：是否评估了"社会认同"被误用为"质量信号"的风险？群体行为是否被赋予了超出其信息含量的权重？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"独立思考"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [social-proof](../thinking/social-proof/SKILL.md) | 前置 | 社会认同解释为何他人行为被视为质量信号 |
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差使流行事物更容易被回忆 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误使寻找支持从众的证据 |
| [groupthink](../thinking/groupthink/SKILL.md) | 并行 | 群体思维使群体压制异议，从众效应使个体跟随 |

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

1. Leibenstein, H. (1950). Bandwagon, snob, and Veblen effects in the theory of consumers' demand. *Quarterly Journal of Economics*, 64(2), 183-207.
2. Bikhchandani, S., Hirshleifer, D., & Welch, I. (1992). A theory of fads, fashion, custom, and cultural change as informational cascades. *Journal of Political Economy*, 100(5), 992-1026.
3. Shiller, R. J. (2000). *Irrational Exuberance*. Princeton University Press.
4. Cialdini, R. B. (2001). The science of persuasion. *Scientific American*, 284(2), 76-81.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
