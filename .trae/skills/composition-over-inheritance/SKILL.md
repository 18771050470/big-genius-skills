---
name: composition-over-inheritance
description: |
  触发：当设计类结构、评估代码复用方式、面临"是否继承"决策时调用；常见信号包括"这个类应该继承还是组合？"、"继承层次太深"、"需要多重继承"、"父类修改导致子类异常"。
  不触发：当问题明显适合继承（严格的 is-a 关系，如"狗是动物"）时；当使用接口/协议实现多态时；当只需简单代码复用且继承不会引入耦合时。
  Invoke when designing class structures, evaluating code reuse approaches, or facing "inherit vs. compose" decisions.
  Do NOT invoke when the problem clearly fits inheritance (strict is-a relationship), when using interfaces/protocols for polymorphism, or when simple reuse without coupling is sufficient.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["solid-principles", "dependency-inversion", "interface-segregation", "design-patterns"]
---

# 组合优于继承思维（Composition Over Inheritance Thinking）

## 核心定义

优先通过组合对象（has-a）实现代码复用，而非通过继承（is-a）——继承是静态白盒复用，组合是动态黑盒复用，后者耦合更低、灵活性更高。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充类关系图、复用需求和变更预期
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确适合组合或继承且方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 评估 is-a 关系的真实性

- 子类是否真的是父类的特殊化？（Liskov 替换原则检验）
- 是否存在"正方形继承矩形"这类违反数学直觉的关系？
- 继承是否只是为了代码复用，而非真正的类型层次？
- 如果关系是"has-a"或"uses-a"，优先选择组合

---

### Step 2: 分析继承的耦合风险

- 父类实现细节是否暴露给子类？（白盒复用）
- 父类修改是否会破坏子类？（脆弱基类问题）
- 继承层次是否超过 3 层？（深度继承增加理解成本）
- 是否需要多重继承？（多数语言不支持或支持有限）

---

### Step 3: 设计组合方案

- 识别可复用的行为单元（策略、状态、能力）
- 将行为封装为独立类/接口
- 通过构造函数或 setter 注入依赖
- 使用委托（delegation）将调用转发给组件

---

### Step 4: 评估组合的优势

- 运行时动态替换组件（灵活性）
- 组件变更不影响宿主类（低耦合）
- 避免继承层次爆炸（可维护性）
- 支持行为的正交组合（一个类可同时拥有多种独立行为）

---

### Step 5: 选择实现策略

- **策略模式**：封装算法族，让它们可以互相替换
- **状态模式**：封装状态相关的行为
- **装饰器模式**：动态添加职责
- **依赖注入**：通过构造函数注入组件
- **接口/协议**：定义行为契约，多种实现可互换

---

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **is-a 才继承，has-a 应组合**：继承表示类型层次，组合表示能力组装。原因：错误的继承关系会违反 Liskov 替换原则，导致运行时异常和逻辑错误。
2. **继承是静态的，组合是动态的**：继承在编译时确定，组合可在运行时调整。原因：业务需求变化时，动态组合更容易适应，无需重构类层次。
3. **继承暴露实现，组合隐藏实现**：子类依赖父类内部实现细节，组合仅依赖接口。原因：暴露实现细节导致脆弱基类问题，父类修改可能级联破坏所有子类。
4. **多重行为用组合，单一层次用继承**：一个类需要多种独立行为时，组合比多重继承更清洁。原因：多重继承引入菱形继承问题，组合可正交叠加多种行为。

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
- [ ] **组合优于继承特供**：是否验证了 is-a 关系的真实性？是否通过 Liskov 替换原则检验？
- [ ] **组合优于继承特供**：是否分析了继承的耦合风险？父类修改是否会导致子类异常？继承层次是否超过3层？
- [ ] **组合优于继承特供**：是否识别了可复用的行为单元？行为是否被封装为独立类/接口？
- [ ] **组合优于继承特供**：是否评估了组合的优势？运行时灵活性、低耦合、正交组合是否被考虑？
- [ ] **组合优于继承特供**：是否选择了合适的实现策略？策略模式、状态模式、装饰器模式、依赖注入是否被正确匹配？
- [ ] **组合优于继承特供**：是否检查了"为了复用而继承"的反模式？代码复用是否通过组合实现？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"多用组合"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [solid-principles](../solid-principles/SKILL.md) | 前置 | SOLID 原则中的 Liskov 替换原则和依赖倒置原则为组合优于继承提供理论基础 |
| [dependency-inversion](../dependency-inversion/SKILL.md) | 并行 | 依赖倒置要求依赖抽象，组合通过接口注入实现这一点 |
| [interface-segregation](../interface-segregation/SKILL.md) | 并行 | 接口隔离原则帮助设计细粒度的行为接口，便于组合 |
| [design-patterns](../design-patterns/SKILL.md) | 后置 | 设计模式（策略、状态、装饰器）提供组合的具体实现方案 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | GoF 设计模式理论背景 |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley.
2. Meyer, B. (1997). *Object-Oriented Software Construction* (2nd ed.). Prentice Hall.
3. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley. Item 18: Favor composition over inheritance.
4. Martin, R. C. (2002). *Agile Software Development: Principles, Patterns, and Practices*. Prentice Hall.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
