---
name: anti-corrosion-thinking
description: |
  触发：当需要集成遗留系统/外部系统、防止其设计缺陷和技术债务污染核心领域模型时调用；常见信号包括"老系统的烂设计会不会影响新系统"、"怎么隔离第三方API的不稳定性"、"新旧系统对接时如何保护新系统的架构"、"API变更时不想改核心逻辑"。
  不触发：当集成的是内部系统且架构风格一致、双向透明时；当集成只是简单的数据透传无需翻译时；当外部系统本身就是项目的一部分且可控时。
  Invoke when integrating legacy/external systems and needing to prevent their design flaws and technical debt from polluting the core domain model.
  Do NOT invoke when integrating internal systems with consistent architecture, when integration is simple data passthrough, or when the external system is fully controlled.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["contract-thinking", "boundary-thinking", "separation-of-concerns", "domain-driven-design"]
---

# 防腐思维（Anti-Corruption Thinking）

## 核心定义

在系统边界设置隔离层，主动将外部系统（遗留系统、第三方服务）的不良设计转化为内部领域模型可接受的形式，防止外部腐化向内部扩散。不是被动防御，是主动翻译。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充外部系统的接口和数据格式
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告防腐层代价与收益的矛盾（如翻译逻辑过于复杂），等待决策
- **提前终止**：若外部系统设计良好好且与内部模型直接兼容、不需要翻译层，可提前终止并标注"无腐化风险，无需防腐层"

---

## 思考流程

### Step 1: 识别腐化源头

- 列出所有与当前系统交互的外部系统（遗留代码、第三方API、外部数据源）
- 评估每个外部系统可能带来的腐化类型：
  - 概念腐化：外部术语与内部领域语言不一致（如外部叫"客户"，内部叫"用户"）
  - 结构腐化：外部数据模型（宽表、JSON字段）与内部领域模型（聚合、值对象）不匹配
  - 行为腐化：外部API的错误处理模式、超时行为与内部约定不一致
  - 协议腐化：外部通信协议（SOAP、旧版REST）与内部协议（gRPC、GraphQL）不兼容
- 标注每个腐化源的影响范围和扩散路径

---

### Step 2: 评估腐化扩散风险

- 如果不隔离，外部设计会如何影响内部代码？
- 外部API变更时，有多少内部代码需要同步修改？修改范围是几个文件还是几十个文件？
- 新团队成员是否会"参考"外部代码风格，导致腐化扩散到新代码？
- 外部系统是否有明确的生命周期？可能被替换或升级吗？
- 计算"不隔离"的总拥有成本 vs "隔离"的成本

---

### Step 3: 设计防腐层隔离策略

- 翻译层（Translation Layer）：映射外部概念到内部领域语言
  - 数据转换：外部DTO → 内部Domain Object
  - 概念映射：外部"Order" → 内部"Purchase"（语言对齐）
- 适配器层（Adapter）：封装外部API的调用细节
  - 协议适配：SOAP → REST / gRPC
  - 错误适配：外部各类异常 → 内部统一异常体系
- 门面层（Facade）：简化外部复杂接口，暴露最小必要接口给内部
- 策略选择：是翻译整个外部模型（全量防腐），还是只隔离差异部分（增量防腐）？

---

### Step 4: 实现防腐层

- 防腐层必须是一等公民代码：有自己的测试、文档、版本管理
- 单向依赖：内部核心领域永远不直接依赖外部系统，只依赖防腐层接口
- 防腐层内部可以"脏"（容纳外部模型的混乱），但对外暴露的接口必须"干净"（符合内部领域模型）
- 错误隔离：外部异常在防腐层内被捕获并转化为内部异常类型，不向外泄漏
- 设置明确的边界：哪些属于防腐层，哪些属于核心领域，不可混在一起

---

### Step 5: 维护和演进防腐层

- 监控外部API变更：订阅外部系统的变更日志/版本升级通知
- 定期审计：防腐层是否还在有效翻译？是否有遗漏的腐化路径？
- 当外部系统升级或替换时：只需修改防腐层内部实现，内部核心代码零变更——这才是防腐层价值的真正体现
- 警惕"防腐层自身腐化"：翻译逻辑堆积过多、成为新的技术债务。防腐层也需要定期清理

---

### Step 6: 总结输出

- 整合分析结果
- 输出腐化源清单、风险评估、防腐层设计方案
- 明确防腐层的边界和职责范围
- 输出应包含：结论 + 腐化评估 + 防腐策略 + 边界定义 + 维护计划 + 关键假设 + 风险

---

## 关键原则

1. **隔离先于集成**：先建立防腐层再连接外部系统，不要先连接再补隔离。原因：一旦外部腐化进入内部代码，清理成本呈指数增长。
2. **防腐层内部可以脏，对外必须干净**：防腐层的使命就是容纳和转化混乱——它的内部是"代价"，它的接口是"价值"。原因：试图让防腐层内部也完美会导致过度设计，增加不必要的复杂度。
3. **单向依赖、不可逆**：内部核心领域绝不直接依赖外部系统，依赖箭头永远指向外。原因：双向依赖是腐化扩散的高速公路，一旦形成极难逆转。
4. **防腐层不是万能药**：如果外部系统和内部模型几乎完全一致，不要建防腐层——过度抽象和过度隔离也是设计腐化。原因：防腐层本身也是代码，需要维护成本，不应为"可能的腐化"而过度防御。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**防腐思维特有关键检查项**：

- [ ] **所有腐化源是否被识别？** 包括概念腐化、结构腐化、行为腐化、协议腐化四类？
- [ ] **扩散风险评估是否具体？** 是否量化了外部变更时内部代码的修改范围？
- [ ] **防腐层边界是否清晰？** 哪些代码属于防腐层、哪些属于核心领域是否明确？
- [ ] **依赖方向是否正确？** 核心领域是否只依赖防腐层接口，不直接依赖外部系统？
- [ ] **防腐层的价值是否被验证？** 替换外部系统时核心代码是否确实可零变更？
- [ ] **是否避免了过度防腐？** 对于设计良好且匹配的外部系统，是否避免了无必要的隔离层？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [contract-thinking](../contract-thinking/SKILL.md) | 互补 | 契约思维定义组件间约定，防腐思维在边界翻译以避免污染 |
| [boundary-thinking](../boundary-thinking/SKILL.md) | 前置 | 边界思维界定系统边界，防腐思维在边界上建隔离层 |
| [separation-of-concerns](../separation-of-concerns/SKILL.md) | 并行 | 关注点分离指导防腐层内部按职责拆解 |
| [single-responsibility-principle](../single-responsibility-principle/SKILL.md) | 后置 | 防腐层内部各翻译器遵循单一职责 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱 |

---

## 参考文献

1. Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley. Chapter 14: Maintaining Model Integrity (Anti-Corruption Layer).
2. Vernon, V. (2013). *Implementing Domain-Driven Design*. Addison-Wesley. Chapter 3: Context Maps.
3. Microsoft Azure Architecture Center. "Anti-Corruption Layer pattern." https://learn.microsoft.com/en-us/azure/architecture/patterns/anti-corruption-layer
4. Fowler, M. (2004). "Anti-Corruption Layer." In *Patterns of Enterprise Application Architecture*. Addison-Wesley.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
