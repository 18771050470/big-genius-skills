---
name: token-economics
description: |
  触发：当设计区块链项目的经济模型、设计代币激励机制、评估加密资产的可持续性、或分析去中心化协议的激励结构时；常见信号包括"代币经济"、"激励机制"、"通证模型"、"通胀/通缩"、"质押奖励"。
  不触发：当项目无需代币即可运行、当经济模型过于复杂导致用户难以理解、当监管禁止代币发行时。
  Invoke when designing blockchain economic models, token incentive mechanisms, assessing crypto asset sustainability, or analyzing decentralized protocol incentives.
  Do NOT invoke when the project can run without tokens, when economic models are too complex for users, or when regulations prohibit token issuance.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L3"
  related: ["game-theory-thinking", "incentive-thinking", "system-thinking", "feedback-loops"]
---

# 代币经济学思维 (Token Economics)

## 核心定义

通过设计代币的供给机制、分配策略、使用场景和激励结构，构建可持续的去中心化经济系统，使代币持有者的利益与协议的长期成功保持一致。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充协议目标或用户行为假设
- **发现矛盾**：当短期激励与长期可持续性冲突时，标记并寻求平衡方案
- **提前终止**：当已设计可行的代币经济模型或确认代币非必要时

---

## 思考流程

### Step 1: 协议价值主张分析

- 明确协议解决的核心问题
- 识别代币在协议中的功能性作用（治理、支付、质押、工作）
- 分析代币是否为协议必需（"为什么需要代币？"）
- 评估代币化带来的价值增量

---

### Step 2: 代币供给设计

- **供给模型选择**：
  - 固定上限（如比特币2100万枚）：创造稀缺性
  - 通胀模型（如以太坊）：持续激励参与者
  - 通缩模型（销毁机制）：减少流通量提升价值
- **发行机制**：
  - 一次性发行 vs 持续发行
  - 挖矿/质押奖励释放曲线
  - 团队、投资者、社区分配比例
- **释放计划（Vesting）**：
  - 锁仓期设计
  - 线性释放 vs 阶梯释放

---

### Step 3: 代币需求场景设计

- **功能性需求**：
  - 支付网络费用（Gas）
  - 质押获得服务或收益
  - 参与治理投票
  - 作为工作代币（如Chainlink）
- **投机性需求**：
  - 价值存储
  - 投资收益
- **网络效应**：
  - 用户增长如何提升代币价值
  - 代币价值如何吸引更多用户

---

### Step 4: 激励机制设计

- **正向激励**：
  - 质押奖励（Staking Rewards）
  - 流动性挖矿（Liquidity Mining）
  - 推荐奖励
  - 贡献者奖励
- **负向激励（惩罚）**：
  - 罚没机制（Slashing）
  - 不活跃惩罚
- **激励相容性分析**：
  - 诚实行为是否是最优策略
  - 攻击成本是否超过收益

---

### Step 5: 可持续性评估

- **长期激励来源**：
  - 协议收入（手续费、服务费）
  - 通胀发行的可持续性
  - 外部资金注入
- **死亡螺旋风险**：
  - 代币价格下跌 → 质押收益下降 → 更多抛售
  - 预防措施：多元化激励、协议收入支撑
- **市场操纵风险**：
  - 大户控盘
  - 流动性不足

---

### Step 6: 治理与演化

- **治理权分配**：
  - 代币持有量 vs 一币一票
  - 委托治理（Liquid Democracy）
  - 二次方投票
- **参数调整机制**：
  - 通胀率调整
  - 手续费调整
  - 奖励分配调整
- **协议升级机制**：
  - 硬分叉 vs 软分叉
  - 治理提案流程

---

## 关键原则

1. **价值捕获**：代币必须能捕获协议创造的价值。原因：无法捕获价值的代币只是投机工具，缺乏长期支撑。

2. **激励相容**：设计使个体理性行为与集体利益一致的机制。原因：如果诚实行为不是最优策略，系统将被攻击。

3. **可持续性优先**：避免依赖不可持续的补贴或 Ponzi 机制。原因：短期激励只能吸引投机者，长期价值才能留住用户。

4. **简洁性原则**：经济模型应简单易懂，降低用户认知门槛。原因：复杂的模型难以被理解和信任，阻碍采用。

5. **抗操纵设计**：防范大户操纵、套利攻击和死亡螺旋。原因：经济系统一旦被操纵，信任崩塌难以恢复。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**代币经济学特有关键检查项**：

- [ ] **代币是否为协议必需？** 还是可有可无的投机工具？
- [ ] **供给模型是否可持续？** 通胀/通缩是否合理？
- [ ] **代币是否有明确的功能性需求？** 还是仅依赖投机？
- [ ] **激励机制是否相容？** 诚实行为是否是最优策略？
- [ ] **是否存在死亡螺旋风险？** 如何预防？
- [ ] **经济模型是否简洁易懂？** 用户能否理解？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [game-theory-thinking](../thinking/game-theory-thinking/SKILL.md) | 基础 | 设计激励相容的机制 |
| [incentive-thinking](../thinking/incentive-thinking/SKILL.md) | 并行 | 分析激励对行为的影响 |
| [system-thinking](../thinking/system-thinking/SKILL.md) | 并行 | 理解代币经济的系统性反馈 |
| [feedback-loops](../thinking/feedback-loops/SKILL.md) | 并行 | 识别正反馈和负反馈循环 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Buterin, V. (2014). A Next-Generation Smart Contract and Decentralized Application Platform. *Ethereum White Paper*.
2. Zargham, M., Shorish, J., & Paruch, K. (2020). Foundations of Cryptoeconomic Systems. *SSRN Electronic Journal*.
3. Athey, S., Parashkevov, I., Sarukkai, V., & Xia, J. (2016). Bitcoin Pricing, Adoption, and Usage: Theory and Evidence. *Stanford University Graduate School of Business Research Paper*.
4. Sockin, M., & Xiong, W. (2023). A Model of Cryptocurrencies. *Management Science*, 69(11), 6684-7701.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
