---
name: probabilistic-thinking
description: |
  触发：当面对不确定性决策、风险评估、未来预测时；常见信号包括"不确定"、"概率"、"风险"、"可能"、"如果"、"估计"、"大概"。
  不触发：当问题完全确定（如数学公式推导、事实核查）；当缺乏任何量化基础（无数据、无经验参考）；当决策时间极短且风险可忽略（日常小选择）。
  Invoke when facing uncertain decisions, risk assessments, or predictions about future events.
  Do NOT invoke when the problem is fully deterministic, lacks any quantitative basis, or when decision time is extremely short with negligible risk.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["first-principles", "inversion", "system-thinking", "occams-razor"]
---

# 概率思维 (Probabilistic Thinking)

## 核心定义

在不确定性条件下，不追求绝对正确，而是系统地量化概率、计算期望值，并根据新证据动态更新判断的思考方式。用数学语言描述不确定性，避免模糊表述。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

> 思维类 Skill 的核心模块。引导 Agent 怎么思考，不规定数据流转格式。
> 4-8 个步骤，每步只写思考要点，不写输入/输出格式。
> 占全文 40-60% 篇幅。

### Step 1: 识别不确定性因素

- 列出所有关键不确定性因素（未知变量、随机事件、信息缺失处）
- 区分已知已知、已知未知、未知未知
- 评估每个因素的可量化性和数据来源
- 标注假设前提

---

### Step 2: 量化概率分布

- 对每个因素分配概率（点估计或区间分布）
- 标注置信水平（如"60%~80%"）
- 使用参考类预测（reference class）校准
- 记录概率赋值的依据

---

### Step 3: 构建决策模型

- 画决策树或计算期望值（EV = Σ 概率 × 效用）
- 考虑时间价值、风险偏好调整
- 对比各选项的期望值、最坏情况、最好情况
- 检查是否存在不可接受的极端损失

---

### Step 4: 考虑风险偏好与边界条件

- 根据决策者风险态度调整方案选择
- 风险规避者优先考虑保底，风险追求者关注高上限
- 检查是否存在不可接受的极端损失
- 评估风险调整后的候选方案

---

### Step 5: 动态更新

- 使用贝叶斯方法更新原有概率
- 新证据应系统性地修正原有概率，而不是完全抛弃或过度强调
- 重新计算期望值
- 标注更新幅度和原因

---

### Step 6: 校准与验证

- 定期检验主观概率与实际频率的匹配度
- 检查是否存在过度自信或确认偏误影响概率赋值
- 评估概率模型的复杂度和可解释性
- 留出"未知未知"的容错空间

---

### Step 7: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

> 使用此思维模型时必须遵守的原则。3-5 条。每条包含"原则 + 原因/后果"。

1. **量化优先**：用具体数字（0%~100%）代替模糊词语（"很可能"）。原因：避免歧义和认知偏误，提供可比较的基础。
2. **期望值决策**：在多数情况下选择期望收益最高的选项，同时考虑风险容忍度。原因：长期遵循期望值决策能获得最优累积收益。
3. **贝叶斯更新**：新证据应系统性地修正原有概率。原因：避免完全抛弃先验或过度强调新证据，保持判断的稳定性。
4. **校准信心**：定期检验主观概率与实际频率的匹配度。原因：改善判断准确性，识别系统性偏差。
5. **警惕未知未知**：概率计算只能覆盖已知不确定因素。原因：需留出容错空间（如冗余、保险、对冲）应对不可预见事件。

---

## 自检清单

> 聚焦概率思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**概率思维特有关键检查项**：

- [ ] **是否用具体数字替代了模糊词语？** "很可能"是否被转化为"60%-80%"？
- [ ] **概率赋值是否有依据？** 是参考类预测、历史数据还是纯粹直觉？
- [ ] **是否考虑了"未知未知"？** 概率计算是否覆盖了所有已知不确定因素？
- [ ] **期望值计算是否完整？** 最坏情况、最好情况和期望收益是否都被呈现？
- [ ] **风险偏好是否被纳入决策？** 期望收益最高的选项是否也符合决策者的风险承受力？
- [ ] **主观概率是否经过了校准检验？** 是否存在过度自信导致概率偏离实际频率？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [bayesian-updating](../thinking/bayesian-updating/SKILL.md) | 并行 | 贝叶斯更新是概率思维的具体实现机制，两者常结合使用 |
| [decision-tree](../thinking/decision-tree/SKILL.md) | 后置 | 概率思维为决策树提供输入参数，决策树是概率的结构化表达 |
| [second-order-thinking](../thinking/second-order-thinking/SKILL.md) | 并行 | 评估概率时，考虑事件连锁反应的二阶、三阶概率 |
| [inverse-thinking](../thinking/inverse-thinking/SKILL.md) | 前置 | 在概率评估前，先识别可能导致失败的极端场景 |

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

1. Kahneman, D., & Tversky, A. (1974). Judgment under uncertainty: Heuristics and biases. *Science*, 185(4157), 1124-1131.
2. Tetlock, P. E., & Gardner, D. (2015). *Superforecasting: The Art and Science of Prediction*. Crown.
3. Taleb, N. N. (2001). *Fooled by Randomness: The Hidden Role of Chance in Life and in the Markets*. Random House.
4. Gigerenzer, G. (2002). *Calculated Risks: How to Know When Numbers Deceive Us*. Simon & Schuster.
