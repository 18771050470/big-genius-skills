---
name: decoy-effect
description: |
  触发：当需要评估选择是否受诱饵选项影响、需要识别"不对称优势"偏差、需要优化选项设计时调用；常见信号包括"这个明显不划算"、"对比之下那个更好"、"加一点钱就能升级"。
  不触发：当只需描述选项、无需评估诱饵影响时；当选项间确实存在绝对优势时（经独立评估验证）；当只需比较两个选项、无需分析第三选项影响时。
  Invoke when needing to evaluate whether choices are affected by decoy options, identify "asymmetric dominance" bias, or optimize option design.
  Do NOT invoke when only describing options without evaluating decoy impact, when options truly have absolute dominance (verified by independent evaluation), or when only comparing two options without analyzing third option impact.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["framing-effect", "anchoring-effect", "choice-overload", "prospect-theory"]
---

# 诱饵效应思维（Decoy Effect Thinking）

## 核心定义

添加一个劣势选项（诱饵）使目标选项更有吸引力。Huber等人在1982年证明：当选项C明显劣于选项B但略劣于选项A时，B的选择率增加。诱饵不旨在被选，旨在改变A和B的相对吸引力。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充各选项独立评估数据、诱饵存在证据和选择模式
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别诱饵效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别诱饵信号

- 是否出现"这个明显不划算"、"对比之下那个更好"、"加一点钱就能升级"等表述？
- 是否有选项明显劣于其他选项？
- 该选项是否旨在改变其他选项的相对吸引力？
- 选择模式是否因添加选项而改变？

---

### Step 2: 评估选项关系

- 各选项的独立价值？（不看其他选项）
- 选项间比较关系？（A vs B, A vs C, B vs C）
- 诱饵选项是否不对称劣势？（明显劣于目标，略劣于竞争者）
- 选择率变化：添加诱饵前后

---

### Step 3: 分析诱饵机制

- 比较效应：诱饵使目标选项看起来更好
- 折中效应：诱饵使目标成为折中选择
- 吸引力效应：诱饵增加目标吸引力
- 理由生成：诱饵提供选择目标的理由

---

### Step 4: 校正诱饵效应

- 独立评估：不看其他选项，只评估每个选项
- 移除诱饵：比较没有诱饵时的选择
- 设计决策检查清单：选项对比≠真实价值
- 使用预先标准：在选择前确定评估标准

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **诱饵旨在被比较**：诱饵选项不旨在被选，旨在改变比较。原因：诱饵提供参照点，使目标选项看起来更优，触发比较效应。
2. **不对称优势是关键**：诱饵明显劣于目标，略劣于竞争者。原因：这种设计使目标选项在比较中获得最大优势，增加选择率。
3. **选项顺序影响**：选项呈现顺序影响诱饵效果。原因：视觉对比和注意力分配影响比较过程，目标选项位置很重要。
4. **独立评估是解药**：不看其他选项，只评估每个选项。原因：独立评估基于内在价值，不受比较效应影响。

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
- [ ] 是否识别了诱饵信号？
- [ ] 是否评估了选项关系和诱饵设计？
- [ ] 是否分析了诱饵驱动机制？
- [ ] 是否使用独立评估校正？
- [ ] 是否考虑了移除诱饵的影响？
- [ ] 输出具体可执行，不含模糊建议（如"避免诱饵"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [framing-effect](../thinking/framing-effect/SKILL.md) | 并行 | 框架效应改变选项表述，诱饵效应改变选项比较 |
| [anchoring-effect](../thinking/anchoring-effect/SKILL.md) | 并行 | 锚定效应使初始值影响估计，诱饵效应使参照选项影响选择 |
| [choice-overload](../thinking/choice-overload/SKILL.md) | 并行 | 选择过载使多选项导致决策困难，诱饵效应利用多选项引导选择 |
| [prospect-theory](../thinking/prospect-theory/SKILL.md) | 并行 | 前景理论解释参照点依赖，诱饵效应利用参照点设计 |

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

1. Huber, J., Payne, J. W., & Puto, C. (1982). Adding asymmetrically dominated alternatives: Violations of regularity and the similarity hypothesis. *Journal of Consumer Research*, 9(1), 90-98.
2. Ariely, D., & Wallsten, T. S. (2005). Source of coherence in attitude measurement. *Journal of Consumer Research*, 32(3), 393-403.
3. Simonson, I. (1989). Choice based on reasons: The case of attraction and compromise effects. *Journal of Consumer Research*, 16(2), 158-174.
4. Trueblood, J. S., Brown, S. D., & Heathcote, A. (2013). The multiattribute linear ballistic accumulator model of context effects in multialternative choice. *Psychological Review*, 120(2), 341-356.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
