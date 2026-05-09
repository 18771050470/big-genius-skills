---
name: boundary-thinking
description: |
  触发：当设计输入验证、处理边界情况、评估资源限制、设计错误处理时调用；常见信号包括"边界情况"、"极端输入"、"资源上限"、"并发限制"、"空值处理"。
  不触发：当仅需正常流程设计、不涉及边界/异常处理、不需要评估系统极限时，不要调用此 Skill。
  Invoke when designing input validation, handling edge cases, evaluating resource limits, or designing error handling.
  Do NOT invoke when only normal flow design is needed, or when no boundary/exception handling is required.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["inverse-thinking", "boundary-thinking", "defensive-programming"]
---

# 边界思维

## 核心定义

主动识别和处理边界情况、异常输入和资源限制，提升系统鲁棒性。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充边界信息（如最大并发、数据量级、超时要求）
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点
- **提前终止**：若某步已识别全部关键边界且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别输入边界

- 要点1：列出所有输入参数的有效范围（最小值、最大值、空值、null、特殊字符）
- 要点2：识别异常输入类型（超长字符串、负数、非法格式、注入攻击）
- 要点3：考虑并发场景下的输入竞争条件

---

### Step 2: 识别资源边界

- 要点1：评估系统资源限制（内存、CPU、磁盘、网络带宽）
- 要点2：识别资源耗尽场景（内存泄漏、连接池耗尽、磁盘满）
- 要点3：评估资源增长的临界点（何时需要扩容或降级）

---

### Step 3: 识别时间边界

- 要点1：评估超时场景（网络超时、数据库超时、第三方API超时）
- 要点2：识别时序问题（竞态条件、乱序消息、时钟漂移）
- 要点3：考虑延迟对用户体验的影响（响应时间阈值）

---

### Step 4: 设计边界防护

- 要点1：为每个边界场景设计防护策略（验证、限流、降级、熔断）
- 要点2：确保边界处理不阻塞正常流程（快速失败、优雅降级）
- 要点3：建立边界监控和告警机制

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步

---

## 关键原则

1. **正常流程只占20%，边界处理占80%**：说明。原因：系统崩溃通常发生在边界情况，而非正常流程。
2. **快速失败优于静默错误**：说明。原因：静默错误累积后爆发更难排查，快速失败立即暴露问题。
3. **边界是动态的**：说明。原因：随着用户增长和数据积累，边界条件会变化，需要定期重新评估。

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
- [ ] **边界思维特供**：是否识别了所有输入参数的边界？最小值、最大值、空值、null、特殊字符、超长输入是否被覆盖？
- [ ] **边界思维特供**：是否评估了资源边界？内存、CPU、磁盘、网络带宽的极限是否被量化？资源耗尽的临界点是否被识别？
- [ ] **边界思维特供**：是否评估了时间边界？超时场景、竞态条件、时钟漂移、时区转换是否被考虑？
- [ ] **边界思维特供**：是否为每个边界场景设计了具体防护策略？验证、限流、降级、熔断措施是否可执行？
- [ ] **边界思维特供**：边界处理是否遵循"快速失败"原则？静默错误是否被消除？边界监控和告警机制是否被建立？
- [ ] **边界思维特供**：是否考虑了并发场景下的边界竞争条件？多线程/分布式环境下的边界问题是否被单独评估？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [inverse-thinking](../thinking/inverse-thinking/SKILL.md) | 前置 | 从失败路径识别边界 |
| [defensive-programming](../thinking/defensive-programming/SKILL.md) | 后置 | 实现边界防护代码 |
| [redundancy-thinking](../thinking/redundancy-thinking/SKILL.md) | 并行 | 关键边界设计冗余 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Myers, G. J., Sandler, C., & Badgett, T. (2011). *The Art of Software Testing* (3rd ed.). Wiley.
2. Nygard, M. T. (2018). *Release It!: Design and Deploy Production-Ready Software* (2nd ed.). Pragmatic Bookshelf.
3. Google SRE Team. (2016). *Site Reliability Engineering: How Google Runs Production Systems*. O'Reilly Media.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
