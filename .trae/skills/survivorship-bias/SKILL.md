---
name: survivorship-bias
description: |
  触发：当需要评估分析是否只关注成功案例、需要从失败案例学习、需要识别选择性可见偏差时调用；常见信号包括"成功人士都这样做"、"看看这些成功案例"、"他们都具备X特质"。
  不触发：当已包含失败案例分析时；当只需描述成功案例特征、无需推断普适规律时；当失败案例数据不可获取时。
  Invoke when needing to evaluate whether analysis only focuses on success cases, learn from failure cases, or identify selective visibility bias.
  Do NOT invoke when failure case analysis is already included, when only describing success case characteristics without inferring universal patterns, or when failure case data is unavailable.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["confirmation-bias", "base-rate-fallacy", "statistical-thinking", "critical-thinking"]
---

# 幸存者偏差思维（Survivorship Bias Thinking）

## 核心定义

人们倾向于只关注成功案例，忽视失败案例，导致错误结论。Wald在二战期间分析返航飞机弹孔分布时发现：应该加固没有弹孔的部位（引擎和油箱），因为被击中这些部位的飞机没能返航。只看到幸存者会得出有偏结论。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充失败案例数据、总体样本量和沉默证据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别幸存者偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别幸存者信号

- 是否只分析成功案例？
- 是否出现"成功人士都这样做"、"看看这些成功案例"等表述？
- 失败案例在哪里？为什么没被看到？
- 总体样本量是多少？成功案例占比多少？

---

### Step 2: 寻找沉默证据

- 失败案例的特征是什么？
- 失败案例是否做了与成功案例相同的事？
- 如果失败案例也做同样的事，那件事就不是成功原因
- 计算：成功者做X的比例 vs 失败者做X的比例

---

### Step 3: 评估选择偏差

- 样本如何被选择？（自我选择、可见性选择、存活选择）
- 哪些案例被系统性排除？
- 可见案例是否代表总体？
- 偏差方向：高估还是低估了某因素的效果？

---

### Step 4: 校正分析

- 包含失败案例到分析中
- 使用总体样本而非可见样本
- 比较成功组和失败组的差异
- 识别真正区分成功和失败的因素

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **沉默证据最危险**：看不见的案例往往提供最有价值的信息。原因：失败案例揭示什么不能成功，成功案例只揭示什么可能成功。
2. **成功者做X ≠ 做X导致成功**：可能失败者也做X，X与成功无关。原因：相关性不等于因果性，需要对照组验证。
3. **总体样本是关键**：只分析可见样本得出有偏结论。原因：选择偏差使可见样本不代表总体，必须考虑被排除的案例。
4. **失败是更好老师**：失败案例比成功案例提供更多信息。原因：成功可能有运气成分，失败通常有明确原因。

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
- [ ] 是否识别了幸存者信号？
- [ ] 是否寻找了沉默证据（失败案例）？
- [ ] 是否评估了选择偏差？
- [ ] 是否包含失败案例到分析中？
- [ ] 是否比较了成功组和失败组？
- [ ] 输出具体可执行，不含模糊建议（如"考虑失败案例"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误选择性收集支持证据，幸存者偏差选择性看到成功案例 |
| [base-rate-fallacy](../thinking/base-rate-fallacy/SKILL.md) | 并行 | 基础概率谬误忽视基础率，幸存者偏差忽视失败率 |
| [statistical-thinking](../thinking/statistical-thinking/SKILL.md) | 前置 | 统计思维提供样本代表性概念 |
| [critical-thinking](../thinking/critical-thinking/SKILL.md) | 前置 | 批判性思维提供客观评估证据框架 |

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

1. Wald, A. (1943). *A Method of Estimating Plane Vulnerability Based on Casualty Data*. Statistical Research Group, Columbia University.
2. Taleb, N. N. (2007). *The Black Swan: The Impact of the Highly Improbable*. Random House. (Chapter 5: Confirmation Bias)
3. Henderson, H. (2009). Survivorship bias: A note. *Economic Inquiry*, 47(4), 817-818.
4. Derks, B., & Pollock, D. (2009). *The Psychology of Success and Failure*. Cambridge University Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
