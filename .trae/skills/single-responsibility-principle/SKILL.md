---
name: single-responsibility-principle
description: |
  触发：当评估一个类/模块/函数是否职责过多、需要拆分臃肿组件、设计新模块时需确定其边界时调用；常见信号包括"这个类太大了不好改"、"改一个功能要动好几个地方"、"这个模块的名字已经不能准确描述它干什么了"、"修改A功能竟然不小心影响了B功能"。
  不触发：当组件职责本身简单清晰且不太可能变化时；当过度拆分会导致碎片化和通信成本激增时；当组件处于原型阶段、职责边界尚未稳定时。
  Invoke when evaluating if a class/module/function has too many responsibilities, splitting bloated components, or defining module boundaries.
  Do NOT invoke when component responsibilities are simple and unlikely to change, when over-splitting causes fragmentation, or when the component is in prototype stage.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["open-closed-principle", "separation-of-concerns", "cohesion-thinking", "minimalism-thinking"]
---

# 单一职责原则（Single Responsibility Principle）

## 核心定义

一个模块（类、函数、包、服务）应该有且只有一个引起它变化的原因——一个模块只对一个角色（Actor）负责。不是"一个模块只做一件事"，而是"一个模块只为一个人/角色服务"。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充模块的使用者和变化原因
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告职责划分的困境，等待决策
- **提前终止**：若模块职责简单且所有变化来源归同一角色，可提前终止并标注"当前职责结构合理"

---

## 思考流程

### Step 1: 识别模块当前承担的所有职责

- 列出模块所有的公开方法和行为
- 按"为谁服务"（Actor/Role）分组：谁是这些功能的需求方？
- 典型Actor：业务团队、运维团队、数据团队、合规团队、用户体验团队
- 区分"计算相似"和"职责相同"：两个方法都操作User数据 ≠ 属于同一职责

---

### Step 2: 识别每个职责的变化来源

- 每个职责会因为谁的需求变更而修改？
- 典型变化来源：
  - 计算薪资的逻辑 → 财务部需求变化
  - 报表格式 → 管理层需求变化
  - 数据持久化 → DBA/基础设施需求变化
- 核心判断标准：如果两个子功能会因为**不同的人**的不同需求而分别修改，它们属于不同职责

---

### Step 3: 评估职责耦合的代价

- 当职责A需要修改时，职责B的代码是否也会被触及？
- 修改职责A时，是否可能意外破坏职责B？
- 两个职责是否需要不同的测试策略？不同的发布节奏？
- 多个职责共享的依赖（如数据库连接）是否阻碍了各自的独立演进？

---

### Step 4: 设计职责分离方案

- 按Actor维度拆分：为不同角色的需求创建独立的类/模块
- 提取变化的维度：将因不同原因变化的部分移到不同类中
- 保持高内聚：移走的是"不属于这个类的职责"，留下的是"紧密相关的职责"
- 命名验证：拆分后的每个类名字是否精准描述了它唯一的职责？
- 不是"拆得越细越好"——只有当不同的Actor确实有独立变化需求时才拆分

---

### Step 5: 总结输出

- 输出当前模块的职责分析：每个职责对应哪个Actor、哪些变化原因
- 输出拆分建议（如果需要）：如何将混在一起的职责分离
- 标注不拆分的理由（如果选择不拆）
- 输出应包含：结论 + 职责清单 + 拆分方案 + 关键假设 + 风险

---

## 关键原则

1. **"一个职责" = "一个变化原因"**：不要误解为"只做一件事"。原因：Bob Martin强调SRP的本质是"一个模块只对一个Actor负责"——两个耦合的功能如果因为同一个Actor的需求而同时变化，它们属于同一个职责。
2. **职责粒度与系统规模匹配**：微服务层级→一个服务=一个Actor，类层级→一个类=一个职责域。原因：在不同抽象层次，SRP的表现形式不同，不能用类的标准去要求微服务。
3. **先有变化后拆分**：不要过早拆分尚未发生变化的职责。原因：Martin Fowler的YAGNI原则——预测未来变化往往出错，等Actor确实提出矛盾需求时再拆分更经济。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**SRP特有关键检查项**：

- [ ] **职责是按Actor区分的吗？** 不是按"功能相似度"而是按"为谁服务"？
- [ ] **每个职责的变化来源是否被明确识别？** 谁会因为什么原因要求修改？
- [ ] **职责耦合是否引起了实际伤害？** 是否有证据表明两个职责的修改确实互相冲突？
- [ ] **拆分后的类名是否精确描述唯一职责？** "Manager"、"Handler"、"Processor"等泛化命名是危险信号
- [ ] **是否避免了过早拆分？** 对于尚未发生冲突变化的职责，是否保留了不拆分的选项？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [open-closed-principle](../open-closed-principle/SKILL.md) | 后置 | SRP拆分后，OCP确保每个小模块对扩展开放 |
| [separation-of-concerns](../separation-of-concerns/SKILL.md) | 父原则 | 关注点分离是SRP的上位概念，SRP是其特化 |
| [minimalism-thinking](../minimalism-thinking/SKILL.md) | 平衡 | 极简思维防止SRP过度拆分导致碎片化 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱 |

---

## 参考文献

1. Martin, R. C. (2003). *Agile Software Development: Principles, Patterns, and Practices*. Pearson. Chapter 8: SRP.
2. Martin, R. C. (2017). *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall. Chapter 7: SRP.
3. Martin, R. C. (2014). "The Single Responsibility Principle." *The Clean Code Blog*. https://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
