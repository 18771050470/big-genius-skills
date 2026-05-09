---
name: zero-knowledge-proof
description: |
  触发：当需要证明某个陈述的真实性而不泄露底层信息、保护隐私的同时建立信任、或进行身份验证而不暴露敏感数据时；常见信号包括"隐私保护"、"证明而不泄露"、"身份验证"、"保密"、"zk-SNARK"。
  不触发：当验证者需要知道完整信息、当计算资源极其有限无法承担证明生成成本、当交互式证明不可行时。
  Invoke when needing to prove statement validity without revealing underlying information, protecting privacy while establishing trust, or identity verification without exposing sensitive data.
  Do NOT invoke when verifier needs complete information, when compute resources are too limited, or when interactive proofs are infeasible.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L3"
  related: ["distributed-trust", "cryptographic-thinking", "privacy-by-design", "probabilistic-thinking"]
---

# 零知识证明思维 (Zero-Knowledge Proof)

## 核心定义

一种密码学协议，允许证明者向验证者证明某个陈述为真，而验证者除了"陈述为真"这一事实外，无法获得关于证明内容的任何额外信息——实现"证明知识而不泄露知识"的密码学目标。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充证明的数学陈述或安全要求
- **发现矛盾**：当零知识属性与可验证性需求冲突时，标记并寻求权衡方案
- **提前终止**：当已找到合适的ZKP方案或确认ZKP不适用时

---

## 思考流程

### Step 1: 问题建模与陈述定义

- 明确需要证明的数学陈述（如"我知道x使得H(x)=y"）
- 识别需要保护的敏感信息（witness/witness）
- 确定公开信息（statement/public input）
- 评估证明的复杂度和计算资源需求

---

### Step 2: ZKP方案选择

- **交互式vs非交互式**：
  - 交互式：需要多轮通信（如Sigma协议）
  - 非交互式：一次性生成证明（如zk-SNARK、zk-STARK）
- **证明大小考量**：
  - zk-SNARK：证明极小（~200字节），适合链上验证
  - zk-STARK：证明较大但无需可信设置
  - Bulletproofs：中等大小，无需可信设置
- **计算成本权衡**：
  - 证明生成时间（通常较慢）
  - 验证时间（通常极快）
- **可信设置需求**：
  - 需要：zk-SNARK（需安全销毁初始参数）
  - 无需：zk-STARK、Bulletproofs

---

### Step 3: 电路设计与约束构建

- 将计算问题转化为算术电路
- 定义约束系统（R1CS、Plonkish等）
- 优化电路规模（减少约束数量）
- 确保电路正确编码原始问题

---

### Step 4: 证明生成

- 使用proving key生成证明
- 输入witness（私密输入）和statement（公开输入）
- 执行证明算法生成证明π
- 验证证明格式的正确性

---

### Step 5: 验证与安全性分析

- 使用verification key验证证明
- 检查完备性（诚实验证者总能验证真陈述）
- 检查可靠性（伪造证明计算不可行）
- 检查零知识性（证明不泄露witness信息）
- 评估后量子安全性（zk-STARK具备，zk-SNARK不具备）

---

### Step 6: 系统集成与优化

- 集成到目标系统（区块链、身份认证等）
- 优化证明生成性能（并行化、GPU加速）
- 建立证明生成和验证的监控
- 输出应包含：方案选择 + 电路设计 + 安全分析 + 集成建议

---

## 关键原则

1. **最小泄露原则**：只证明必要的事实，不泄露任何额外信息。原因：零知识属性的核心价值在于隐私保护，任何信息泄露都违背设计目标。

2. **可验证性优先**：确保证明可被独立高效验证。原因：零知识证明的价值在于建立信任，无法验证的证明失去意义。

3. **计算成本权衡**：在证明生成成本和验证成本之间平衡。原因：ZKP通常证明慢但验证快，需要根据应用场景优化。

4. **可信设置审慎**：需要可信设置的方案必须确保初始参数安全销毁。原因：泄露初始参数会导致伪造证明成为可能。

5. **后量子准备**：考虑量子计算威胁，优先选择后量子安全的方案。原因：量子计算机可能破解基于椭圆曲线的ZKP方案。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**零知识证明特有关键检查项**：

- [ ] **陈述是否被正确形式化为数学问题？** 逻辑完备吗？
- [ ] **敏感信息（witness）是否被充分保护？** 证明中无泄露？
- [ ] **选择的ZKP方案是否适合应用场景？** 交互式还是非交互式？
- [ ] **电路设计是否正确编码了原始问题？** 有无逻辑错误？
- [ ] **可信设置（如需要）是否安全执行？** 初始参数是否销毁？
- [ ] **是否考虑了后量子安全性？** 量子威胁如何应对？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [distributed-trust](../thinking/distributed-trust/SKILL.md) | 并行 | 在去中心化环境中建立无需信任的验证 |
| [cryptographic-thinking](../thinking/cryptographic-thinking/SKILL.md) | 基础 | 理解零知识证明的密码学基础 |
| [privacy-by-design](../thinking/privacy-by-design/SKILL.md) | 并行 | 将隐私保护嵌入系统设计 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 理解零知识证明的概率完备性 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Goldwasser, S., Micali, S., & Rackoff, C. (1985). The Knowledge Complexity of Interactive Proof Systems. *Proceedings of the 17th Annual ACM Symposium on Theory of Computing*, 291-304.
2. Ben-Sasson, E., Chiesa, A., Garman, C., Green, M., Miers, I., Tromer, E., & Virza, M. (2014). Zerocash: Decentralized Anonymous Payments from Bitcoin. *2014 IEEE Symposium on Security and Privacy*, 459-474.
3. Ben-Sasson, E., Bentov, I., Horesh, Y., & Riabzev, M. (2018). Scalable, Transparent, and Post-Quantum Secure Computational Integrity. *Cryptology ePrint Archive*.
4. Parno, B., Howell, J., Gentry, C., & Raykova, M. (2013). Pinocchio: Nearly Practical Verifiable Computation. *2013 IEEE Symposium on Security and Privacy*, 238-252.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
