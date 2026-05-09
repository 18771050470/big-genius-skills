---
name: false-consensus-effect
description: |
  触发：当需要评估是否高估他人与自己观点一致、需要识别"大家都这么想"偏差、需要校正共识感知时调用；常见信号包括"正常人都会同意"、"这还用说"、"大家都这么认为"。
  不触发：当只需描述观点、无需评估共识程度时；当共识确实存在、经调查验证时；当只需记录意见、无需分析普遍性时。
  Invoke when needing to evaluate whether consensus with others is overestimated, identify "everyone thinks this way" bias, or correct consensus perception.
  Do NOT invoke when only describing opinions without evaluating consensus degree, when consensus truly exists (verified by survey), or when only recording opinions without analyzing universality.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["curse-of-knowledge", "self-serving-bias", "availability-bias", "bandwagon-effect"]
---

# 错误共识效应思维（False Consensus Effect Thinking）

## 核心定义

人们高估他人与自己观点、行为一致的程度。Ross等人在1977年广告牌实验证明：同意挂广告牌的人中62%认为别人也会同意，拒绝挂广告牌的人中仅33%认为别人会同意（即67%认为别人也会拒绝）。每个人都觉得别人和自己想的一样。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充实际共识数据、调查统计和不同意见分布
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别错误共识效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别共识信号

- 是否出现"正常人都会同意"、"这还用说"、"大家都这么认为"等表述？
- 是否高估他人与自己观点一致？
- 是否认为不同意见者不正常？
- 是否忽视反对声音？

---

### Step 2: 评估共识程度

- 实际有多少人同意？（调查数据）
- 自己的社交圈是否代表性样本？（选择性暴露）
- 不同意见是否被压制或沉默？（沉默螺旋）
- 共识估计是否系统偏向自己观点？

---

### Step 3: 分析共识机制

- 选择性暴露：只接触相似观点的人
- 可得性启发：同意例子更容易回忆
- 自我验证：共识信念提供心理舒适
- 社交同质性：朋友圈观点趋同

---

### Step 4: 校正共识偏差

- 调查实际分布：用数据替代直觉
- 寻找反对意见：主动接触不同观点
- 识别回声室：评估信息源多样性
- 设计决策检查清单：我的观点≠普遍观点

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **社交圈不代表整体**：朋友圈观点趋同，不反映整体分布。原因：选择性暴露使只接触相似观点，样本偏差导致高估共识。
2. **同意更容易回忆**：同意例子比反对例子更容易想起。原因：可得性启发使频繁接触的观点被高估频率。
3. **不同意见被极端化**：认为不同意见者不正常。原因：自我验证动机使将不同意见者视为异常，维护自己观点正确性。
4. **调查数据是解药**：用实际数据替代直觉估计。原因：调查提供客观分布，纠正选择性暴露导致的偏差。

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
- [ ] 是否识别了错误共识信号？
- [ ] 是否评估了实际共识程度？
- [ ] 是否分析了共识驱动机制？
- [ ] 是否使用调查数据校正？
- [ ] 是否主动寻找了反对意见？
- [ ] 输出具体可执行，不含模糊建议（如"了解不同意见"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [curse-of-knowledge](../thinking/curse-of-knowledge/SKILL.md) | 并行 | 知识诅咒假设他人知道相同信息，错误共识假设他人持有相同观点 |
| [self-serving-bias](../thinking/self-serving-bias/SKILL.md) | 并行 | 自利偏差使高估自己优点，错误共识使高估自己观点普遍性 |
| [availability-bias](../thinking/availability-bias/SKILL.md) | 并行 | 可得性偏差使同意例子更容易回忆 |
| [bandwagon-effect](../thinking/bandwagon-effect/SKILL.md) | 并行 | 从众效应使跟随感知到的共识，错误共识使高估共识 |

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

1. Ross, L., Greene, D., & House, P. (1977). The false consensus phenomenon: An attributional bias in self-perception and social perception processes. *Journal of Experimental Social Psychology*, 13(3), 279-301.
2. Mullen, B., Atkins, J. L., Champion, D. S., Edwards, C., Hardy, D., Story, J. E., & VanderKloot, M. (1985). The false consensus effect: A meta-analysis of 115 hypothesis tests. *Journal of Experimental Social Psychology*, 21(3), 262-283.
3. Krueger, J., & Clement, R. W. (1994). The truly false consensus effect: An ineradicable and egocentric bias in social perception. *Journal of Personality and Social Psychology*, 67(4), 596-610.
4. Marks, G., & Miller, N. (1987). Ten years of research on the false-consensus effect: An empirical and theoretical review. *Psychological Bulletin*, 102(1), 72-90.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
