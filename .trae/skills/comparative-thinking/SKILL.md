---

## SKILL.md

```yaml
---
name: comparative-thinking
description: |
  触发：当需要对比两个或多个事物、方案、观点时调用；常见信号包括“比较”、“对比”、“区别”、“相似”、“优劣分析”、“A vs B”。
  不触发：当只需描述单一事物无需对比时；当对比对象完全相同或完全不同无需分析时；当决策只需基于单一维度且已明确时。
  Invoke when facing the need to compare multiple options, concepts, or scenarios to deepen understanding.
  Do NOT invoke when only describing a single thing without comparison; when comparison objects are identical or completely different requiring no analysis; when decisions are based on a single dimension that is already clear.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["analogical-thinking", "categorical-thinking", "systems-thinking", "decomposition-thinking"]
---
```

# 比较思维（Comparative Thinking）

## 核心定义

**比较思维** 是一种通过 **同中求异、异中求同** 来深化理解的认知工具。它要求我们：
- 在看似相同的事物中找出关键差异（同中求异）
- 在看似不同的事物中找出深层共性（异中求同）
- 区分 **本质差异** 和 **表面差异**，避免陷入简单的二元对立

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

## 思考流程

### Step 1: 明确比较目的与范围

- 定义比较的目标（选优？理解差异？迁移学习？）
- 确定比较范围（哪些对象需纳入，哪些不纳入）
- 列出关键比较维度（如性能、成本、复杂度、可维护性等）
- 比较目标 + 范围 + 维度清单

### Step 2: 分别理解每个对象

- 独立理解每个对象的核心特征、内在逻辑
- 避免过早将对象"捆绑"在一起比较，防止偏见
- 每个对象的独立概要

### Step 3: 同中求异——在相似中找到关键差异

- 先找出所有对象的共同点（表面相似 + 本质相似）
- 在共同基础上，逐一标记差异点
- 区分：哪些差异是"程度差异"（如响应时间 100ms vs 200ms），哪些是"性质差异"（如 SQL vs NoSQL）
- 共同点列表 + 差异点矩阵（含程度/性质标签）

### Step 4: 异中求同——在差异中发现深层共性

- 从差异中寻找背后的共同目标、约束、逻辑
- 将"不同解决方案"抽象为对"同一问题"的不同权衡
- 例如：微服务 vs 单体——都是为满足业务能力，但不同阶段
- 深层共性列表 + 权衡光谱

### Step 5: 区分本质差异与表面差异

- 逐项评估差异的影响程度（改变该差异会根本改变结果吗？）
- 排除表面差异（如颜色、命名、次要细节）
- 保留本质差异（如架构范式、数据一致性模型、安全策略）
- 本质差异清单（高影响）+ 表面差异清单（低影响）

### Step 6: 探究差异根源与逻辑

- 对每个本质差异，追问"为什么会产生这种差异？"
- 分析：是由于设计目标不同？历史演变？技术限制？
- 理解差异背后的取舍（trade-off）和优化方向
- 差异原因分析表 + 取舍逻辑图

### Step 7: 综合形成洞见与决策建议

- 从比较中提炼一条核心洞见（如"A更适合快速迭代，B适合稳定生产"）
- 如果有决策需求，给出基于本质差异的推荐
- 指出比较的局限性（例如：未考虑 X 维度，或数据时间差）
- 核心洞见 + 比较总结表 + 决策建议（可选）

## 关键原则

| 原则 | 说明 | 为什么重要 |
|------|------|-----------|
| **1. 避免二元对立** | 不简单说“A好B坏”，而是分析在什么上下文下各自优劣 | 二元对立掩盖了中间状态和条件依赖，导致错误决策 |
| **2. 同中求异 + 异中求同** | 两种方向缺一不可 | 只求异会陷入琐碎差异；只求同会忽略关键区别 |
| **3. 区分本质与表面** | 表面差异往往与目标无关，本质差异决定结果 | 混淆两者会导致耗费精力在无关细节上 |
| **4. 追溯差异原因** | 不仅看到不同，更理解为什么不同 | 理解原因才能预测在不同环境下差异是否会持续 |
| **5. 保持上下文敏感性** | 比较结果不能脱离场景（团队、阶段、约束） | 一个场景下的最优解在另一场景可能完全错误 |

## 自检清单

> 聚焦比较思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**比较思维特有关键检查项**：

- [ ] **比较目的是否明确？** 选优、理解、迁移还是验证？不同目的对应不同比较策略？
- [ ] **是否分别独立理解了每个对象？** 还是直接对比导致了对每个对象的理解不足？
- [ ] **比较维度是否完整且相关？** 关键维度是否被遗漏？无关维度是否干扰了判断？
- [ ] **是否区分了本质差异与表面差异？** 表面差异是否被过度关注，本质差异是否被忽略？
- [ ] **是否追溯了差异的深层原因？** 设计目标、历史演变、技术限制等是否被分析？
- [ ] **是否避免了"谁更好"的二元叙事？** 结论是否是条件性的（"在X场景下A更好，在Y场景下B更好"）？
- [ ] **是否考虑了时间/环境变化后的时效性？** 当前比较结论在未来是否仍然成立？
- [ ] **是否标注了未覆盖的维度或假设？** 比较的局限性是否被诚实披露？

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [analogical-thinking](../thinking/analogical-thinking/SKILL.md) | 后置 | 从比较结果中建立类比，将洞见迁移到新问题 |
| [categorical-thinking](../thinking/categorical-thinking/SKILL.md) | 前置 | 在比较之前对对象进行归类，明确维度 |
| [systems-thinking](../thinking/systems-thinking/SKILL.md) | 并行 | 理解比较对象在更大系统中的相互作用与反馈 |
| [decomposition-thinking](../thinking/decomposition-thinking/SKILL.md) | 前置 | 当对象复杂时，先分解成可比较的子模块 |

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Gentner, D. (1983). Structure-mapping: A theoretical framework for analogy. *Cognitive Science*, 7(2), 155-177.
2. Medin, D. L., Goldstone, R. L., & Gentner, D. (1993). Respects for similarity. *Psychological Review*, 100(2), 254-278.
3. Markman, A. B., & Gentner, D. (1993). Structural alignment during similarity comparisons. *Cognitive Psychology*, 25(4), 431-467.