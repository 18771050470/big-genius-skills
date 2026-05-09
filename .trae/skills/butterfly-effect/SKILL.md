---
name: butterfly-effect
description: |
  触发：当需要分析复杂系统中初始条件的微小变化如何导致长期结果的巨大差异、评估系统对初始条件的敏感性、或理解非线性系统的不可预测性时调用；常见信号包括"一个小改动引发了连锁反应"、"初始条件的微小差异"、"长期预测困难"、"系统对细节高度敏感"。
  不触发：当系统是完全线性且可预测的时；当仅需短期预测且系统稳定时；当问题不涉及时间演化或动态变化时。
  Invoke when: analyzing how small changes in initial conditions lead to large differences in long-term outcomes, assessing system sensitivity to initial conditions, or understanding unpredictability in nonlinear systems.
  Do NOT invoke when: the system is completely linear and predictable; when only short-term prediction is needed and the system is stable; when the problem does not involve time evolution or dynamic change.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["system-thinking", "emergence", "chaos-theory", "sensitive-dependence", "nonlinear-dynamics"]
---

# 蝴蝶效应思维（Butterfly Effect Thinking）

## 核心定义

初始条件的微小差异在非线性动态系统中被指数级放大，导致长期行为的不可预测性——确定性系统未必可预测。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统的动态方程、初始条件范围和历史演化数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别系统为线性稳定系统（非混沌），可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别系统动态特征

- 系统是否包含非线性反馈机制？（正反馈/负反馈的混合）
- 系统是否存在时间延迟？（延迟导致振荡和放大）
- 系统维度是否≥3？（低维系统通常不混沌）
- 系统是否远离平衡态？（平衡态附近通常线性化有效）

---

### Step 2: 评估初始条件敏感性

- 识别关键初始参数：哪些变量的微小变化会影响长期轨迹？
- 计算/估计李雅普诺夫指数（Lyapunov Exponent）：正值表示混沌
- 进行敏感性测试：改变初始条件1%，观察结果变化幅度
- 区分"敏感"与"不稳定"：敏感系统仍可能有吸引子结构

---

### Step 3: 分析放大机制

- 追踪微小扰动的传播路径：通过哪些反馈回路被放大？
- 识别放大节点：系统中的"杠杆点"在哪里？
- 评估放大速率：指数级（混沌）vs 多项式级（复杂但可预测）
- 检查是否存在阻尼机制：负反馈是否能在某阶段抑制放大？

---

### Step 4: 评估预测边界

- 确定可预测时间尺度：基于李雅普诺夫指数计算预测 horizon
- 区分短期可预测性与长期不可预测性
- 评估概率预测的可行性：即使轨迹不可预测，统计分布是否稳定？
- 识别系统吸引子：长期行为是否仍受限于特定区域（奇异吸引子）？

---

### Step 5: 设计鲁棒策略

- 避免依赖长期精确预测：采用适应性策略而非计划性策略
- 建立早期预警系统：在扰动尚小时检测并干预
- 设计冗余和缓冲：为不可预测的冲击预留空间
- 采用集合预测：运行多个初始条件的模拟，评估结果分布

---

### Step 6: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **非线性≠复杂，但复杂常含非线性**：线性系统即使复杂也可分解求解，非线性系统的叠加原理失效，导致整体行为不可还原为部分之和。
2. **确定性≠可预测性**：混沌系统是确定性的（无随机因素），但由于对初始条件的指数级敏感，长期行为在实践上不可预测。
3. **吸引子提供边界**：混沌并非完全随机，系统的长期行为通常被限制在奇异吸引子的几何结构中，统计特征可能稳定。
4. **短期可预测、长期需适应**：混沌系统的可预测时间尺度有限，超出后应采用适应性策略而非预测性策略。
5. **微小干预可能无效**：在混沌系统中，试图通过精确控制初始条件来操控长期结果通常失败，因为测量误差和噪声同样被放大。

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
- [ ] **蝴蝶效应特供**：是否正确识别了系统的非线性特征？线性系统不应被误判为混沌
- [ ] **蝴蝶效应特供**：是否评估了初始条件敏感性？是否进行了改变初始条件的敏感性测试？
- [ ] **蝴蝶效应特供**：是否分析了微小扰动的放大机制？传播路径和放大节点是否被追踪？
- [ ] **蝴蝶效应特供**：是否确定了可预测时间尺度？短期可预测性与长期不可预测性是否被区分？
- [ ] **蝴蝶效应特供**：是否检查了系统吸引子结构？长期行为是否被限制在特定区域内？
- [ ] **蝴蝶效应特供**：是否设计了适应性策略而非依赖长期精确预测？鲁棒性措施是否具体可执行？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"考虑不确定性"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [system-thinking](../system-thinking/SKILL.md) | 前置 | 系统思维帮助识别反馈回路和动态结构，为蝴蝶效应分析提供全局视角 |
| [emergence](../emergence/SKILL.md) | 并行 | 涌现行为常伴随混沌动力学，两者共同解释复杂系统的不可预测性 |
| [chaos-theory](../chaos-theory/SKILL.md) | 前置/互补 | 混沌理论提供李雅普诺夫指数、分岔分析等定量工具 |
| [sensitive-dependence](../sensitive-dependence/SKILL.md) | 并行 | 敏感依赖是蝴蝶效应的核心数学特征 |
| [nonlinear-dynamics](../nonlinear-dynamics/SKILL.md) | 前置 | 非线性动力学提供分析工具（相图、分岔图、吸引子） |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | 混沌理论基础（洛伦兹方程、李雅普诺夫指数等） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Lorenz, E. N. (1963). Deterministic nonperiodic flow. *Journal of the Atmospheric Sciences*, 20(2), 130-141.
2. Lorenz, E. N. (1972). Predictability: Does the flap of a butterfly's wings in Brazil set off a tornado in Texas? *American Association for the Advancement of Science*, 139th Meeting.
3. Strogatz, S. H. (2018). *Nonlinear Dynamics and Chaos: With Applications to Physics, Biology, Chemistry, and Engineering* (2nd ed.). Westview Press.
4. Gleick, J. (1987). *Chaos: Making a New Science*. Viking Penguin.
5. Smith, L. A. (2007). *Chaos: A Very Short Introduction*. Oxford University Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
