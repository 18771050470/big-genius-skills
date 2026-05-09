---
name: open-closed-principle
description: |
  触发：当需要新增功能但又担心修改已有代码引入Bug、设计插件化架构时调用；常见信号包括"加新功能能不能不改老代码"、"这个if-else链越来越长了怎么扩展"、"怎么让组件支持新模式而不破坏现有模式"、"设计框架/库的扩展点时"。
  不触发：当修改已有代码是唯一合理方案时；当系统处于雏形阶段、过度抽象反而阻碍快速迭代时；当新功能与已有逻辑高度耦合无法干净分离时。
  Invoke when needing to add new functionality without modifying existing code to avoid introducing bugs, or when designing plugin architectures.
  Do NOT invoke when modifying existing code is the only reasonable approach, when the system is in nascent stages, or when new functionality is deeply coupled with existing logic.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["single-responsibility-principle", "composition-over-inheritance", "strategy-pattern", "dependency-inversion-principle"]
---

# 开闭原则（Open/Closed Principle）

## 核心定义

软件实体（类、模块、函数）应该对扩展开放——可以添加新行为；对修改关闭——不改变已有源代码就能做到。通过抽象和多态，让新功能以"添加新代码"而非"修改旧代码"的方式引入。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充未来的扩展方向和变化预期
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告过度抽象 vs 直接修改的权衡困境，等待决策
- **提前终止**：若系统当前稳定且无明确扩展需求，可提前终止并标注"YAGNI——等有扩展需求时再抽象"

---

## 思考流程

### Step 1: 识别变化维度

- 系统的哪些行为会随着时间变化？哪些是稳定的？
- 分析历史变更记录：过去半年哪些类型的修改最频繁？
- 区分"可能变化"和"确定会变化"——只对"确定会变化"做扩展准备
- 变化维度是OCP应用的前提：不知道该维度，OCP就是盲目抽象

---

### Step 2: 封装变化点

- 将每种变化可能性隔离到独立的模块/类中
- 策略模式：将算法族封装为可插拔的策略接口
- 插件架构：定义标准插件接口，新功能作为新插件加载
- 模板方法：固定算法骨架，可变步骤留给子类实现
- 核心做法：为变化维度定义抽象（接口/抽象类）

---

### Step 3: 面向抽象编程

- 让核心代码依赖抽象接口，而非具体实现
- 新功能 = 实现一个新类（实现已有接口），而非修改已有类的代码
- 验证：是否可以通过"添加新文件"而非"修改旧文件"来增加新功能？
- 如果需要修改旧文件，检查是否因为一开始没有为这个变化维度定义抽象

---

### Step 4: 评估扩展点的维护成本

- 每个抽象接口都是一份契约——需要维护、测试、文档
- 过多的扩展点会增加系统的认知负荷
- 策略模式的成本：N个策略类 + 1个接口 + 1个上下文类 vs 1个if-else
- 判断标准：变化发生的概率 × 手工修改的成本 > 抽象的成本 → 值得抽象
- 抽象的程度应匹配变化的确定性：100%会变化→强抽象，20%可能→轻抽象

---

### Step 5: 总结输出

- 输出变化维度分析：哪些确定变化、哪些可能变化
- 输出抽象设计方案：为确定变化的方向定义哪些接口
- 输出成本收益评估：抽象的代价是否被未来的修改成本所cover
- 输出应包含：结论 + 变化维度 + 抽象方案 + 成本评估 + 关键假设 + 风险

---

## 关键原则

1. **抽象跟随变化**：只为确定会变化的维度做抽象。原因：OCP最常见误用就是过度抽象——为"可能"的变化预埋扩展点，结果80%的扩展点从未被用上。
2. **开闭针对的是"修改的涟漪效应"**：OCP的目标不是"永远不改代码"，而是修改一个功能不需要连锁修改多个文件。原因：修改范围可控是OCP的核心价值，并非吹毛求疵地禁止修改。
3. **先做对，再做抽象**：不要试图一开始就设计完美的抽象。原因：Kent Beck的建议——先让代码work，观察真实的变化模式，然后基于真实模式而非臆测做抽象。简单实现→发现重复→重构为抽象。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**OCP特有关键检查项**：

- [ ] **变化维度是否有真实数据支撑？** 是基于历史变更记录还是纯猜测？
- [ ] **抽象是否足够稳定？** 接口定义会不会在可预见的未来也需要修改？
- [ ] **"添加新功能"是否真的只需要添加新文件？** 是否需要修改工厂类/注册表？
- [ ] **抽象的成本是否被量化和评估？** 接口 + N个实现类 vs 一个if-else的认知负荷对比？
- [ ] **是否避免了为"可能"变化做的过度抽象？** 是否有未使用的扩展点？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [single-responsibility-principle](../single-responsibility-principle/SKILL.md) | 前置 | SRP拆分职责后，OCP确保每个独立模块对扩展开放 |
| [dependency-inversion-principle](../dependency-inversion-principle/SKILL.md) | 后置 | DIP提供依赖反转的机制，OCP是DIP的目标 |
| [composition-over-inheritance](../composition-over-inheritance/SKILL.md) | 并行 | 组合提供比继承更灵活的扩展方式 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱 |

---

## 参考文献

1. Meyer, B. (1988). *Object-Oriented Software Construction*. Prentice Hall. (OCP的原始出处——Meyer提出了开闭原则)
2. Martin, R. C. (2003). *Agile Software Development: Principles, Patterns, and Practices*. Pearson. Chapter 9: OCP.
3. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. (Strategy, Template Method, Decorator等体现OCP的模式)

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
