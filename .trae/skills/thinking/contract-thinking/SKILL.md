---
name: contract-thinking
description: |
  触发：当设计API/接口/服务间通信时、需要明确组件间的权利和义务、防止因假设不一致导致的集成故障时调用；常见信号包括"这个接口谁负责保证数据格式"、"调用方和服务方各自的职责是什么"、"集成时怎么避免互相甩锅"、"是否可以信任上游传进来的数据"。
  不触发：当接口双方属于同一团队且沟通频繁无需形式化契约时；当接口极其简单（如纯查询、无副作用）且约定已经足够清晰时；当敏捷迭代速度优先、暂时可接受契约不完善时。
  Invoke when designing APIs/interfaces/service communications, needing to clarify component rights and obligations, or preventing integration failures from inconsistent assumptions.
  Do NOT invoke when both sides belong to the same team with frequent communication, when the interface is extremely simple with sufficiently clear conventions, or when sprint velocity takes priority.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["anti-corrosion-thinking", "boundary-thinking", "fail-fast", "defensive-programming", "single-responsibility-principle"]
---

# 契约思维（Contract Thinking）

## 核心定义

在组件交互前明确定义双方的权利（可以期望什么）和义务（必须提供什么）——前置条件、后置条件、不变式——将隐含假设转化为显式契约，从根本上消除"我以为你会..."式Bug。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充接口双方的使用场景和期望行为
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告契约矛盾（如前置条件对调用方要求过高），等待决策
- **提前终止**：若接口足够简单且双方有共同认知（如团队内部纯查询接口），可提前终止并标注"轻量契约即可"

---

## 思考流程

### Step 1: 识别需要契约的交互边界

- 列出所有系统组件间的交互点：模块间调用、服务间RPC/REST调用、数据库访问、消息队列、回调函数
- 区分内部契约（同团队模块间）和外部契约（跨团队、对外API）
- 评估当前每个交互点的假设显式化程度：哪些行为依赖"默认大家都懂"？
- 优先级排序：跨团队 > 对外API > 模块间 > 函数间

---

### Step 2: 定义前置条件（Preconditions）

- 调用方在调用前必须保证什么？
- 哪些输入值是被允许的？哪些是明确不允许的？
- 系统状态在调用前必须满足什么？（如"必须先完成认证"）
- 前置条件越弱（要求越低），接口越易用——平衡严格性和易用性
- 核心原则：如果调用方不满足前置条件，服务方没有义务提供任何保证

---

### Step 3: 定义后置条件（Postconditions）

- 服务方在调用成功后保证什么？
- 返回值的数据结构和值的约束（非null、非空、范围）
- 系统状态变更的保证（幂等性、一致性级别、持久化保证）
- 副作用清单：哪些状态被修改了？有没有发送消息/事件？
- 后置条件是服务方的承诺——必须能够被测试验证

---

### Step 4: 定义不变式（Invariants）

- 在整个组件生命周期中，哪些条件必须始终为真？
- 类的实例一旦创建完成，哪些属性不可变？
- 数据库的哪些约束永远不能被违反？
- 不变式是契约的最强保证——不管发生什么，这些条件必须成立
- 通常在构造函数/初始化时建立不变式，所有公开方法都维护它

---

### Step 5: 定义错误契约

- 什么情况下调用会失败？每种失败会得到什么？
- 异常的语义：网络超时 ≠ 业务拒绝 ≠ 系统故障
- 重试语义：哪些操作可以安全重试（幂等的）？哪些不行？
- SLA契约：响应时间上限（P99 < 200ms）、可用性承诺（99.9%）、限流上限
- 降级契约：服务不可用时的默认行为（返回缓存、返回默认值、返回错误）

---

### Step 6: 验证和实施契约

- 编写契约测试（Contract Test）：验证服务方是否履行后置条件
- 输入边界测试：用前置条件的边界值验证调用方是否被正确校验
- 在代码中使契约显式化：类型系统（TypeScript/Rust的强类型）、断言（assert/guard）、运行时校验
- 契约文档化：OpenAPI/Swagger、Protobuf IDL、代码注释中的@pre/@post标记
- 契约变更管理：修改契约时通知所有依赖方，设定过渡期

---

### Step 7: 总结输出

- 整合分析结果
- 输出每个关键接口的前置条件、后置条件、不变式、错误契约
- 明确契约的验证策略和变更管理流程
- 输出应包含：结论 + 契约清单 + 验证方案 + 变更策略 + 关键假设 + 风险

---

## 关键原则

1. **契约必须是显式的**：任何"默认大家都懂"的假设都是潜在Bug。原因：隐含假设在团队人员变动、时间推移后必然丢失，导致集成故障。
2. **前置条件应由调用方负责（或由服务方防御性校验）**：谁违约谁负责。原因：如果服务方不校验前置条件，调用方的错误会渗透到服务方内部导致隐蔽故障——遵循fail-fast原则。
3. **后置条件是可测试的承诺**：每个后置条件必须能写自动化测试验证。原因：无法验证的承诺不是契约，是愿望。
4. **契约变更需要版本化**：修改契约 = 发布新版本 = 通知消费者。原因：消费者依赖旧契约运行，静默变更契约是线上故障的第一大来源。
5. **小心"契约膨胀"**：不要为了完美而定义过细的契约。原因：契约也是代码，也需要维护——契约的粒度应与交互的稳定性匹配：对外API契约最严格，内部工具函数最宽松。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**契约思维特有关键检查项**：

- [ ] **前置条件是否明确？** 调用方必须保证什么？不满足时会发生什么？
- [ ] **后置条件是否可测试？** 每个承诺是否能写自动化测试验证？
- [ ] **不变式是否贯穿整个生命周期？** 是否有状态变更可能破坏不变式？
- [ ] **错误语义是否区分清楚？** 网络故障、业务拒绝、系统Bug是否有不同的契约约定？
- [ ] **契约变更是否有通知机制？** 变更后依赖方如何感知？
- [ ] **契约的粒度是否合适？** 对外API严格 vs 内部函数宽松的权衡是否合理？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [anti-corrosion-thinking](../anti-corrosion-thinking/SKILL.md) | 互补 | 防腐思维翻译不兼容的契约，契约思维先定义清晰的契约 |
| [fail-fast](../fail-fast/SKILL.md) | 后置 | 契约违反时应快速失败暴露问题，而非静默容忍 |
| [defensive-programming](../defensive-programming/SKILL.md) | 互补 | 防御式编程在接收端校验违的前置条件，契约思维在任何情况下都需要校验违补契约 |
| [boundary-thinking](../boundary-thinking/SKILL.md) | 前置 | 边界思维确定在哪建立契约，契约思维确定契约内容 |
| [single-responsibility-principle](../single-responsibility-principle/SKILL.md) | 并行 | 单一职责确保每个组件只承担一份契约 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱 |

---

## 参考文献

1. Meyer, B. (1997). *Object-Oriented Software Construction* (2nd ed.). Prentice Hall. Chapters 11-12: Design by Contract.
2. Meyer, B. (1992). "Applying 'Design by Contract'." *IEEE Computer*, 25(10), 40-51.
3. Mitchell, R., & McKim, J. (2002). *Design by Contract, by Example*. Addison-Wesley.
4. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley. Item 49: Check parameters for validity.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
