---
name: critical-mass
description: |
  触发：当需要判断一个趋势是否即将爆发、评估产品/想法/行为何时从缓慢增长转向指数增长、分析网络效应的启动条件时调用；常见信号包括"什么时候能火"、"用户增长停滞后突然爆发"、"病毒式传播临界点"、"市场渗透率超过X%后变化"。
  不触发：当增长是纯线性且无加速迹象时；当系统不存在网络效应或正反馈时；当只需预测短期（<3个月）趋势、临界点效应尚未显现时。
  Invoke when judging whether a trend is about to explode, evaluating when a product/idea/behavior shifts from slow to exponential growth, or analyzing network effect activation conditions.
  Do NOT invoke when growth is purely linear with no acceleration signs, when the system lacks network effects or positive feedback, or when only predicting short-term (<3 months) trends where critical mass effects have not yet emerged.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["feedback-loops", "network-effects", "diffusion-of-innovations", "power-law"]
---

# 临界点思维（Critical Mass / Tipping Point Thinking）

## 核心定义

当系统变量超过特定阈值后，正反馈回路被激活，导致行为/趋势/产品从缓慢线性增长跃迁为指数级爆发。Rogers 1962年提出创新扩散理论，Gladwell 2000年将"临界点"概念普及化——小变化引发大效应的杠杆时刻。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充当前渗透率、用户增长曲线、网络效应强度和竞争环境
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确临界点位置且策略清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别正反馈机制

- 系统中存在哪些正反馈回路？（用户增长→更多内容→更多用户；采用者增加→兼容性提升→更多采用者）
- 网络效应类型：直接网络效应（用户间互动，如微信）还是间接网络效应（互补品增加，如iOS应用生态）？
- 正反馈强度：每增加一个用户，对其他用户的价值提升多少？
- 是否存在跨边网络效应？（平台连接供需双方，如Uber）

### Step 2: 估算临界点阈值

- 历史类比：类似产品/趋势的临界点出现在多少渗透率？（通常10-25%，Rogers扩散曲线）
- 数学模型： Bass扩散模型中的创新系数和模仿系数
- 网络密度：达到什么密度后信息/行为能自发传播？
- 社会证明：需要多少"早期采用者"才能触发"早期多数"的跟随？

### Step 3: 评估当前状态与临界点的距离

- 当前渗透率 vs 临界点阈值：差距多大？
- 增长速度：是加速还是减速？二阶导数为正还是负？
- 催化剂：什么事件可能加速达到临界点？（KOL背书、媒体报道、政策变化）
- 阻碍因素：什么可能阻止达到临界点？（替代品、负面事件、基础设施不足）

### Step 4: 设计跨越临界点的策略

- 降低临界点：通过产品简化、价格补贴、邀请奖励降低用户采纳门槛
- 集中资源：在特定细分市场（ beachhead market）先达到局部临界点，再扩展
- 制造催化剂：策划病毒式传播事件、KOL合作、媒体曝光
- 维持增长惯性：达到临界点后，确保供应链/客服/基础设施能承载指数增长

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **临界点前增长缓慢，临界点后指数爆发**：正反馈回路在阈值前被抑制，超过阈值后被激活。原因：网络效应需要最小用户基数才能自我维持。
2. **10-25%是常见临界点区间**：Rogers创新扩散曲线显示，早期采用者占16%，跨越到早期多数时触发爆发。原因：社会证明需要足够多"同类人"已采纳。
3. **局部临界点先于全局临界点**：在细分市场先达到临界点是常见策略。原因：全局市场太大，资源分散无法达到阈值；局部突破后产生示范效应。
4. **临界点后的基础设施崩溃是最大风险**：指数增长若超出系统承载能力，会导致服务质量下降、用户流失。原因：正反馈既能放大成功也能放大失败。

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
- [ ] 正反馈机制是否被识别？网络效应类型是否被分类？
- [ ] 临界点阈值是否被估算（含依据）？
- [ ] 当前状态与临界点的距离是否被评估？
- [ ] 是否设计了跨越临界点的具体策略？
- [ ] 是否考虑了临界点后的承载能力风险？
- [ ] 输出具体可执行，不含模糊建议（如"加大推广"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [feedback-loops](../thinking/feedback-loops/SKILL.md) | 前置 | 临界点是正反馈回路从抑制到激活的阈值 |
| [network-effects](../thinking/network-effects/SKILL.md) | 并行 | 网络效应是临界点最常见的驱动力 |
| [diffusion-of-innovations](../thinking/diffusion-of-innovations/SKILL.md) | 前置 | 创新扩散理论提供临界点的理论框架 |
| [power-law](../thinking/power-law/SKILL.md) | 并行 | 幂律分布描述临界点后的赢家通吃格局 |

---

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | Bass扩散模型、网络效应理论、Rogers创新扩散 |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Rogers, E. M. (1962). *Diffusion of Innovations* (1st ed.). Free Press.
2. Gladwell, M. (2000). *The Tipping Point: How Little Things Can Make a Big Difference*. Little, Brown and Company.
3. Bass, F. M. (1969). A new product growth for model consumer durables. *Management Science*, 15(5), 215-227.
4. Schelling, T. C. (1971). Dynamic models of segregation. *Journal of Mathematical Sociology*, 1(2), 143-186.
5. Katz, M. L., & Shapiro, C. (1985). Network externalities, competition, and compatibility. *American Economic Review*, 75(3), 424-440.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
