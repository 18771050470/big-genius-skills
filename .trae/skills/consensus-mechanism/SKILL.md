---
name: consensus-mechanism
description: |
  触发：当设计分布式系统的一致性协议、选择区块链共识算法、评估网络容错能力或解决分布式状态同步问题时；常见信号包括"共识算法"、"一致性"、"PoW"、"PoS"、"BFT"、"最终性"。
  不触发：当系统是中心化架构、当强一致性非必需、当CAP定理约束下可用性优先时。
  Invoke when designing distributed consensus protocols, selecting blockchain algorithms, evaluating network fault tolerance, or solving distributed state synchronization.
  Do NOT invoke when the system is centralized, when strong consistency is unnecessary, or when availability is prioritized under CAP constraints.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L3"
  related: ["distributed-trust", "byzantine-fault-tolerance", "game-theory-thinking", "trade-off-thinking"]
---

# 共识机制思维 (Consensus Mechanism)

## 核心定义

分布式系统中使多个节点就某一状态或值达成一致的协议和算法，解决去中心化环境下的"拜占庭将军问题"，确保系统在部分节点故障或作恶时仍能保持一致性和可用性。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充网络规模、节点性质或性能要求
- **发现矛盾**：当安全性与活性需求冲突时，标记并寻求CAP权衡方案
- **提前终止**：当已选择合适共识机制或确认需要定制设计时

---

## 思考流程

### Step 1: 系统需求分析

- **节点规模**：少量节点（<100）vs 大规模网络（>1000）
- **节点性质**：许可网络（已知身份）vs 无许可网络（开放参与）
- **故障模型**：崩溃故障 vs 拜占庭故障
- **性能需求**：吞吐量（TPS）、延迟（确认时间）、最终性
- **能源约束**：是否介意高能耗

---

### Step 2: 共识机制分类与选择

- **中本聪共识（Nakamoto Consensus）**：
  - PoW（工作量证明）：算力竞争，高能耗，开放网络
  - PoS（权益证明）：质押竞争，低能耗，资本密集
  - 特点：概率性最终性，最长链规则
- **BFT类共识**：
  - PBFT：实用拜占庭容错，确定性最终性
  - HotStuff：流水线BFT，高吞吐量
  - Tendermint：BFT+PoS混合
  - 特点：即时最终性，许可网络
- **混合共识**：
  - PoW+PoS：结合两者优势
  - DAG+共识：异步结构提升吞吐量

---

### Step 3: 安全性分析

- **容错阈值**：
  - BFT：最多容忍1/3拜占庭节点
  - PoW：51%攻击阈值
  - PoS：通常2/3质押诚实
- **攻击向量**：
  - 双花攻击
  - 审查攻击
  - 长程攻击（PoS特有）
  - 自私挖矿
- **经济安全**：攻击成本 vs 攻击收益

---

### Step 4: 活性与最终性分析

- **活性（Liveness）**：系统持续产出新块/达成共识的能力
  - 网络分区容忍
  - 交易确认时间
- **最终性（Finality）**：交易一旦被确认就不可回滚
  - 概率性最终性（中本聪共识）
  - 确定性最终性（BFT共识）
- **CAP权衡**：一致性、可用性、分区容忍性的平衡

---

### Step 5: 激励与治理设计

- **出块奖励**：激励诚实参与
- **惩罚机制**：
  - PoW：沉没成本（电力、硬件）
  - PoS：罚没（Slashing）
- **治理机制**：
  - 链上治理（代币投票）
  - 链下治理（核心开发者）
  - 混合治理

---

### Step 6: 性能优化与扩展

- **分片（Sharding）**：水平扩展提升吞吐量
- **Layer 2**：链下处理，链上结算
- **共识优化**：
  - 流水线设计
  - 并行共识
  - 轻节点验证
- 输出应包含：机制选择 + 安全分析 + 性能评估 + 优化建议

---

## 关键原则

1. **容错优先**：共识机制必须容忍预期的故障比例。原因：分布式系统必然面临节点故障，无容错机制的系统无法在实际网络中运行。

2. **经济安全**：使攻击成本超过潜在收益。原因：密码学安全是基础，但经济激励是防止理性攻击者的关键。

3. **CAP权衡**：根据应用场景选择一致性、可用性、分区容忍性的平衡。原因：CAP定理证明三者不可兼得，必须针对性优化。

4. **渐进最终性**：理解概率性最终性与确定性最终性的区别。原因：不同业务场景对最终性的要求不同，选择需匹配需求。

5. **去中心化程度**：在性能和安全之间找到合适的去中心化程度。原因：完全去中心化往往性能低下，需要权衡。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**共识机制特有关键检查项**：

- [ ] **容错阈值是否满足需求？** 能容忍多少比例的故障节点？
- [ ] **攻击成本是否超过收益？** 经济安全是否成立？
- [ ] **CAP权衡是否与场景匹配？** 一致性优先还是可用性优先？
- [ ] **最终性类型是否符合业务需求？** 概率性还是确定性？
- [ ] **激励机制是否相容？** 诚实行为是否是最优策略？
- [ ] **性能是否满足应用需求？** 吞吐量、延迟是否可接受？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [distributed-trust](../thinking/distributed-trust/SKILL.md) | 基础 | 理解共识机制在分布式信任中的作用 |
| [byzantine-fault-tolerance](../thinking/byzantine-fault-tolerance/SKILL.md) | 基础 | 理解拜占庭容错的理论基础 |
| [game-theory-thinking](../thinking/game-theory-thinking/SKILL.md) | 并行 | 设计激励相容的共识机制 |
| [trade-off-thinking](../thinking/trade-off-thinking/SKILL.md) | 并行 | 在安全性、活性、去中心化之间权衡 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Castro, M., & Liskov, B. (1999). Practical Byzantine Fault Tolerance. *Proceedings of the Third Symposium on Operating Systems Design and Implementation*, 173-186.
2. Yin, M., Malkhi, D., Reiter, M. K., Gueta, G. G., & Abraham, I. (2019). HotStuff: BFT Consensus in the Lens of Blockchain. *arXiv preprint arXiv:1803.05069*.
3. Buchman, E., Kwon, J., & Milosevic, Z. (2018). The Latest Gossip on BFT Consensus. *arXiv preprint arXiv:1807.04938*.
4. Eyal, I., Gencer, A. E., Sirer, E. G., & Van Renesse, R. (2016). Bitcoin-NG: A Scalable Blockchain Protocol. *13th USENIX Symposium on Networked Systems Design and Implementation*, 45-59.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
