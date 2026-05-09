---
name: separation-of-concerns
description: |
  触发：当系统复杂度上升、模块职责混杂、需要提升可维护性时；当不同功能领域（UI/业务逻辑/数据访问）耦合在一起时；常见信号包括"这个模块做了太多事""改一处动全身""测试一个功能需要启动整个系统"。
  不触发：当系统非常简单（<100行）且拆分反而增加复杂度时；当性能要求极高且分离会带来不可接受的 overhead 时；当原型验证阶段快速迭代优先于结构清晰时。
  Invoke when system complexity rises, module responsibilities are mixed, or when different functional domains are tightly coupled.
  Do NOT invoke for very simple systems where separation adds overhead, when performance constraints prohibit separation, or during rapid prototyping where speed trumps structure.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["modular-thinking", "single-responsibility-principle", "abstraction-layering", "encapsulation-thinking"]
---

# 关注点分离（Separation of Concerns, SoC）

## 核心定义

将系统按功能职责划分为独立模块，每个模块只关注一件事，通过清晰的边界和接口降低复杂度、提升可维护性。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统规模、性能约束、团队结构信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若系统已清晰分离且无需调整，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别混杂的关注点

- 当前系统中哪些职责被混合在一起？
- 按功能维度分类：UI渲染、业务逻辑、数据访问、配置管理、日志记录、安全验证
- 按变化频率分类：哪些部分经常变，哪些很少变？
- 按团队维度分类：哪些部分由不同团队维护？
- 标注"关注点冲突热点"——改动最频繁、bug最集中的区域

### Step 2: 定义关注点的边界

- 每个关注点的职责范围是什么？输入和输出分别是什么？
- 关注点之间的依赖关系：谁依赖谁？依赖方向是否合理？
- 边界接口设计：用什么机制隔离？（函数接口、类接口、服务接口、消息队列）
- 避免"虚假分离"：表面分成不同文件，实际上仍然直接调用内部实现

### Step 3: 设计分离策略

- **水平分离**：按功能层分离（表现层/业务层/数据层）
- **垂直分离**：按业务领域分离（用户模块/订单模块/支付模块）
- **切面分离**：横切关注点分离（日志、安全、事务、监控）
- **分离粒度**：函数级、类级、模块级、服务级——选择合适粒度
- 评估每种策略对复杂度、性能、可测试性的影响

### Step 4: 处理依赖与通信

- 分离后的模块如何通信？同步调用还是异步消息？
- 依赖方向是否形成循环？如何打破循环依赖？
- 共享数据如何处理？避免"共享可变状态"成为新的耦合点
- 接口契约设计：版本兼容性、错误处理、超时机制

### Step 5: 验证分离效果

- **可测试性测试**：能否独立测试每个关注点？
- **可修改性测试**：修改一个关注点是否需要改动其他关注点？
- **可理解性测试**：新成员能否只读一个模块就理解其职责？
- **性能测试**：分离是否引入了不可接受的性能开销？
- 标注"分离泄漏点"——本应独立但实际上仍然耦合的地方

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **分离是手段不是目的**：分离是为了降低复杂度，如果分离本身增加了复杂度，需要重新评估。原因：过度分离会导致模块碎片化、接口膨胀、理解成本上升。
2. **接口是契约，不是建议**：一旦定义了模块边界，所有交互必须通过接口，禁止绕过接口直接访问内部实现。原因：接口是分离的保障，绕过接口等于没有分离。
3. **变化频率决定分离方式**：经常一起变化的关注点可以放在一起，变化频率不同的应该分离。原因：分离的核心价值是隔离变化的影响范围。
4. **警惕"分布式单体"**：表面拆分成多个服务，但所有服务必须同时部署、同时升级，这不是真正的分离。原因：独立部署是服务级分离的核心判据。

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
- [ ] 是否识别了所有混杂的关注点？是否标注了"关注点冲突热点"？
- [ ] 每个关注点的职责范围、输入输出是否被清晰定义？
- [ ] 分离策略是否被评估？水平分离、垂直分离、切面分离是否都被考虑？
- [ ] 依赖关系是否被分析？是否存在循环依赖？
- [ ] 共享数据处理方式是否被设计？是否避免了"共享可变状态"？
- [ ] 分离效果是否被验证？可测试性、可修改性、可理解性是否被测试？
- [ ] 是否识别了"分离泄漏点"和"虚假分离"？
- [ ] 输出具体可执行，不含模糊建议（如"拆分成模块"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [single-responsibility-principle](../thinking/single-responsibility-principle/SKILL.md) | 关联 | 每个模块/类只负责一件事，是SoC在面向对象中的具体应用 |
| [modular-thinking](../thinking/modular-thinking/SKILL.md) | 前置 | 先理解模块化思维，再应用关注点分离 |
| [abstraction-layering](../thinking/abstraction-layering/SKILL.md) | 并行 | 通过分层抽象实现关注点分离 |
| [encapsulation-thinking](../thinking/encapsulation-thinking/SKILL.md) | 关联 | 隐藏内部实现，只暴露必要接口，是SoC的实现手段 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | 思维模型的理论背景（可选） |

---

## 参考文献

1. Dijkstra, E. W. (1974). "On the Role of Scientific Thought". *Selected Writings on Computing: A Personal Perspective*, 60–66. Springer.
2. Parnas, D. L. (1972). "On the Criteria To Be Used in Decomposing Systems into Modules". *Communications of the ACM*, 15(12), 1053–1058.
3. Martin, R. C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship*. Prentice Hall.
4. Richards, M. (2015). *Software Architecture Patterns*. O'Reilly Media.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
