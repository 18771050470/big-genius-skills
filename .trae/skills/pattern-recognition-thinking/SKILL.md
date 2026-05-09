---
name: pattern-recognition-thinking
description: |
  触发：当需要从数据或经验中识别规律、需要区分真实模式和随机噪音、需要评估模式预测能力时调用；常见信号包括"我注意到一个规律"、"每次X发生Y就会发生"、"这看起来像某种模式"。
  不触发：当只需描述单个事件、无需寻找规律时；当数据量过小（<30样本）无法统计验证时；当模式已被科学理论解释、无需重新识别时。
  Invoke when needing to identify patterns from data or experience, distinguish real patterns from random noise, or evaluate pattern predictive power.
  Do NOT invoke when only describing single events without finding patterns, when sample size is too small (<30) for statistical validation, or when patterns are already explained by scientific theory.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["inductive-reasoning", "statistical-thinking", "confirmation-bias", "narrative-thinking"]
---

# 模式识别思维（Pattern Recognition Thinking）

## 核心定义

从数据、经验或观察中识别重复出现的结构、关系或趋势。Simon和Chase在1973年研究国际象棋大师时发现：专家的核心能力是识别模式。但人类大脑过度敏感于模式识别，容易在随机数据中"看到"模式（模式错觉），需要统计验证区分真实模式和随机噪音。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充数据样本量、历史观测记录和模式出现频率
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已验证模式真实性且预测模型清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别候选模式

- 观察到的重复现象是什么？
- 模式出现的频率和条件？
- 模式是确定性的还是概率性的？
- 标注模式类型：时间序列模式、空间模式、关联模式、因果模式

---

### Step 2: 收集验证数据

- 有多少样本支持这个模式？（样本量）
- 有多少样本不支持这个模式？（反例）
- 数据收集是否有偏差？（选择性回忆、确认偏误）
- 样本是否独立？是否存在自相关？

---

### Step 3: 统计验证

- 模式是否在统计上显著？（p值 < 0.05）
- 效应量大小：模式解释多少变异？
- 是否存在混淆变量？
- 交叉验证：模式在新数据上是否复现？

---

### Step 4: 评估预测能力

- 模式对未来事件的预测准确度？
- 预测的置信区间是多少？
- 模式是否有理论支撑？（机制解释）
- 模式是否稳定？（随时间变化？）

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **模式需要统计验证**：肉眼看到的模式可能是随机波动。原因：人类大脑是模式识别机器，即使在纯随机数据中也会"看到"模式（聚类错觉）。
2. **样本量决定可信度**：小样本中的模式不可靠。原因：小样本中随机波动幅度大，容易产生虚假模式。大数定律需要足够样本。
3. **反例比正例更有价值**：一个可靠反例足以推翻模式。原因：科学方法通过证伪推进知识，证实只能增加信心不能证明。
4. **预测能力是最终检验**：能解释过去不等于能预测未来。原因：过拟合模型完美拟合历史数据但无法预测未来，预测能力是模式真实性的最终检验。

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
- [ ] 候选模式是否被清晰描述？
- [ ] 样本量是否足够？是否有反例？
- [ ] 是否进行了统计显著性检验？
- [ ] 是否进行了交叉验证？
- [ ] 模式预测能力是否被评估？
- [ ] 输出具体可执行，不含模糊建议（如"寻找规律"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [inductive-reasoning](../thinking/inductive-reasoning/SKILL.md) | 前置 | 归纳推理提供从具体到一般的推理方法 |
| [statistical-thinking](../thinking/statistical-thinking/SKILL.md) | 并行 | 统计思维提供模式验证的数学工具 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误选择性回忆支持模式的证据 |
| [narrative-thinking](../thinking/narrative-thinking/SKILL.md) | 并行 | 叙事思维评估模式解释是否过度简化 |

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

1. Simon, H. A., & Chase, W. G. (1973). Skill in chess. *American Psychologist*, 28(4), 321-334.
2. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux. (Chapter 10: The Law of Small Numbers)
3. Taleb, N. N. (2001). *Fooled by Randomness: The Hidden Role of Chance in Life and in the Markets*. Random House.
4. Gilovich, T., Vallone, R., & Tversky, A. (1985). The hot hand in basketball: On the misperception of random sequences. *Cognitive Psychology*, 17(3), 295-315.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
