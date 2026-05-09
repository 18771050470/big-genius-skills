---
name: base-rate-fallacy
description: |
  触发：当需要评估判断是否忽视基础概率、需要将个案信息与统计基准结合、需要识别代表性偏差时调用；常见信号包括"这个案例很典型"、"看起来像X"、"特征完全匹配"。
  不触发：当基础概率不可用或不可靠时；当只需定性描述、无需概率估计时；当个案信息完全压倒基础概率时（经贝叶斯计算验证）。
  Invoke when needing to evaluate whether judgments ignore base rates, integrate case-specific information with statistical benchmarks, or identify representativeness bias.
  Do NOT invoke when base rates are unavailable or unreliable, when only qualitative description is needed without probability estimation, or when case-specific information completely overwhelms base rates (verified by Bayesian calculation).
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["bayesian-updating", "representativeness-heuristic", "probabilistic-thinking", "pattern-recognition-thinking"]
---

# 基础概率谬误思维（Base Rate Fallacy Thinking）

## 核心定义

人们倾向于忽视基础概率（先验概率），过度关注个案信息。Kahneman和Tversky在1973年提出代表性启发式：人们根据相似度判断概率，忽视基础概率。例如：即使某疾病发病率仅1/1000，检测呈阳性后人们仍认为患病概率90%以上，实际仅约2%。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充基础概率数据、检测准确率和假阳性率
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别基础概率谬误影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别基础概率信号

- 是否出现"这个案例很典型"、"看起来像X"、"特征完全匹配"等表述？
- 是否忽视基础概率（先验概率）？
- 是否过度关注个案特征而忽视统计基准？
- 是否混淆条件概率 P(A|B) 和 P(B|A)？

---

### Step 2: 获取基础概率数据

- 该事件的基础概率是多少？（人群中的发病率、事件发生率）
- 检测/判断的准确率是多少？（真阳性率、假阳性率）
- 样本量是否足够？基础概率是否可靠？
- 基础概率是否适用于当前个案？

---

### Step 3: 贝叶斯计算校正

- 使用贝叶斯定理：P(患病|阳性) = P(阳性|患病) × P(患病) / P(阳性)
- 计算后验概率，而非依赖直觉
- 比较直觉判断与贝叶斯计算结果
- 评估差异程度：基础概率谬误的影响大小

---

### Step 4: 设计防偏差机制

- 始终先查基础概率，再评估个案
- 使用频率格式替代概率格式（"1000人中1人患病"替代"0.1%概率"）
- 可视化贝叶斯更新过程（决策树或自然频率树）
- 训练贝叶斯思维：基础概率是起点，个案信息是调整

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **基础概率是起点**：任何概率判断都应以基础概率为起点，个案信息只是调整。原因：基础概率反映总体统计规律，个案信息可能有噪音。
2. **代表性不等于概率**：看起来像某事物不等于就是某事物。原因：罕见事物的典型特征可能出现在更多人身上，假阳性数量可能超过真阳性。
3. **频率格式更易理解**：用"1000人中10人"替代"1%概率"，大脑更容易处理。原因：频率格式提供具体样本，降低认知负荷，减少计算错误。
4. **贝叶斯是校正工具**：贝叶斯定理提供数学框架整合基础概率和个案信息。原因：直觉无法正确处理条件概率，贝叶斯提供准确计算方法。

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
- [ ] **基础概率谬误特供**：是否识别了"这个案例很典型"、"看起来像X"、"特征完全匹配"等代表性偏差信号？是否明确标注了先验概率？
- [ ] **基础概率谬误特供**：是否获取了可靠的基础概率数据？数据来源、样本量和时效性是否被评估？基础概率是否适用于当前个案？
- [ ] **基础概率谬误特供**：是否使用贝叶斯定理（或自然频率法）计算后验概率？计算过程是否完整展示？
- [ ] **基础概率谬误特供**：是否比较了直觉判断与贝叶斯计算结果？差异幅度是否被量化？基础概率谬误的影响大小是否被评估？
- [ ] **基础概率谬误特供**：是否使用频率格式（如"1000人中1人"）替代概率格式呈现结果？频率树或决策树是否被用于可视化？
- [ ] **基础概率谬误特供**：是否检查了条件概率的混淆？P(A|B) 和 P(B|A) 是否被正确区分？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"考虑基础概率"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 前置 | 贝叶斯更新提供基础概率与个案信息整合的数学框架 |
| [representativeness-heuristic](../thinking/representativeness-heuristic/SKILL.md) | 并行 | 代表性启发式解释为何忽视基础概率 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供基础概率概念框架 |
| [pattern-recognition-thinking](../thinking/pattern-recognition-thinking/SKILL.md) | 并行 | 模式识别可能触发代表性偏差 |

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

1. Kahneman, D., & Tversky, A. (1973). On the psychology of prediction. *Psychological Review*, 80(4), 237-251.
2. Tversky, A., & Kahneman, D. (1974). Judgment under uncertainty: Heuristics and biases. *Science*, 185(4157), 1124-1131.
3. Gigerenzer, G., & Hoffrage, U. (1999). Bayesian reasoning with natural frequencies: An ecological perspective. *Psychological Review*, 106(2), 425-430.
4. Bar-Hillel, M. (1980). The base-rate fallacy in probability judgments. *Acta Psychologica*, 44(3), 211-233.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
