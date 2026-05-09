---
name: margin-of-safety
description: |
  触发：当面临不确定性、需要防范极端风险、设计容错机制时调用；常见信号包括"如果最坏情况发生怎么办"、"系统能承受多大冲击"、"需要留多少余量"。
  不触发：当风险完全可控、无不确定性时；当只需最优解、无需考虑容错时；当安全边际的成本远超潜在收益时。
  Invoke when facing uncertainty, needing to guard against extreme risks, or designing fault tolerance mechanisms.
  Do NOT invoke when risks are completely controllable without uncertainty, when only optimal solutions are needed without considering fault tolerance, or when the cost of safety margin far exceeds potential benefits.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["probabilistic-thinking", "redundancy-thinking", "boundary-thinking", "inverse-thinking"]
---

# 安全边际（Margin of Safety）

## 核心定义

在预期最坏情况的基础上，额外增加缓冲余量，确保即使估计错误或遭遇极端冲击，系统仍能存活。核心公式：安全边际 = 实际容量 / 预期最大负载 - 1。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统容量、预期负载和可接受风险水平
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已确定合理的安全边际且实施方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 评估预期最坏情况

- 列出所有可能的风险场景
- 量化每个风险场景的影响程度和发生概率
- 确定"合理最坏情况"（不是极端黑天鹅，而是有合理概率发生的 worst case）
- 使用历史数据或行业基准校准估计

---

### Step 2: 计算基础容量

- 系统在当前配置下的最大承载能力是多少？
- 容量的定义：吞吐量、并发数、资金储备、时间余量等
- 标注容量的测量方法和不确定性
- 区分理论容量和实际可用容量（通常实际 < 理论）

---

### Step 3: 确定安全边际系数

- 根据风险容忍度选择安全边际系数：
  - 低风险容忍（生命安全相关）：3-5倍
  - 中风险容忍（财务相关）：2-3倍
  - 高风险容忍（可快速迭代的产品）：1.5-2倍
- 考虑估计的不确定性：估计越不确定，安全边际越大
- 参考行业标准和历史教训

---

### Step 4: 设计缓冲机制

- 容量缓冲：预留额外资源（服务器、资金、时间）
- 时间缓冲：在截止日期前设置内部截止日
- 财务缓冲：保持现金储备或信用额度
- 技术缓冲：降级方案、熔断机制、回滚能力
- 评估缓冲成本 vs 风险损失的期望值

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **安全边际不是浪费**：冗余是保险，不是低效。原因：一次极端事件的损失可能超过多年冗余成本。
2. **边际大小取决于不确定性**：估计越不准，边际越大。原因：安全边际的核心是补偿估计误差。
3. **边际会随时间消耗**：安全边际不是一次性设置就永久有效。原因：负载增长、技术债务、环境变化都会消耗边际。
4. **边际不能替代根本修复**：安全边际是临时保护，不是长期方案。原因：持续依赖边际会掩盖系统性问题。

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
- [ ] "合理最坏情况"是否基于数据而非臆想？
- [ ] 容量测量是否区分了理论和实际？
- [ ] 安全边际系数是否有明确依据？
- [ ] 缓冲成本是否被量化并与风险损失对比？
- [ ] 是否考虑了边际随时间的消耗？
- [ ] 输出具体可执行，不含模糊建议（如"多留余量"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 前置 | 概率思维量化风险分布，安全边际基于分布确定缓冲大小 |
| [redundancy-thinking](../thinking/redundancy-thinking/SKILL.md) | 并行 | 冗余思维设计备份机制，安全边际确定备份容量 |
| [boundary-thinking](../thinking/boundary-thinking/SKILL.md) | 并行 | 边界思维识别系统极限，安全边际在极限前设置缓冲区 |
| [inverse-thinking](../thinking/inverse-thinking/SKILL.md) | 前置 | 逆向思维识别失败路径，安全边际为失败路径提供缓冲 |

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

1. Graham, B. (1949). *The Intelligent Investor*. Harper & Row. Chapter 20: "Margin of Safety".
2. Taleb, N. N. (2012). *Antifragile: Things That Gain from Disorder*. Random House.
3. Klarman, S. (2004). *Margin of Safety: Risk-Averse Value Investing Strategies for the Thoughtful Investor*. HarperBusiness.
4. Engineering ToolBox. (2024). *Factors of Safety*. https://www.engineeringtoolbox.com/factors-safety-d_972.html

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
