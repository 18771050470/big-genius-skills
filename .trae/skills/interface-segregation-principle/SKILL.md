---
name: interface-segregation-principle
description: |
  触发：当设计接口/抽象类时评估其是否过于臃肿、当调用方被迫依赖它不需要的方法时调用；常见信号包括"这个接口太大了我只需要其中一个方法"、"实现接口时要写一堆空方法或throw UnsupportedOperationException"、"修改接口的一个方法导致所有实现类都要重新编译部署"。
  不触发：当接口本来就只有1-2个方法、所有实现方都需要全部方法时；当接口是稳定的行业标准（如JDK的Collection接口）且调用方接受其复杂度时。
  Invoke when designing interfaces and evaluating if they're too bloated, or when callers are forced to depend on methods they don't need.
  Do NOT invoke when interfaces are naturally small (1-2 methods), when all implementors genuinely need all methods, or when the interface is a stable industry standard.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["single-responsibility-principle", "dependency-inversion-principle", "minimalism-thinking", "contract-thinking"]
---

# 接口隔离原则（Interface Segregation Principle）

## 核心定义

客户端不应该被迫依赖它不使用的方法——臃肿的接口应该被拆分为更小、更专注的接口。不是"接口应该小"，而是"接口应该精准匹配每个客户端的实际需要"。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充接口的所有客户端和使用场景
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告接口拆分粒度权衡的矛盾，等待决策
- **提前终止**：若接口自然小巧且所有客户端都需要全部方法，可提前终止并标注"无需隔离"

---

## 思考流程

### Step 1: 列出接口的所有客户端

- 谁是接口的使用者和实现者？
- 每个客户端实际调用了接口的哪些方法？哪些方法被哪些客户端调用？
- 绘制方法-客户端矩阵：清晰展示"谁需要什么"
- 区分主动使用（客户端真的调用了）和被动依赖（接口存在但不使用）

---

### Step 2: 识别"胖接口"的症状

- 是否存在实现类需要 `throw new UnsupportedOperationException()` 的方法？
- 是否存在实现类对某些方法返回 `null` 或空实现？
- 接口的某个方法修改后，不相关的实现类也被迫重新编译/部署？
- 客户端代码的import中有接口，但只用到了接口中30%的方法？
- 接口的方法签名是否暗示了它们属于不同的角色？（如save()和sendEmail()属于不同关注点）

---

### Step 3: 按客户端角色拆分接口

- 将接口的方法按"哪些客户端需要它们"分组
- 为每组客户端定义独立的精简接口（Role-specific Interface）
- 调用方A只依赖接口A（只含A需要的方法），调用方B只依赖接口B
- 一个类可以实现多个小接口——这比实现一个胖接口更清晰
- 让原本实现胖接口的类改为实现多个小接口（或通过组合委托）

---

### Step 4: 评估拆分后的收益和代价

- 收益：修改接口A不影响接口B的客户端，编译/部署独立性
- 收益：接口更容易理解和实现，新人不需要理解不需要的方法
- 代价：接口数量增加，类需要声明实现多个接口
- 现代语言的默认方法（default method）可以减轻拆分的痛苦——小接口 + default方法提供向后兼容

---

### Step 5: 总结输出

- 输出当前接口的方法-客户端矩阵
- 输出拆分方案：每个角色接口包含哪些方法
- 标注拆分的成本和收益
- 输出应包含：结论 + 拆分方案 + 成本评估 + 关键假设 + 风险

---

## 关键原则

1. **接口属于客户端，不属于实现方**：接口的定义应该由"调用方需要什么"来决定，而不是"实现方有什么"。原因：接口是客户端和实现方之间的契约——契约的起草应优先照顾使用方的需求。
2. **胖接口的伤害是间接且持续的**：一个客户端对胖接口的修改，会连锁影响所有实现方和其他客户端。原因：接口的耦合效应——修改胖接口的任何一个方法，所有依赖该接口的代码都被迫参与变更。
3. **拆分粒度要平衡**：不要把所有方法都拆成单方法接口。原因：每个接口都是抽象层，太多抽象层导致导航和理解困难——接口隔离的目标是"精准匹配"，不是"最小化"。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**ISP特有关键检查项**：

- [ ] **方法-客户端矩阵是否被绘制？** 每个客户端实际使用了哪些方法？
- [ ] **是否存在"空实现"或`UnsupportedOperationException`？** 这是胖接口的最大症状
- [ ] **拆分后的每个接口是否对应一个明确的客户端角色？** 接口名是否体现角色？
- [ ] **拆分粒度是否合理？** 有没有过度拆分到单方法接口（反之亦然）？
- [ ] **修改一个接口是否不影响其他接口的客户端？** 核心价值是否实现？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [single-responsibility-principle](../single-responsibility-principle/SKILL.md) | 进阶 | SRP是"一个类一个职责"，ISP是"一个接口一个角色" |
| [dependency-inversion-principle](../dependency-inversion-principle/SKILL.md) | 后置 | ISP拆分接口后，DIP确保底层依赖高层定义的小接口 |
| [minimalism-thinking](../minimalism-thinking/SKILL.md) | 并行 | 极简思维帮你砍掉接口中不是每个客户都需要的方法 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱 |

---

## 参考文献

1. Martin, R. C. (2003). *Agile Software Development: Principles, Patterns, and Practices*. Pearson. Chapter 12: ISP.
2. Martin, R. C. (1996). "The Interface Segregation Principle." *Engineering Notebook, C++ Report*.
3. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley. Item 20: Prefer interfaces to abstract classes. Item 21: Design interfaces for posterity.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
