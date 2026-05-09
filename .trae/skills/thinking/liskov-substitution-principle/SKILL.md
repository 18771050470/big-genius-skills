---
name: liskov-substitution-principle
description: |
  触发：当设计继承体系、实现接口多态、评估子类是否合理替代父类时调用；常见信号包括"这个子类继承父类后有些方法用不了"、"子类抛出了父类没有的异常"、"子类改了父类方法的行为导致调用方出Bug"、"继承后子类违反父类契约"。
  不触发：当不使用继承/子类型多态时；当只是代码复用（非is-a关系）用组合即可时；当语言不支持传统继承时。
  Invoke when designing inheritance hierarchies, implementing interface polymorphism, or evaluating if a subclass can reasonably substitute its parent.
  Do NOT invoke when not using inheritance/subtype polymorphism, when composition suffices for code reuse, or when the language lacks traditional inheritance.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["contract-thinking", "open-closed-principle", "composition-over-inheritance", "interface-segregation-principle"]
---

# 里氏替换原则（Liskov Substitution Principle）

## 核心定义

子类（派生类型）必须能够完全替代其父类（基类型），而程序的行为不发生任何不符合预期——不是语法上能编译通过，而是行为语义上完全可替代。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充父类契约和行为语义
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告子类型无法替代父类型的根本矛盾，等待决策
- **提前终止**：若不使用继承体系、使用组合即可，可提前终止并标注"用组合替代继承绕过LSP问题"

---

## 思考流程

### Step 1: 明确父类的完整契约

- 不只是方法签名，更是行为的语义约定
- 列出父类所有公开方法的前置条件、后置条件、不变式
- 列出父类可能抛出的异常类型和含义
- 明确父类方法的隐含约定：返回值范围、副作用、线程安全性
- 这一步必须从调用方的视角出发：调用方对父类有什么合理期望？

---

### Step 2: 检查子类是否弱化了前置条件

- 子类的方法是否可以接受**更弱**（更宽松）的前置条件？
- 允许：父类要求参数 > 0，子类允许参数 >= 0（放宽了，调用方原来的参数仍然有效）
- 不允许：父类允许参数为null，子类不允许null（收紧了——原来传null的调用方会出错）
- 核心规则：前置条件不能被加强——调用方基于父类契约传参，子类不能拒绝父类接受的输入

---

### Step 3: 检查子类是否强化了后置条件

- 子类的方法是否保证**更强**（更严格）的后置条件？
- 允许：父类保证返回非null，子类保证返回非null且非空字符串（更强——调用方更安心）
- 不允许：父类保证返回非null，子类可能返回null（弱化了——调用方按父类契约期望非null会崩溃）
- 核心规则：后置条件不能被弱化——调用方基于父类契约使用返回值，子类不能提供更弱的保证

---

### Step 4: 检查子类是否违反了父类不变式

- 子类是否维护了父类定义的所有不变式？
- 父类不变式：例如"width和height必须始终为正"
- 如果子类允许width或height变为0或负值，就违反了不变式
- 子类可以添加自己的额外不变式（更强约束），但不能破坏父类的

---

### Step 5: 检查异常行为兼容性

- 子类抛出的异常必须是父类异常的子类型
- 子类不能抛出父类方法签名中未声明的受检异常（checked exception）
- 子类的异常语义必须与父类一致：父类的"NotFoundException"不能被子类的"SystemError"替代（语义完全不对）

---

### Step 6: 总结输出

- 输出LSP违反清单及每个违反点的具体修复建议
- 标注哪些违反是"必须修复"（会导致运行时崩溃），哪些是"建议修复"（语义不一致但不致崩溃）
- 输出应包含：结论 + 违反清单 + 修复方案 + 关键假设 + 风险

---

## 关键原则

1. **LSP是行为契约，不是语法规则**：编译通过 ≠ 符合LSP。原因：LSP的核心是行为语义——子类必须遵守父类的隐含约定，而不仅仅是方法签名一致。经典的"正方形不是矩形"反例：代码上正方形可以继承矩形，但setWidth(5)后getHeight()应该返回什么？（行为不一致）
2. **违反LSP = 违反OCP**：如果子类不能替代父类，所有依赖父类的代码都无法对扩展开放。原因：调用方需要 `instanceof` 检查或特殊分支处理特定子类→修改调用方代码→OCP被破坏。
3. **用组合规避LSP**：当继承关系本质上是代码复用而非is-a关系时，应该用组合。原因：LSP只约束继承——如果你不确定子类能否完全替代父类，大概率不该用继承。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**LSP特有关键检查项**：

- [ ] **父类的完整契约是否被明确列出？** 不仅是方法签名，还包括行为语义？
- [ ] **子类是否加强了任何前置条件？** 调用的入参范围是否被收窄？
- [ ] **子类是否弱化了任何后置条件？** 返回值的保证是否变差？
- [ ] **子类是否破坏了父类的不变式？** 有没有父类承诺"永远成立"的条件被子类违反？
- [ ] **异常行为是否兼容？** 子类抛出的异常类型和语义是否与父类一致？
- [ ] **是否认真考虑了"用组合替代继承"？** 如果LSP有违反，组合是否更合适？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [contract-thinking](../contract-thinking/SKILL.md) | 前置 | 契约思维定义父类的完整契约，LSP检查子类是否遵守 |
| [open-closed-principle](../open-closed-principle/SKILL.md) | 后置 | LSP保障后OCP才能正常工作 |
| [composition-over-inheritance](../composition-over-inheritance/SKILL.md) | 规避 | 当继承关系违反LSP时，用组合替代 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱 |

---

## 参考文献

1. Liskov, B., & Wing, J. M. (1994). "A behavioral notion of subtyping." *ACM Transactions on Programming Languages and Systems*, 16(6), 1811-1841.
2. Liskov, B. (1987). "Data abstraction and hierarchy." *OOPSLA '87 Keynote Address*.
3. Martin, R. C. (2003). *Agile Software Development: Principles, Patterns, and Practices*. Pearson. Chapter 10: LSP.
4. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley. Item 10: Obey the general contract when overriding equals. Item 18: Favor composition over inheritance.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
