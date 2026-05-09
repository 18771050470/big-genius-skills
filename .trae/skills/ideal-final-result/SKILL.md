---
name: ideal-final-result
description: |
  触发：当面对复杂创新问题需要突破心理惯性、寻找突破性解决方案、评估技术系统发展方向或消除技术矛盾时；常见信号包括"理想解"、"突破瓶颈"、"消除矛盾"、"完美方案"、"TRIZ"、"创新设计"。
  不触发：当问题已有明确标准答案、当资源极度受限无法追求理想状态、当时间紧迫需要快速妥协方案时。
  Invoke when facing complex innovation problems requiring breakthrough thinking, evaluating technical system evolution, or resolving technical contradictions.
  Do NOT invoke when problems have clear standard solutions, when resources are extremely limited, or when quick compromise is needed.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L3"
  related: ["triz", "first-principles-thinking", "constraint-thinking", "technical-system-evolution-laws", "function-analysis"]
---

# 最终理想解思维 (Ideal Final Result)

## 核心定义

一种TRIZ创新思维方法，通过设想系统在保持功能的同时自我消除（理想度趋向无穷大），突破心理惯性束缚，引导创新方向朝向功能实现与系统存在的完美统一。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统的核心功能、当前限制条件、目标组件
- **发现矛盾**：当理想解与物理可行性冲突时，标记矛盾类型（技术矛盾/物理矛盾）并寻求消除路径
- **提前终止**：当已找到可实现的近似理想解或确认理想解在当前技术条件下不可达时

---

## 思考流程

### Step 1: 系统功能界定

- 明确技术系统的核心功能（Main Function）是什么
- 识别目标组件（Target）：功能作用的直接对象
- 区分基本功能、附加功能和辅助功能
- 排除与核心功能无关的组件和特性

---

### Step 2: 理想最终状态设想

- 运用IFR公式："系统本身执行所需功能，但系统自身不存在"
- 思考：如果资源无限、物理定律可调整，最完美的解决方案是什么
- 设想功能自我实现的状态（如：物体自我移动而不需要运输系统）
- 记录所有阻碍理想状态实现的因素（即矛盾点）

---

### Step 3: 理想度评估与障碍识别

- 计算当前系统的理想度：Idealness = Σ有用功能 / (Σ有害功能 + 成本)
- 识别导致理想度降低的关键因素：
  - 有害功能（系统带来的副作用）
  - 冗余组件（对核心功能非必需的部件）
  - 能量/信息/物质传递损耗
- 明确技术矛盾（改善A导致恶化B）和物理矛盾（同一参数需要相反状态）

---

### Step 4: 向IFR逼近的路径设计

- 运用TRIZ分离原理处理物理矛盾：
  - 空间分离：在A位置是X，在B位置是Y
  - 时间分离：在T1时刻是X，在T2时刻是Y
  - 条件分离：在条件C下是X，在非C下是Y
  - 系统级别分离：子系统是X，超系统是Y
- 运用40个发明原理消除技术矛盾
- 思考：如何让系统组件"自我服务"（Self-service）

---

### Step 5: 功能理想模型构建

- 构建功能理想模型（FIM, Functional Ideal Model）：
  - X元素自己改变Y参数（消除执行器）
  - 环境或超系统元素执行功能（消除系统组件）
  - 消除目标组件本身（功能由其他方式实现）
- 评估各FIM的可实现性和理想度提升潜力
- 选择最优路径或组合多个FIM

---

### Step 6: 现实约束与过渡方案

- 评估当前技术条件下最接近IFR的方案
- 设计分阶段实现路径：
  - 短期：可立即实现的改进
  - 中期：技术成熟后可实现的突破
  - 长期：接近理想状态的终极方案
- 识别需要突破的关键技术瓶颈

---

### Step 7: 总结输出

- 明确最终理想解（IFR）的定义
- 列出识别的所有矛盾及其消除思路
- 提供向IFR逼近的具体路径建议
- 标注关键假设和技术不确定性
- 建议下一步调用的Skill（如需要矛盾矩阵分析，调用function-analysis）

---

## 关键原则

1. **功能导向而非形式导向**：关注"功能如何实现"而非"现有组件如何改进"。原因：心理惯性往往束缚于现有形式，阻碍突破性创新。

2. **理想度最大化原则**：持续追求有用功能增加、有害功能减少、系统简化。原因：技术系统的进化方向就是理想度不断提高。

3. **矛盾是创新的钥匙**：识别并消除矛盾（而非妥协）是达到理想解的必经之路。原因：阿奇舒勒研究发现，所有发明问题的核心都是消除矛盾。

4. **系统自我消除趋势**：最理想的状态是系统功能由目标自身、环境或超系统实现。原因：这代表了资源利用的最高效率和系统复杂度的最低化。

5. **IFR作为方向而非终点**：IFR可能当前不可达，但它指明了创新的正确方向。原因：即使只能部分实现，向IFR逼近的过程本身就产生高价值创新。

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
- [ ] 考虑了二阶/三阶效应（如技术演进对产业的影响）
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [triz](../thinking/triz/SKILL.md) | 前置 | 需要理解TRIZ整体框架时先调用 |
| [technical-system-evolution-laws](../thinking/technical-system-evolution-laws/SKILL.md) | 并行 | 评估系统所处S曲线阶段，判断IFR的可行性 |
| [function-analysis](../thinking/function-analysis/SKILL.md) | 后置 | 需要深入分析组件功能时调用 |
| [first-principles-thinking](../thinking/first-principles-thinking/SKILL.md) | 并行 | 从第一性原理角度重新审视IFR |
| [constraint-thinking](../thinking/constraint-thinking/SKILL.md) | 后置 | 识别约束条件后，评估如何在约束下逼近IFR |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整IFR分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | TRIZ理论背景与阿奇舒勒研究（可选） |

---

## 参考文献

1. Altshuller, G.S. (1986). *To Find an Idea: Introduction to Theory of Inventive Problem Solving*. Nauka Publishers.
2. Altshuller, G.S. (1973). *Algorithm of Invention*. Moscow Worker Publishers.
3. MATRIZ Official Materials. TRIZ Trends of Engineering Systems Evolution (TESE).
4. 创新世界 (Innovation.World). Ideal Final Result Theory.
