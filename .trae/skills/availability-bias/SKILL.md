---
name: availability-bias
description: |
  触发：当需要评估判断是否受易回忆信息影响、需要纠正概率估计时调用；常见信号包括"最近新闻说X很危险"、"我认识的人都这样"、"感觉这事经常发生"。
  不触发：当有完整统计数据可用时；当只需定性描述、无需概率估计时；当信息样本量充足且代表性强时。
  Invoke when needing to evaluate whether judgments are affected by easily recalled information, or needing to correct probability estimates.
  Do NOT invoke when complete statistical data is available, when only qualitative description is needed without probability estimation, or when information sample size is sufficient and representative.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["dual-process-thinking", "probabilistic-thinking", "confirmation-bias", "anchoring-effect"]
---

# 可得性偏差思维（Availability Bias Thinking）

## 核心定义

人们倾向于根据事件在记忆中回忆的难易程度来估计其发生概率，而非基于实际统计数据。Tversky和Kahneman在1973年提出：生动、近期、情绪化的事件更容易被回忆，导致概率估计系统性偏高。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充实际统计数据、样本量和代表性信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别可得性偏差影响且校正方案明确，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别判断来源

- 当前概率估计是基于什么信息？
- 这些信息是否因为生动、近期、情绪化而容易被回忆？
- 区分"容易回忆"和"经常发生"：两者不一定相关
- 标注信息来源的偏差风险：媒体曝光、个人经历、社交媒体

---

### Step 2: 评估可得性偏差影响

- 检查偏差类型：
  - 回忆偏差：最近发生的事件更容易被回忆
  - 生动性偏差：戏剧性事件比平淡事件更容易被回忆
  - 媒体曝光偏差：频繁报道的事件被高估概率
- 评估偏差方向：高估还是低估？
- 评估偏差程度：与实际统计数据差距多大？

---

### Step 3: 寻找基准数据（Base Rate）

- 查找实际统计数据：事件真实发生率是多少？
- 样本量是否充足？样本是否具有代表性？
- 使用外部视角：同类事件的平均发生率是多少？
- 对比直觉估计和基准数据，计算偏差幅度

---

### Step 4: 校正概率估计

- 用基准数据替代直觉估计
- 如果基准数据不可用，标注不确定性范围
- 设计决策规则：在什么情况下可以依赖直觉？
  - 高规律性环境 + 大量练习 + 即时反馈 → 可依赖
  - 低规律性环境或缺乏练习 → 必须用数据

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **容易回忆≠经常发生**：媒体频繁报道飞机失事，但飞机是最安全的交通方式。原因：媒体偏好戏剧性事件，不代表真实频率。
2. **个人经验是最强偏差源**：认识的人出事会大幅高估风险。原因：个人经验生动具体，比统计数据更容易回忆，但样本量极小。
3. **基准数据是最强校正**：用实际统计数据替代直觉估计。原因：基准数据来自大样本，不受个人记忆偏差影响。
4. **情绪放大可得性**：恐惧、愤怒等情绪使事件记忆更深刻。原因：情绪增强记忆编码，使情绪化事件更容易被回忆，导致概率高估。

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
- [ ] **可得性偏差特供**：是否识别了信息来源的"可得性"特征？信息是否因生动、近期、情绪化而容易被回忆？
- [ ] **可得性偏差特供**：是否区分了"容易回忆"和"经常发生"？是否明确标注了"回忆难易≠发生频率"？
- [ ] **可得性偏差特供**：是否评估了偏差类型（回忆偏差/生动性偏差/媒体曝光偏差）和偏差方向（高估/低估）？
- [ ] **可得性偏差特供**：是否找到了可靠的基准数据（Base Rate）？样本量是否充足且具代表性？
- [ ] **可得性偏差特供**：是否量化了直觉估计与基准数据的偏差幅度？偏差是否被具体数值化？
- [ ] **可得性偏差特供**：是否评估了情绪对可得性的放大作用？恐惧、愤怒等情绪是否被单独分析？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"客观看待"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [dual-process-thinking](../thinking/dual-process-thinking/SKILL.md) | 前置 | 双过程思维识别系统1直觉，可得性偏差是系统1的典型偏差 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维提供基准数据校正方法 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误选择性回忆支持性证据，可得性偏差回忆生动事件 |
| [anchoring-effect](../thinking/anchoring-effect/SKILL.md) | 并行 | 锚定效应和可得性偏差都是启发式偏差 |

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

1. Tversky, A., & Kahneman, D. (1973). Availability: A heuristic for judging frequency and probability. *Cognitive Psychology*, 5(2), 207-232.
2. Tversky, A., & Kahneman, D. (1974). Judgment under uncertainty: Heuristics and biases. *Science*, 185(4157), 1124-1131.
3. Schwarz, N., & Vaughn, L. A. (2002). The availability heuristic revisited: Ease of recall and content of recall as distinct sources of information. In *Heuristics and Biases: The Psychology of Intuitive Judgment* (pp. 103-119). Cambridge University Press.
4. Combs, B., & Slovic, P. (1979). Newspaper coverage of causes of death. *Journalism Quarterly*, 56(4), 836-840.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
