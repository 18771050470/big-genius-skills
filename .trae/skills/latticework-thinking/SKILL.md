---
name: latticework-thinking
description: |
  触发：当需要跨学科整合知识、构建多维认知框架、避免单一思维模型偏差时调用；常见信号包括"这个问题从不同学科角度看会怎样"、"有没有更全面的分析框架"、"单一视角不够用"。
  不触发：当问题明确属于单一学科领域时；当只需应用一个特定思维模型即可解决时；当跨学科整合会导致分析瘫痪时。
  Invoke when needing to integrate knowledge across disciplines, build multi-dimensional cognitive frameworks, or avoid single-model bias.
  Do NOT invoke when the problem clearly belongs to a single discipline, when a single thinking model suffices, or when cross-disciplinary integration would lead to analysis paralysis.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["model-thinking", "system-thinking", "holism", "probabilistic-thinking"]
---

# 思维格栅（Latticework Thinking）

## 核心定义

将来自不同学科的核心概念编织成相互关联的认知网络，用多维视角交叉验证问题，避免"手里只有锤子，看什么都是钉子"的单一思维偏差。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充问题背景和可用学科视角
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已整合足够学科视角且结论清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别问题的多维属性

- 分析问题涉及哪些维度：经济、心理、物理、生物、社会、技术等
- 每个维度对应哪些学科的核心概念？
- 哪些学科视角最可能提供洞察？
- 避免强行套用不相关学科的概念

---

### Step 2: 提取各学科核心模型

- 从每个相关学科中提取1-3个核心概念或定律
- 确保理解模型的本质，而非表面类比
- 标注每个模型的适用边界和前提假设
- 示例：经济学→机会成本、心理学→确认偏误、物理学→临界质量

---

### Step 3: 交叉应用与验证

- 用每个学科模型独立分析问题，得出各自结论
- 比较不同模型的结论：一致还是矛盾？
- 如果矛盾，哪个模型的前提假设更贴近当前问题？
- 寻找模型之间的互补性：A模型解释X，B模型解释Y

---

### Step 4: 整合为统一框架

- 将各模型的洞察编织成连贯的分析框架
- 识别模型之间的连接点：哪些概念在不同学科中有对应？
- 标注框架的覆盖范围和盲区
- 形成可复用的"格栅"：下次遇到类似问题可直接调用

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **模型必须来自真实学科**：不能发明伪概念。原因：格栅的力量来自经过验证的学科知识，而非个人臆想。
2. **理解模型的前提假设**：每个模型都有适用边界。原因：将模型应用到其假设不成立的场景会导致错误结论。
3. **交叉验证优于单一视角**：多个模型一致时结论更可靠。原因：不同学科独立发展出的模型如果指向同一结论，该结论的置信度更高。
4. **格栅是动态生长的**：不断学习新学科模型，丰富格栅。原因：格栅的价值随模型数量增长而非线性增加，而是指数增加。

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
- [ ] 引用的学科模型是否来自真实学科？是否有伪概念？
- [ ] 每个模型的前提假设是否被标注？
- [ ] 不同模型的结论是否被交叉验证？
- [ ] 矛盾结论是否被合理解释？
- [ ] 整合框架是否连贯，而非简单罗列？
- [ ] 输出具体可执行，不含模糊建议（如"多角度思考"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [model-thinking](../thinking/model-thinking/SKILL.md) | 前置 | 模型思维提供单个模型的使用方法，格栅思维整合多个模型 |
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 系统思维提供全局结构，格栅思维提供多学科视角 |
| [holism](../thinking/holism/SKILL.md) | 并行 | 整体论强调不可分割性，格栅思维强调多维交叉 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维提供量化框架，格栅思维提供定性视角 |

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

1. Munger, C. T. (1994). *The Worldly Wisdom*. USC Law School Speech.
2. Munger, C. T. (2005). *Poor Charlie's Almanack: The Wit and Wisdom of Charles T. Munger*. Donning Company Publishers.
3. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux.
4. Farnam Street. (2024). *Mental Models*. https://fs.blog/mental-models/

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
