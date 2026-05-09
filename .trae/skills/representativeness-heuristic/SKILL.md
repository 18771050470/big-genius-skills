---
name: representativeness-heuristic
description: |
  触发：当需要评估判断是否基于相似度而非概率、需要识别代表性启发式偏差、需要纠正类别判断时调用；常见信号包括"看起来像X"、"典型的Y"、"完全符合Z的特征"。
  不触发：当只需定性描述相似度、无需概率判断时；当有完整统计数据可用时；当类别判断基于统计模型而非直觉时。
  Invoke when needing to evaluate whether judgments are based on similarity rather than probability, identify representativeness heuristic bias, or correct category judgments.
  Do NOT invoke when only qualitatively describing similarity without probability judgment, when complete statistical data is available, or when category judgment is based on statistical models rather than intuition.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["base-rate-fallacy", "conjunction-fallacy", "pattern-recognition-thinking", "probabilistic-thinking"]
---

# 代表性启发式思维（Representativeness Heuristic Thinking）

## 核心定义

人们根据事物与典型原型的相似度判断其概率，忽视基础概率和样本量。Tversky和Kahneman在1972年提出：当A高度代表B时，人们判断A来自B的概率很高。这导致基础概率忽视、合取谬误和样本量不敏感等系统性偏差。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充基础概率数据、样本量和统计分布信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别代表性启发式影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别代表性信号

- 是否出现"看起来像X"、"典型的Y"、"完全符合Z的特征"等表述？
- 是否基于相似度判断概率？
- 是否忽视了基础概率（先验概率）？
- 是否忽视了样本量大小？

---

### Step 2: 评估代表性偏差

- 判断是否基于刻板印象或原型？
- 是否认为小样本能代表总体？（小数定律）
- 是否认为随机序列应该"看起来随机"？（赌徒谬误）
- 是否认为描述详细的事件更可能发生？（合取谬误）

---

### Step 3: 获取统计基准

- 该类别的基础概率是多少？
- 样本量是否足够大？（<30为小样本）
- 数据分布是什么？（正态、偏态、幂律）
- 是否有历史数据验证代表性判断？

---

### Step 4: 校正判断

- 使用贝叶斯定理整合基础概率和个案信息
- 小样本判断增加不确定性范围
- 识别随机序列的真实特征（聚集是正常现象）
- 使用统计模型替代直觉判断

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **相似不等于概率**：看起来像某类别不等于就是该类别。原因：罕见类别的典型特征可能出现在更多人身上，基础概率决定真实可能性。
2. **小样本不可靠**：小样本的统计特征不稳定，不能代表总体。原因：抽样误差在小样本中更大，极端值更容易出现。
3. **随机不"看起来随机"**：真实随机序列包含聚集和模式，不"均匀分布"。原因：人类对随机性的直觉是错误的，认为随机应该均匀分布。
4. **详细不等于可能**：描述越详细的事件不一定更可能。原因：合取事件概率低于单一事件，细节增加降低概率。

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
- [ ] 是否识别了代表性信号？
- [ ] 是否评估了代表性偏差类型？
- [ ] 是否获取了统计基准（基础概率、样本量、分布）？
- [ ] 是否使用贝叶斯定理校正？
- [ ] 是否考虑了小样本不可靠性？
- [ ] 输出具体可执行，不含模糊建议（如"考虑统计"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [base-rate-fallacy](../thinking/base-rate-fallacy/SKILL.md) | 并行 | 基础概率谬误是代表性启发式的直接后果 |
| [conjunction-fallacy](../thinking/conjunction-fallacy/SKILL.md) | 并行 | 合取谬误是代表性启发式的典型表现 |
| [pattern-recognition-thinking](../thinking/pattern-recognition-thinking/SKILL.md) | 并行 | 模式识别可能触发代表性偏差 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维提供统计校正框架 |

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

1. Tversky, A., & Kahneman, D. (1972). Subjective probability: A judgment of representativeness. *Cognitive Psychology*, 3(3), 430-454.
2. Tversky, A., & Kahneman, D. (1974). Judgment under uncertainty: Heuristics and biases. *Science*, 185(4157), 1124-1131.
3. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 14: Tom W's Specialty)
4. Gigerenzer, G. (1996). On narrow norms and vague heuristics: A reply to Kahneman and Tversky. *Psychological Review*, 103(3), 592-596.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
