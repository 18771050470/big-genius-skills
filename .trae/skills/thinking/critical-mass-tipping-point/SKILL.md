---
name: critical-mass-tipping-point
description: |
  触发：当需要评估产品/想法/行为是否接近大规模传播阈值、分析社会流行病传播机制、设计增长策略时调用；常见信号包括"什么时候能爆发？"、"为什么一直不温不火？"、"如何引爆传播？"、"用户增长停滞"。
  不触发：当系统完全是线性增长且无网络效应时；当只需分析个体行为、无需群体传播时；当问题与传播/扩散无关时。
  Invoke when evaluating whether a product/idea/behavior is approaching a mass传播 threshold, analyzing social epidemic mechanisms, or designing growth strategies.
  Do NOT invoke when growth is purely linear with no network effects, when only individual behavior is analyzed, or when the problem is unrelated to传播/diffusion.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["network-effects", "viral-growth", "diffusion-of-innovations", "feedback-loops"]
---

# 临界点与引爆点思维（Critical Mass / Tipping Point Thinking）

## 核心定义

系统量变积累到特定阈值后发生质变，小投入在临界点后引发大规模连锁反应——理解传播的三要素（个别人物法则、附着力因素、环境威力）是引爆流行的关键。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充当前用户基数、传播数据和社会网络结构
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确系统远离临界点或已过临界点且方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 评估当前系统状态

- 当前用户/采纳者数量是多少？
- 增长率是加速、线性还是减速？
- 系统是否显示出正反馈迹象？（用户带来用户）
- 与潜在总市场相比，当前渗透率是多少？

---

### Step 2: 识别临界点阈值

- 理论临界点：基于网络效应的数学模型（如 Metcalfe 定律）
- 历史类比：类似产品/想法的临界点是多少？
- 实证观察：用户增长曲线是否出现拐点？
- 关键假设：达到什么条件后增长会自我维持？

---

### Step 3: 分析传播三要素

- **个别人物法则（Law of the Few）**：
  - 联络员（Connectors）：谁拥有最大的社交网络？
  - 内行（Mavens）：谁是信息专家？
  - 推销员（Salesmen）：谁有说服力？
- **附着力因素（Stickiness）**：
  - 信息/产品本身是否有记忆点？
  - 是否容易被理解和传播？
- **环境威力（Power of Context）**：
  - 外部环境是否支持传播？
  - 群体规模是否达到 150 人（邓巴数）的社交边界？

---

### Step 4: 设计引爆策略

- 集中资源突破临界点，而非均匀分散
- 识别并激活关键节点（联络员、内行、推销员）
- 提升产品/信息的附着力（简化、具象、情感化）
- 创造有利于传播的环境（时机、场景、社会压力）

---

### Step 5: 监控与调整

- 设定关键指标：病毒系数（K-factor）、传播周期、留存率
- 监控是否接近临界点：增长率是否加速？
- 若未达预期：分析是哪个传播要素薄弱？
- 若已过临界点：准备基础设施应对爆发式增长

---

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **临界点前后是两种系统**：临界点前的增长依赖外部推动，临界点后的增长自我维持。原因：网络效应在临界点后产生正反馈，每新增一个用户都使产品对所有用户更有价值。
2. **资源应集中而非分散**：在达到临界点之前，将资源集中在最小可行市场。原因：均匀分散资源无法在任何单一市场达到临界质量，集中投入才能突破阈值。
3. **三要素缺一不可**：个别人物、附着力、环境威力必须同时满足。原因：缺少任何一环，传播链条都会断裂——有传播者但产品无附着力，或有附着力但无传播者。
4. **临界点是动态变化的**：市场环境、竞争态势、用户预期会改变临界点位置。原因：今天有效的引爆策略明天可能失效，需要持续监控和调整。

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
- [ ] **临界点特供**：是否评估了当前系统状态？用户基数、增长率、渗透率是否被量化？
- [ ] **临界点特供**：是否识别了临界点阈值？是否基于网络效应模型或历史类比进行估算？
- [ ] **临界点特供**：是否分析了三要素？个别人物（联络员/内行/推销员）、附着力、环境威力是否被逐一评估？
- [ ] **临界点特供**：是否设计了集中突破策略？资源是否被聚焦于最小可行市场而非均匀分散？
- [ ] **临界点特供**：是否设定了关键监控指标？病毒系数（K-factor）、传播周期、留存率是否被定义？
- [ ] **临界点特供**：是否评估了临界点的动态性？市场环境变化是否被考虑？是否准备了应对爆发式增长的方案？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"加大推广"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [network-effects](../network-effects/SKILL.md) | 前置 | 网络效应解释为何临界点后增长自我维持 |
| [viral-growth](../viral-growth/SKILL.md) | 并行 | 病毒式增长提供量化传播指标（K-factor） |
| [diffusion-of-innovations](../diffusion-of-innovations/SKILL.md) | 前置 | 创新扩散理论解释不同采纳者群体的角色 |
| [feedback-loops](../feedback-loops/SKILL.md) | 前置 | 正反馈回路是临界点突破后的增长引擎 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | 传播理论、网络效应数学模型 |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Gladwell, M. (2000). *The Tipping Point: How Little Things Can Make a Big Difference*. Little, Brown and Company.
2. Rogers, E. M. (2003). *Diffusion of Innovations* (5th ed.). Free Press.
3. Schelling, T. C. (1978). *Micromotives and Macrobehavior*. W. W. Norton & Company.
4. Granovetter, M. (1978). Threshold models of collective behavior. *American Journal of Sociology*, 83(6), 1420-1443.
5. Dunbar, R. I. M. (1992). Neocortex size as a constraint on group size in primates. *Journal of Human Evolution*, 22(6), 469-493.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
