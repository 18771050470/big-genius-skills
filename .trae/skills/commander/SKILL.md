---
name: commander
description: |
  触发：所有任务。
  任何用户输入都必须调用 Commander 进行统一调度和路由。
license: MIT
metadata:
  type: "meta-skill"
  category: "meta"
  layer: "L0"
---

# 总指挥 Skill（Commander）

## 核心定义

任务总指挥，负责分析任务 → 制定策略 → 调度 Skill → 监控执行 → 交付结果的全流程 orchestration。

> 一句话：不是亲自干活，而是决定谁来干、按什么顺序干、怎么验证干好了。

---

## 触发信号

**强制触发**：所有任务都必须调用 Commander 进行统一调度。

> 无论任务简单或复杂，一律先经过 Commander 分析后再决定执行路径。

---

## 执行模式

### 快速路径（轻量模式）

**触发条件**（满足任一即可）：
- 用户明确指定了 Skill
- 任务明确且步骤 ≤ 3
- 纯执行型任务，无需分析

**执行流程**：
```
用户输入 → 识别 Skill → 直接调用 → 输出结果
```

> 快速路径触发条件详见 [references/routing-rules.md](references/routing-rules.md)「快速路径触发」章节

### 标准路径（完整模式）

**触发条件**：
- 任务复杂（步骤 > 3 或涉及多个领域）
- 用户请求不明确，需要分析
- 涉及多个 Skill 协调

**执行流程**：任务解析 → Skill 调度 → 计划制定 → 执行监控 → 结果交付

> 标准路径触发条件及路由决策流程详见 [references/routing-rules.md](references/routing-rules.md)

---

## 核心能力

### 1. 任务解析与复杂度评估 — 分析用户请求，评估任务特征
- **具体表现**：执行意图识别、评估复杂度、识别模糊点、判断是否需要澄清
- **适用场景**：所有任务的起始阶段
- **能力要点**：
  - 解析任务类型（分析型/执行型/混合型）
  - 评估步骤数、涉及领域、风险等级
  - 识别需求模糊点和潜在冲突
  - 按 AGENT_CORE_RULES 规范判断是否需要主动提问
- **参考文件**：[references/routing-rules.md](references/routing-rules.md) 提供意图识别规则和复杂度评估标准

### 2. Skill 需求分析与调度 — 确定所需 Skill 及调用策略
- **具体表现**：列出所需 Skill、确定调用时机、识别依赖关系、处理缺失 Skill
- **适用场景**：任务解析后，执行计划制定前
- **能力要点**：
  - 识别思维模型 Skill 和角色 Skill 的需求
  - 确定 Skill 调用时机（前置/并行/后置）
  - 梳理 Skill 间依赖关系和数据传递路径
  - 制定缺失 Skill 的处理方案（降级/跳过/请求用户）
- **参考文件**：
  - [references/scenario-map.md](references/scenario-map.md) 提供场景类型与技能链的映射关系
  - [references/layer-skills.md](references/layer-skills.md) 提供各层级技能列表与触发条件

### 3. 执行计划制定 — 将任务拆解为可执行的步骤
- **具体表现**：拆解执行步骤、定义输入输出、制定验证标准、预估风险
- **适用场景**：Skill 调度策略确定后
- **能力要点**：
  - 将任务拆解为具体执行步骤
  - 为每步定义输入、预期输出、验证标准
  - 制定失败处理策略（停止/重试/升级）
  - 识别关键里程碑和风险点

### 4. 执行监控与动态调整 — 按计划执行并实时监控
- **具体表现**：调用 Skill、监控结果、处理异常、动态调整计划
- **适用场景**：计划执行阶段
- **能力要点**：
  - 按顺序调用各 Skill，传递正确上下文
  - 监控每步执行结果，验证是否通过
  - 处理执行异常和阻塞
  - 根据实际情况动态调整计划
- **参考文件**：
  - [references/react-loop.md](references/react-loop.md) 提供 ReAct 循环控制机制
  - [references/error-handling.md](references/error-handling.md) 提供异常处理策略和降级方案

### 5. 结果整合与交付 — 整合各步骤产出，形成最终交付物
- **具体表现**：整合产出、验证符合度、识别遗留问题、输出总结
- **适用场景**：所有步骤执行完成后
- **能力要点**：
  - 整合各步骤产出为完整交付物
  - 验证最终交付是否符合原始需求
  - 识别遗留问题和下一步建议
  - 输出执行总结和经验教训

---

## 关键原则

1. **先分析后执行**：不急于动手，先制定完整策略
2. **Skill 组合 > 单一 Skill**：复杂任务需要多视角
3. **动态调整计划**：计划不是一成不变的
4. **验证驱动**：每步必须有明确的验证标准
5. **用户知情权**：重大决策和变更必须告知用户

---

## 自检清单

- [ ] 任务解析准确，复杂度评估合理
- [ ] Skill 选择恰当，组合关系清晰
- [ ] 执行计划具体可执行，每步有验证标准
- [ ] 执行过程中监控到位，异常处理及时
- [ ] 最终交付符合用户原始需求
- [ ] 遗留问题和下一步建议明确

---

## 参考文件

| 文件 | 作用 | 使用场景 |
|------|------|---------|
| [references/routing-rules.md](references/routing-rules.md) | 定义意图识别规则、快速/标准路径触发条件、路由决策流程 | 任务解析阶段，判断走快速路径还是标准路径 |
| [references/scenario-map.md](references/scenario-map.md) | 定义场景类型、关键词特征与技能链的映射关系 | Skill 需求分析阶段，根据场景匹配技能组合 |
| [references/error-handling.md](references/error-handling.md) | 定义各类异常场景的处理策略和降级方案 | 执行监控阶段，处理技能执行失败等异常 |
| [references/react-loop.md](references/react-loop.md) | 定义 ReAct 循环机制、各阶段职责与迭代策略 | 执行监控阶段，控制思考-行动-观察的循环 |
| [references/layer-skills.md](references/layer-skills.md) | 定义各层级的技能列表与触发条件 | Skill 需求分析阶段，了解可用技能及其层级关系 |

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
