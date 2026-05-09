---
name: distributed-trust
description: |
  触发：当设计去中心化系统、消除单点信任依赖、建立无需中介的协作机制或评估分布式系统的信任模型时；常见信号包括"去中心化"、"无需信任"、"共识"、"拜占庭容错"、"分布式账本"。
  不触发：当中心化信任更高效、当参与方完全可信、当系统需要高效率低延迟时。
  Invoke when designing decentralized systems, eliminating single-point trust dependencies, establishing trustless collaboration, or evaluating distributed trust models.
  Do NOT invoke when centralized trust is more efficient, when participants are fully trusted, or when high efficiency and low latency are required.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L3"
  related: ["consensus-mechanism", "byzantine-fault-tolerance", "game-theory-thinking", "redundancy-thinking"]
---

# 分布式信任思维 (Distributed Trust)

## 核心定义

通过密码学、共识算法和经济激励机制，在互不信任的节点之间建立可验证的协作信任，消除对单一中心化权威的依赖，实现"无需信任的信任"。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充节点行为假设或安全模型
- **发现矛盾**：当去中心化目标与性能需求冲突时，标记并寻求权衡方案
- **提前终止**：当已找到合适的信任模型或确认分布式信任不适用时

---

## 思考流程

### Step 1: 信任需求分析

- 识别系统中需要信任的核心功能（身份、状态、顺序）
- 分析参与方的信任假设（诚实、理性、恶意）
- 评估中心化信任的风险（单点故障、审查、腐败）
- 确定去中心化的必要性和可行性

---

### Step 2: 威胁模型定义

- **节点故障类型**：
  - 崩溃故障（Crash Fault）：节点停止响应
  - 拜占庭故障（Byzantine Fault）：节点任意作恶
- **攻击向量**：
  - 女巫攻击（Sybil Attack）：单一实体控制多个节点
  - 51%攻击：控制大多数共识权力
  - 长程攻击：从早期历史分叉
- **网络假设**：
  - 同步网络 vs 异步网络
  - 消息延迟边界

---

### Step 3: 信任机制选择

- **密码学信任**：
  - 数字签名验证身份和消息完整性
  - 哈希链保证数据不可篡改
  - 零知识证明保护隐私
- **共识机制**：
  - PoW：算力竞争，适合开放网络
  - PoS：权益质押，能源效率高
  - BFT：投票共识，适合许可网络
- **经济激励**：
  - 诚实行为奖励
  - 恶意行为惩罚（罚没机制）
  - 代币经济学设计

---

### Step 4: 容错能力设计

- 确定系统需要容忍的故障节点比例
- **BFT容错**：最多容忍f个拜占庭节点，需要3f+1个节点
- **Nakamoto容错**：概率性安全，51%攻击阈值
- 设计故障检测和恢复机制
- 评估系统的活性（liveness）和安全性（safety）

---

### Step 5: 激励对齐分析

- 分析各参与方的利益诉求
- 设计激励相容机制（诚实行为是最优策略）
- 评估可能的攻击成本和收益
- 确保攻击成本大于攻击收益
- 考虑长期激励和短期激励的平衡

---

### Step 6: 权衡评估与优化

- **去中心化程度**：完全去中心化 vs 部分中心化
- **性能权衡**：吞吐量、延迟 vs 安全性
- **能源效率**：PoW高能耗 vs PoS低能耗
- **治理机制**：链上治理 vs 链下治理
- 输出应包含：信任模型 + 机制设计 + 安全分析 + 权衡建议

---

## 关键原则

1. **密码学锚定**：用密码学原语作为信任的基础。原因：数学保证比人为信任更可靠，密码学提供可验证的安全性。

2. **经济安全**：使攻击成本超过攻击收益。原因：理性的攻击者不会因亏损而攻击，经济激励约束行为。

3. **容错设计**：假设部分节点会故障或作恶。原因：分布式系统必然面临节点故障，容错设计确保系统鲁棒性。

4. **透明可验证**：所有关键操作必须可独立验证。原因：可验证性是分布式信任的核心，无法验证的信任是盲目的。

5. **渐进去中心化**：根据成熟度逐步增加去中心化程度。原因：完全去中心化开发和治理困难，渐进路径更可行。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**分布式信任特有关键检查项**：

- [ ] **威胁模型是否完整？** 拜占庭故障、女巫攻击都考虑了吗？
- [ ] **容错能力是否满足需求？** f个故障节点需要多少总节点？
- [ ] **激励是否相容？** 诚实行为是否是最优策略？
- [ ] **攻击成本是否超过收益？** 经济安全是否成立？
- [ ] **关键操作是否可独立验证？** 透明度如何保证？
- [ ] **去中心化程度是否与性能需求平衡？**

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [consensus-mechanism](../thinking/consensus-mechanism/SKILL.md) | 并行 | 选择适合的共识算法实现分布式一致性 |
| [byzantine-fault-tolerance](../thinking/byzantine-fault-tolerance/SKILL.md) | 基础 | 理解拜占庭容错的能力和限制 |
| [game-theory-thinking](../thinking/game-theory-thinking/SKILL.md) | 并行 | 设计激励相容的机制 |
| [redundancy-thinking](../thinking/redundancy-thinking/SKILL.md) | 并行 | 通过冗余提升系统容错能力 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Lamport, L., Shostak, R., & Pease, M. (1982). The Byzantine Generals Problem. *ACM Transactions on Programming Languages and Systems*, 4(3), 382-401.
2. Nakamoto, S. (2008). Bitcoin: A Peer-to-Peer Electronic Cash System. *White Paper*.
3. Castro, M., & Liskov, B. (2002). Practical Byzantine Fault Tolerance and Proactive Recovery. *ACM Transactions on Computer Systems*, 20(4), 398-461.
4. Eyal, I., & Sirer, E. G. (2014). Majority Is Not Enough: Bitcoin Mining Is Vulnerable. *Financial Cryptography and Data Security*, 436-454.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
