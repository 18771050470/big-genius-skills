---
name: halo-effect
description: |
  触发：当需要评估判断是否受单一特征光环影响、需要识别"一好百好"偏差、需要纠正整体评价时调用；常见信号包括"他很帅肯定能力强"、"名校毕业一定优秀"、"大公司出来的肯定靠谱"。
  不触发：当只需描述特征、无需评估整体判断时；当单一特征确实与整体能力相关时（经实证验证）；当只需记录印象、无需分析偏差时。
  Invoke when needing to evaluate whether judgments are affected by single trait halo, identify "one good means all good" bias, or correct overall evaluation.
  Do NOT invoke when only describing traits without evaluating overall judgment, when single trait truly correlates with overall ability (verified by empirical evidence), or when only recording impressions without analyzing bias.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["horn-effect", "attractiveness-bias", "confirmation-bias", "representativeness-heuristic"]
---

# 晕轮效应思维（Halo Effect Thinking）

## 核心定义

人们因单一正面特征而对整体产生正面评价。Thorndike在1920年军官评估实验证明：外貌好的军官被评价为智力更高、领导力更强。单一特征的光环扩散到无关特征的评价。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充各特征独立评估数据、光环特征证据和评价偏差数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别晕轮效应影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别光环信号

- 是否出现"他很帅肯定能力强"、"名校毕业一定优秀"、"大公司出来的肯定靠谱"等表述？
- 是否因单一特征而对整体产生正面评价？
- 是否将光环特征扩散到无关特征？
- 是否忽视负面特征？

---

### Step 2: 评估特征关系

- 光环特征是什么？（外貌、学历、声誉）
- 光环特征与评价特征是否相关？（实证证据）
- 光环特征是否被过度加权？
- 其他特征是否被忽视？

---

### Step 3: 分析光环机制

- 认知捷径：单一特征作为整体评价代理
- 首因效应：第一印象影响后续评价
- 一致性偏好：维持评价一致性
- 情感扩散：正面情感扩散到所有特征

---

### Step 4: 校正晕轮效应

- 特征独立评估：每个特征单独评分
- 盲评设计：隐藏光环特征
- 多评估者：减少个人光环影响
- 设计评估矩阵：强制逐项评估

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **特征不必然相关**：单一特征不证明其他特征优秀。原因：外貌、学历与能力相关性有限，光环使无关特征被高估。
2. **光环扩散无意识**：人们 unaware 光环影响评价。原因：认知自动将正面特征扩散到整体，难以自我察觉。
3. **首因效应强化**：第一印象形成后难以改变。原因：一致性偏好使后续信息被解释为支持第一印象。
4. **独立评估是解药**：每个特征单独评分。原因：独立评估阻止光环扩散，提供客观特征评价。

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
- [ ] 是否识别了晕轮信号？
- [ ] 是否评估了特征关系和相关性？
- [ ] 是否分析了光环驱动机制？
- [ ] 是否使用特征独立评估校正？
- [ ] 是否设计了盲评或多评估者机制？
- [ ] 输出具体可执行，不含模糊建议（如"客观评价"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [horn-effect](../thinking/horn-effect/SKILL.md) | 并行 | 角效应是晕轮效应的负面版本，一坏百坏 |
| [attractiveness-bias](../thinking/attractiveness-bias/SKILL.md) | 前置 | 外貌吸引力偏差是晕轮效应的常见表现 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误使寻找支持光环的证据 |
| [representativeness-heuristic](../thinking/representativeness-heuristic/SKILL.md) | 并行 | 代表性启发使基于典型特征判断整体 |

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

1. Thorndike, E. L. (1920). A constant error in psychological ratings. *Journal of Applied Psychology*, 4(1), 25-29.
2. Nisbett, R. E., & Wilson, T. D. (1977). The halo effect: Evidence for unconscious alteration of judgments. *Journal of Personality and Social Psychology*, 35(4), 250-256.
3. Dion, K., Berscheid, E., & Walster, E. (1972). What is beautiful is good. *Journal of Personality and Social Psychology*, 24(2), 285-290.
4. Cooper, W. H. (1981). Ubiquitous halo. *Psychological Bulletin*, 90(2), 218-244.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
