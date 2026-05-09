---
name: triz
description: |
  触发：当面临技术矛盾需要创新解决方案时；当传统方法无法突破技术瓶颈时；当需要系统化地生成专利级创新方案时；常见信号包括"这个技术难题卡了很久""想要A就必须牺牲B""有没有完全不同的技术路线"。
  不触发：当问题已有成熟解决方案时；当非技术因素（市场、政策）是主要瓶颈时；当不需要创新只需执行时。
  Invoke when facing technical contradictions requiring innovative solutions, when traditional methods hit bottlenecks, or when systematic patent-level innovation is needed.
  Do NOT invoke when mature solutions already exist, when non-technical factors are the primary bottleneck, or when execution without innovation is sufficient.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["lateral-thinking", "first-principles-thinking", "constraint-thinking", "creative-thinking"]
---

# TRIZ（发明问题解决理论）

## 核心定义

由苏联发明家Genrich Altshuller于1946年创立的系统化创新方法论，通过分析20万份专利发现：只有1%的解决方案是真正的突破性发明，其余99%都遵循可重复的模式。TRIZ提供40个发明原理、39个工程参数和矛盾矩阵，将创新从随机试错转化为系统化流程。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充技术系统的组成、待改善参数、恶化参数、已有尝试
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已通过矛盾矩阵找到明确解决方案，可提前进入验证步骤，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 定义技术矛盾

- 想要改善什么参数？（速度、强度、可靠性、精度等）
- 改善该参数会导致什么参数恶化？
- 用39个工程参数描述矛盾：改善参数X vs 恶化参数Y
- 区分技术矛盾（参数冲突）和物理矛盾（同一参数相反要求）
- 标注矛盾类型：是否属于经典TRIZ矛盾矩阵覆盖范围

### Step 2: 查询矛盾矩阵

- 在39×39矛盾矩阵中查找改善参数与恶化参数的交叉点
- 矩阵推荐哪些发明原理？（通常1-4个原理）
- 记录矩阵推荐的所有原理编号
- 如果矛盾不在矩阵中，考虑使用分离原理处理物理矛盾

### Step 3: 应用发明原理

- 针对每个推荐原理，思考如何应用于当前问题：
  - **原理1：分割**——将物体分成独立部分、使物体可拆卸、提高分割程度
  - **原理2：抽取**——从物体中抽取有害部分/属性、抽取必要部分/属性
  - **原理3：局部质量**——物体不同部分执行不同功能、每个部分在最有利条件下工作
  - ...（共40个原理，按需展开）
- 每个原理至少生成1-2个具体方案
- 记录所有方案，不评判可行性

### Step 4: 运用分离原理（物理矛盾专用）

- **空间分离**：矛盾需求在不同空间位置满足（A在这里，B在那里）
- **时间分离**：矛盾需求在不同时间段满足（A在此时，B在彼时）
- **条件分离**：矛盾需求在不同条件下满足（A在X条件下，B在Y条件下）
- **系统级别分离**：矛盾需求在不同系统层级满足（子系统A，超系统B）
- 评估哪种分离方式最适合当前物理矛盾

### Step 5: 评估理想度

- 计算每个方案的理想度：有用功能 / (有害功能 + 成本)
- 理想最终解（IFR）：系统自己解决问题，不需要外部干预
- 向IFR靠近：哪些方案更接近"自服务""零成本""零危害"？
- 标注每个方案的专利潜力（高/中/低）

### Step 6: 验证与选择

- 用技术可行性评估每个方案
- 检查是否引入新的技术矛盾（二次矛盾）
- 评估实施成本和资源需求
- 选择最优方案或方案组合
- 标注：如果TRIZ无法解决，是否需要转向其他创新方法

### Step 7: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **矛盾是创新的路标**：技术矛盾不是障碍，而是指向突破方向的信号。原因：Altshuller发现所有发明本质上都是消除矛盾，矛盾定义得越清晰，解决方案越明确。
2. **理想度只增不减**：每个改进都应提升系统理想度（有用功能增加，有害功能和成本减少）。原因：技术系统的进化方向是向理想最终解逼近。
3. **模式比灵感可靠**：40个发明原理覆盖了95%的技术问题，系统化检索比等待灵感更高效。原因：20万份专利的分析证明创新有模式可循。
4. **物理矛盾是更高阶的机会**：当同一参数需要同时满足相反要求时，往往意味着颠覆性创新。原因：物理矛盾的解决通常涉及系统级别的重构，产生专利级创新。

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
- [ ] 技术矛盾是否被精确定义？是否用39个工程参数描述了矛盾？
- [ ] 是否查询了矛盾矩阵并记录了推荐的发明原理？
- [ ] 每个推荐原理是否至少生成了1个具体应用方案？
- [ ] 如果是物理矛盾，是否应用了分离原理（空间/时间/条件/系统级别）？
- [ ] 是否计算了各方案的理想度并向IFR靠近？
- [ ] 是否评估了二次矛盾（新方案是否引入了新矛盾）？
- [ ] 是否标注了方案的专利潜力？
- [ ] 输出具体可执行，不含模糊建议（如"尝试创新"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [lateral-thinking](../thinking/lateral-thinking/SKILL.md) | 关联 | TRIZ的40个原理是结构化的水平思考工具 |
| [first-principles-thinking](../thinking/first-principles-thinking/SKILL.md) | 前置 | 在应用TRIZ前，先用第一性原理拆解问题本质 |
| [constraint-thinking](../thinking/constraint-thinking/SKILL.md) | 关联 | 技术矛盾本质上就是约束，约束思维提供互补视角 |
| [creative-thinking](../thinking/creative-thinking/SKILL.md) | 关联 | TRIZ是结构化的创造性思维，创意阶段可互相补充 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | 40个发明原理详解和矛盾矩阵（可选） |

---

## 参考文献

1. Altshuller, G. S. (1984). *Creativity as an Exact Science: The Theory of the Solution of Inventive Problems*. Gordon and Breach.
2. Altshuller, G. S. (1999). *The Innovation Algorithm: TRIZ, Systematic Innovation and Technical Creativity*. Technical Innovation Center.
3. Rantanen, K., & Domb, E. (2002). *Simplified TRIZ: New Problem-Solving Applications for Engineers and Manufacturing Professionals*. CRC Press.
4. Savransky, S. D. (2000). *Engineering of Creativity: Introduction to TRIZ Methodology of Inventive Problem Solving*. CRC Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
