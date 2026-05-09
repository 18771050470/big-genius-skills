# SKILL.md

```markdown
---
name: model-thinking
description: |
  触发：当面对复杂现实需要简化理解、预测或决策时调用；常见信号包括“这个问题太复杂了”、“我们能不能有个框架来分析”、“如何预测趋势”、“解释这个现象的本质”。
  不触发：当问题已高度结构化且有现成解决方案时；当只需执行具体操作无需抽象建模时；当现实过于简单不需要模型简化时。
  Invoke when facing complex reality needing simplified understanding, prediction, or decision-making; signals include "this is too complex", "can we have a framework", "how to predict trends", "explain the essence of the phenomenon".
  Do NOT invoke when the problem is already highly structured with ready-made solutions; when only executing specific operations without need for abstract modeling; when reality is too simple to require model simplification.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["first-principles", "systems-thinking", "thought-experiment"]
---

# 模型思维 (Model Thinking)

## 核心定义

**模型思维** 是“用简化的模型代替复杂现实来理解和预测”的认知框架。其核心信条是乔治·博克斯的名言：“所有模型都是错的，但有些是有用的。” 模型不是现实本身，而是我们为了理解、预测和决策而创造的抽象简化工具。

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

## 思考流程

### Step 1: 界定问题与目标

- 明确要理解/预测的核心现象；确定时间范围、边界和约束；区分“已知”和“未知”
- 清晰的问题陈述（如“未来三个月用户留存率趋势如何？”）

### Step 2: 选择备选模型

- 从记忆或知识库中检索相关模型（如幂律分布、S曲线、马尔可夫链、线性回归、系统动力学模型等）；列出至少2-3个候选模型，并记录各自的假设
- 候选模型列表及其假设清单

### Step 3: 模型匹配与初步映射

- 将现实数据的特征与模型假设进行匹配；判断哪个模型的简化方式最能保留问题的本质；忽略次要细节
- 选定的模型 + 初步参数/状态估计

### Step 4: 应用模型进行推理

- 模拟或推导模型的行为；预测结果或解释因果机制；用模型语言重新描述问题
- 模型推理结果（预测值、趋势曲线、关键杠杆点等）

### Step 5: 验证与敏感性分析

- 检查预测是否与现有数据矛盾；调整参数看结果变化幅度；识别“若假设不成立”的鲁棒性
- 置信度评估 + 模型脆弱点清单

### Step 6: 提炼洞见与决策

- 将模型结论转化为通俗洞见；指出“模型的错的”部分（即简化忽略了什么）；给出基于模型但需结合经验的行动建议
- 最终结论、行动建议、模型局限声明

## 关键原则

1. **简化是必要的，但必须保留本质** - 模型必须去掉无关细节，但保留驱动结果的关键变量和关系。原因：保留太多细节会使模型如同现实一样复杂而失去解释力；去掉过多则模型无用。
2. **所有模型都有假设，必须明示并质疑** - 每个模型依赖的简化假设（如线性关系、独立性、均衡态等）必须被明确列出并审查是否合理。原因：模型的“有用”程度取决于假设与现实的匹配度；隐藏假设会导致误用。
3. **模型是工具，不是答案** - 模型提供框架和洞见，而非真理。决策时需要结合经验、直觉、伦理等非模型因素。原因：现实永远比模型复杂，过度依赖模型会导致“模型迷恋”错误。
4. **模型需要被不断修正** - 随着新数据、新反馈的出现，模型应被调整或替换。原因：所有模型都是暂时正确的，保持模型鲜活才能持续有用。
5. **多个模型优于单一模型** - 用多个不同视角的模型分析同一问题，能得到更稳健的洞见。原因：每个模型都“错”在不同方面，综合多个模型能弥补各自的盲区。

## 自检清单

> 聚焦模型思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**模型思维特有关键检查项**：

- [ ] **问题范围是否被清楚界定？** 是否避免了"万能模型"陷阱——用一个模型解释一切？
- [ ] **是否列出了至少2个候选模型？** 单一模型的假设是否被充分审视？
- [ ] **所选模型的关键假设是否被明确？** 假设与现实的匹配度是否被审慎评估？
- [ ] **是否承认"所有模型都是错的"？** 模型输出是否被当作近似值而非真理？
- [ ] **是否做了敏感性分析？** 哪些参数变化对模型结论影响最大？
- [ ] **模型结论是否被翻译为易懂洞见？** 纯数字输出是否被转化为可理解的洞察？
- [ ] **决策中是否保留了非模型判断空间？** 直觉、经验、伦理等是否被纳入？
- [ ] **模型的版本和局限是否被记录？** 未来迭代和修正的基础是否被建立？

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [first-principles](../thinking/first-principles/SKILL.md) | 并行 | 当需要验证模型假设是否基于基本事实时，先用第一性原理拆解，再建立简化模型 |
| [systems-thinking](../thinking/systems-thinking/SKILL.md) | 前置 | 模型思维依赖对系统结构的理解——先用系统思维识别要素和关系，再选择合适模型 |
| [thought-experiment](../thinking/thought-experiment/SKILL.md) | 并行 | 当无法获取真实数据时，通过思维实验来"运行"模型，检测模型的行为和边界 |
| [abstraction](../thinking/abstraction/SKILL.md) | 前置 | 模型本质是抽象——需要先抽象出问题的关键特征，才能构建或选择模型 |

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Page, S. E. (2018). *The Model Thinker: What You Need to Know to Make Data Work for You*. Basic Books.
2. Simon, H. A. (1962). The Architecture of Complexity. *Proceedings of the American Philosophical Society*, 106(6), 467-482.
3. Sterman, J. D. (2000). *Business Dynamics: Systems Thinking and Modeling for a Complex World*. McGraw-Hill.
4. Epstein, J. M., & Axtell, R. (1996). *Growing Artificial Societies: Social Science from the Bottom Up*. MIT Press.
```

---