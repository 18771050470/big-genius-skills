---
name: redundancy-thinking
description: |
  触发：当需要设计高可用系统、构建容错架构、消除单点故障（SPOF）、为关键路径引入备份机制时调用；常见信号包括"这个服务挂了怎么办"、"有没有单点故障"、"如何保证99.99%可用性"、"关键数据会不会丢"。
  不触发：当系统可用性要求极低、故障影响可忽略时；当简单方案已充分满足可靠性需求时；当引入冗余带来的复杂性远超其价值时；当处理的是纯计算逻辑优化而非系统韧性设计时。
  Invoke when designing high-availability systems, building fault-tolerant architectures, eliminating single points of failure (SPOF), or introducing backup mechanisms for critical paths.
  Do NOT invoke when system availability requirements are extremely low, when simple solutions adequately meet reliability needs, when redundancy complexity far outweighs its value, or when dealing with pure computational optimization rather than system resilience design.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["antifragility", "system-thinking", "boundary-thinking", "precautionary-principle", "margin-of-safety"]
---

# 冗余思维（Redundancy Thinking）

## 核心定义

在关键路径上有意引入重复组件或功能，用合理的"浪费"换取系统在部分故障时仍能正常运行的韧性——不做最强，做打不死的。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统架构和故障场景信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点（如"冗余本身成了故障源"），等待决策
- **提前终止**：若评估后确认系统可靠性需求不高且无关键路径需要保护，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别关键路径和单一故障点

- 梳理系统完整的数据流和控制流
- 标记所有"一旦失效则系统整体瘫痪"的单一故障点（SPOF）
- 区分关键路径（必须保护）和次要路径（可降级）
- 评估每个故障点的失效概率和失效后果
- 警惕"隐藏的SPOF"：共享电源、共享网络、共享DNS、同一云厂商可用区

---

### Step 2: 确定冗余层级和类型

- 硬件冗余：双电源、RAID磁盘阵列、双网卡、多服务器
- 软件冗余：多实例部署、服务降级、断路器模式
- 数据冗余：主从复制、异地多活、WAL日志、快照备份
- 时间冗余：重试机制、幂等设计、超时后回退
- 信息冗余：校验和、纠错码（ECC）、奇偶校验
- 人为冗余：值班轮换、知识备份（避免单点知识持有者）
- 根据失效后果选择冗余深度：N+1（容忍1个故障）还是N+2（容忍2个故障）

---

### Step 3: 选择冗余架构模式

- 主动-主动（Active-Active）：所有节点同时服务，故障时负载重新分配。优势：资源利用率高、故障切换无延迟。代价：数据一致性复杂。
- 主动-被动（Active-Passive）：主节点服务，备节点待命。优势：数据一致性简单。代价：资源浪费、切换有延迟。
- N+1 冗余：N个节点满足需求 + 1个热备。适用于同质化服务。
- 2N 冗余：完全双份。适用于极端关键系统（航空、核电、医疗生命支持）。
- 降级模式（Graceful Degradation）：非关键功能故障后系统继续运行核心功能。
- 评估每种模式对一致性、延迟、吞吐量、运维复杂度的代价

---

### Step 4: 评估冗余引入的新风险

- 冗余组件本身会不会成为新的故障源？（"冗余切换逻辑"本身可能故障）
- 是否存在共因故障（Common Cause Failure）？——所有冗余节点被同一原因同时击穿（同一机房断电、同一软件Bug）
- 冗余间同步机制是否可靠？脑裂（Split-Brain）风险怎么处理？
- 冗余增加的系统复杂度是否超过了可靠性收益？
- 谨记NASA教训：盲目加冗余有时反而降低可靠性（冗余管理逻辑的故障率 > 被保护组件的故障率）

---

### Step 5: 设计故障检测与切换机制

- 故障如何被检测？心跳（Heartbeat）、外部监控（External Watchdog）、超时探测
- 检测到故障后多久触发切换？（MTTD：平均检测时间 vs MTTR：平均恢复时间）
- 切换是自动还是人工？自动切换的误判风险？
- 切换后如何确保数据一致性？是否有数据丢失窗口？
- 故障恢复后如何回切？是否需要人工确认？
- 混沌工程测试：定期主动注入故障验证冗余机制是否真的有效

---

### Step 6: 计算冗余的成本收益

- 冗余成本 = 硬件/软件/运维额外支出 + 复杂度带来的认知负荷 + 潜在的系统性能损失
- 冗余收益 = 故障损失期望值减少 = (故障概率 × 故障损失) / (1 + 冗余防护层数)
- 判断冗余是否"值得"：如果冗余自身增加的故障概率 > 所消除的故障概率，则不引入
- 考虑"冗余应该加在哪里"：加在最脆弱的环节（木桶最短的那块板），而非到处撒胡椒面

---

### Step 7: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 标注哪些SPOF已被消除，哪些仍存在及其容忍理由
- 明确冗余架构的选择理由和替代方案的排除原因
- 输出应包含：结论 + 建议 + 关键假设 + 遗留风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **冗余服务于韧性而非完美**：冗余不能消除故障，只能降低故障影响。原因：任何组件最终都会故障，冗余让你在故障发生时活下来，而不是不故障。
2. **冗余自身也会故障**：冗余机制（切换逻辑、监控、同步）本身就是新的故障源。原因：NASA可靠性工程研究发现，过度冗余可能导致系统可靠性不升反降——冗余管理逻辑的复杂度可能引入更多Bug。
3. **共因故障是冗余的死穴**：如果所有冗余节点共享同一个脆弱性（同一软件版本、同一机房、同一供应商），冗余形同虚设。原因：Titanic的水密舱壁就是冗余设计失败的经典案例——相邻舱壁不够高，一次撞击击穿多个。
4. **成本收益驱动决策**：冗余不是越多越好，必须在可用性收益和引入的复杂度之间权衡。原因：每个9的可用性提升都对应指数级增长的成本（99% → 99.9% → 99.99% → 99.999%），应用层冗余往往比硬件冗余性价比更高。
5. **测试冗余机制，不假设它有效**：未经测试的冗余不是真正的冗余。原因：大量生产故障的根因是"以为切换会生效，实际切换脚本从没跑过"。

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
- [ ] 所有SPOF是否被识别？包括隐性的共享依赖（DNS、电源、云可用区）？
- [ ] 冗余架构模式是否根据场景合理选择？是否考虑了Active-Active vs Active-Passive的代价？
- [ ] 共因故障风险是否被评估？冗余节点是否有共享的脆弱性？
- [ ] 冗余自身引入的新故障源是否被识别？
- [ ] 故障检测和切换机制是否被设计？MTTD和MTTR是否被估算？
- [ ] 成本收益是否量化？冗余复杂度是否超过了可靠性收益？
- [ ] 输出具体可执行，不含模糊建议（如"加冗余"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [antifragility](../antifragility/SKILL.md) | 互补 | 冗余提供韧性底线（不坏），反脆弱实现从此类冲击中成长（变强） |
| [system-thinking](../systems-thinking/SKILL.md) | 前置 | 系统思维识别整体依赖和反馈，冗余思维在关键点引入备份 |
| [boundary-thinking](../boundary-thinking/SKILL.md) | 并行 | 边界思维定义故障的边界条件，冗余思维在边界内增加容错 |
| [precautionary-principle](../precautionary-principle/SKILL.md) | 前置 | 预防原则提醒"不确定性不能成为不行动的理由"，触发冗余设计 |
| [margin-of-safety](../margin-of-safety/SKILL.md) | 并行 | 安全边际提供容量缓冲，冗余提供功能备份 |

---

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Shooman, M. L. (2002). *Reliability of Computer Systems and Networks: Fault Tolerance, Analysis, and Design*. Wiley-Interscience.
2. Knight, J. C. (2002). "Safety critical systems: Challenges and directions." *Proceedings of the 24th International Conference on Software Engineering (ICSE)*, 547-550.
3. Avizienis, A., Laprie, J. C., Randell, B., & Landwehr, C. (2004). "Basic concepts and taxonomy of dependable and secure computing." *IEEE Transactions on Dependable and Secure Computing*, 1(1), 11-33.
4. Leveson, N. G. (2011). *Engineering a Safer World: Systems Thinking Applied to Safety*. MIT Press. (Chapter 7: STPA hazard analysis for complex systems)
5. Gray, J. (1986). "Why do computers stop and what can be done about it?" *Tandem Computers Technical Report 85.7*.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
