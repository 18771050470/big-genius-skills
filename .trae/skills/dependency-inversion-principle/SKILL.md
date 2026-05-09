---
name: dependency-inversion-principle
description: |
  触发：当设计模块间依赖关系、评估高层模块是否被低层实现绑定、需要让核心业务逻辑不依赖具体技术实现时调用；常见信号包括"改数据库从MySQL到PostgreSQL要不要改业务逻辑"、"这个Service直接new了具体实现怎么测试"、"高层策略怎么不被低层细节绑死"、"想替换第三方库但改动太大"。
  不触发：当模块本身就没有稳定抽象（原型阶段快速试错）；当具体实现极不可能变化（如JDK核心类String）；当引入抽象层带来的间接性超过未来可替换性的收益时。
  Invoke when designing module dependencies, evaluating if high-level modules are bound to low-level implementations, or decoupling business logic from technical details.
  Do NOT invoke when modules have no stable abstraction (prototype phase), when concrete implementations are extremely unlikely to change, or when the indirection cost exceeds the future substitutability benefit.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["open-closed-principle", "interface-segregation-principle", "dependency-injection", "single-responsibility-principle"]
---

# 依赖倒置原则（Dependency Inversion Principle）

## 核心定义

高层模块不应依赖低层模块，两者都应依赖抽象。抽象不应依赖细节，细节应依赖抽象。把依赖关系"倒过来"——让容易变化的东西（具体实现）依赖稳定的东西（抽象接口），而不是反过来。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充高层策略和低层实现的具体技术栈
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告抽象层成本与未来灵活性收益的矛盾，等待决策
- **提前终止**：若具体实现几乎不可能变化（如不打算换数据库/框架），可提前终止并标注"该依赖不值得倒置"

---

## 思考流程

### Step 1: 识别当前依赖方向

- 绘制当前模块的依赖图：谁依赖谁？
- 标注高层模块（业务策略、核心逻辑）和低层模块（数据库、网络、文件系统、第三方库）
- 检查依赖箭头：高层→低层？低层→高层？
- 典型的DIP违反：Service → RepositoryImpl → 具体的JDBC/ORM类
- 判断标准：如果我想替换低层实现时，高层代码是否需要修改？

---

### Step 2: 提取稳定的抽象

- 为低层模块定义抽象接口——接口由高层模块的需求决定，不是由低层模块的实现倒推
- 接口应该表达高层模块"希望底层做什么"，而非"底层能做什么"
- 例如：业务层说"我需要保存订单" → 定义 OrderRepository 接口（高层拥有）
- 不要让底层数据库的细节污染接口：接口参数是领域对象，不是SQL语句

---

### Step 3: 反转依赖方向

- 让低层模块实现高层定义的抽象接口
- 依赖箭头变为：低层 → 高层抽象
- 原来的依赖（高层→低层具体类）被打破
- 具体实现类的创建推迟到运行时（通过依赖注入、工厂模式、服务定位器）
- 验证结果：低层修改不影响高层编译，高层测试可以用Mock替代低层

---

### Step 4: 评估依赖倒置的代价

- 增加了接口/抽象类的数量 → 代码量的增加
- 增加了间接性 → 调试时需要在接口和实现之间跳转
- 抽象设计的难度 → 需要预见"哪些行为是稳定的"和"哪些是可能变化的"
- 判断准则：倒置带来的可替换性价值 > 间接性成本？
- 优先级：对外接口 > 容易变化的第三方库 > 稳定的标准库（可不倒置）

---

### Step 5: 总结输出

- 输出当前依赖关系图和DIP违反清单
- 输出抽象接口设计方案：每个关键依赖点定义什么接口
- 标注不倒置的依赖及理由
- 输出应包含：结论 + 抽象接口 + 依赖图 + 不倒置清单 + 关键假设 + 风险

---

## 关键原则

1. **高层拥有接口**：抽象接口定义在高层模块中，而非低层模块中。原因：接口是契约——契约应该由使用方起草。如果接口定义在低层，低层变更时接口跟着变，高层还是被低层牵着走。
2. **抽象稳定于细节**：抽象的接口应该比具体实现更稳定——接口不应该频繁变化，实现换了一茬又一茬。原因：如果抽象本身不稳定（频繁修改），DIP就没有意义——你还是得频繁修改依赖方代码。
3. **不是每个依赖都需要倒置**：String、ArrayList、File等标准库/语言内置类不需要倒置。原因：DIP针对的是"容易变化的具体实现"，不是所有具体类。标准库极度稳定，倒置反而增加不必要的间接性。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**DIP特有关键检查项**：

- [ ] **高层模块是否定义了自己的接口？** 接口是否在高层包中而非低层包中？
- [ ] **替换低层实现时高层代码是否需要修改？** 核心验证——如果修改了就是DIP违反
- [ ] **接口是由高层的需求驱动的吗？** 还是被低层实现反向塑形的？
- [ ] **抽象是否足够稳定？** 接口变动频率是否低于实现变动频率？
- [ ] **是否保留了不倒置的正当理由？** 标准库/极稳定依赖是否被误倒了？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [open-closed-principle](../open-closed-principle/SKILL.md) | 目标 | DIP是实现OCP的机制——依赖倒置后，替换实现=添加新代码（OCP满足） |
| [interface-segregation-principle](../interface-segregation-principle/SKILL.md) | 前置 | ISP先瘦身接口，DIP再让高层依赖这些瘦接口 |
| [single-responsibility-principle](../single-responsibility-principle/SKILL.md) | 前置 | SRP确定"谁定义这个接口"，DIP确保"接口在正确的位置" |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱 |

---

## 参考文献

1. Martin, R. C. (2003). *Agile Software Development: Principles, Patterns, and Practices*. Pearson. Chapter 11: DIP.
2. Martin, R. C. (2017). *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall. Chapter 11: DIP.
3. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. (Strategy, Bridge, Abstract Factory等体现DIP的模式)

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
