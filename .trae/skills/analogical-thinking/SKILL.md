
---
name: analogical-thinking
description: |
  触发：当遇到陌生问题、需要创新解决方案、或试图理解新领域时调用；常见信号包括 "这就像..."、"有没有类似的..."、"换个角度思考"等。
  不触发：当问题已有成熟标准解法无需创新时；当只需执行已知流程无需跨领域迁移时；当场景为纯逻辑推导或数值计算时。
  Invoke when facing a novel problem, seeking creative solutions, or trying to understand an unfamiliar domain; common signals include "this is like...", "is there something similar...", "think from another angle".
  Do NOT invoke when the problem has mature standard solutions requiring no innovation; when only executing known processes without cross-domain transfer; when the scenario is pure logical deduction or numerical calculation.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["first-principles-thinking", "lateral-thinking", "mind-mapping"]
---

# 类比思维 (Analogical Thinking)

## 核心定义

类比思维是一种通过发现两个不同领域之间的**深层结构相似性**，将已知领域的知识、模式或解决方案迁移到未知领域，从而产生新颖见解或创新方案的思维方式。它是创新和学习的核心引擎。

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

## 思考流程

### Step 1: 定义目标问题

- 清晰描述问题核心：目标是什么？关键约束是什么？期望成果是什么？
- 简洁的问题陈述（如：“如何让在线教育平台像游戏一样吸引用户？”）

### Step 2: 搜索候选源领域

- 从知识库、经验库中检索在**结构上**（而非表面上）相似且自身理解深入的领域。可以列出3-5个候选项，优先选择自己熟悉的领域。
- 候选源领域列表（如：游戏设计、戏剧表演、健身房会员体系）

### Step 3: 提取深层结构

- 分析源领域的关键元素、关系、流程、约束和反馈机制。绘制源领域的“结构模型”（如游戏中的升级系统：经验值→等级→解锁内容→成就感）。
- 源领域的结构抽象图（文字或图示）

### Step 4: 构建映射关系

- 系统性地找到目标元素与源元素之间的对应关系。明确哪些映射是有效的，哪些是无效的（不能强求）。
- 映射表（如：游戏经验值 ↔ 学习进度；游戏等级 ↔ 知识阶段；解锁内容 ↔ 进阶课程）

### Step 5: 迁移知识/解决方案

- 基于映射，将源领域的已知机制、策略或解法直接或改编后应用到目标领域。生成具体行动计划或设计草案。
- 初步的创新方案（如：设计“经验值+等级+成就徽章”的学习系统，模仿游戏即时反馈机制）

### Step 6: 验证与迭代

- 检查迁移后的方案是否在目标领域合理、可行且有效。特别关注映射中的“失配点”和隐藏风险。必要时修正映射或寻找更好的源领域。
- 优化后的最终方案 + 映射合理性检查报告

### Step 7: 记录与抽象化（可选）

- 将此次类比抽象为一个可复用的“类比模板”（如：“用户参与度提升系统可以借鉴游戏化设计”），存入个人思维库。
- 结构化的类比记录（源、目标、映射、效果、注意事项）

## 关键原则

1. **结构优先，表面为次**：类比的价值在于深层逻辑的相似，而非外观或名词的雷同。例如，将“蚊子吸血”类比为“疫苗注射”是基于“微小物体穿透皮肤输送物质”的结构相似，而非两者都讨厌。
2. **多样性保障稳健**：至少尝试2-3个不同领域的源，避免单一偏见的“锚定效应”。同一个问题可以用生物学、工程学、艺术等不同角度类比，综合评估。
3. **映射完整性与边界**：明确哪些特征一一对应，哪些不能对应。强求完美映射会导致错误。例如，用“国家边界”类比“细胞膜”时，要意识到国家有军队、细胞膜没有军队，不能映射。
4. **验证是必要环节**：迁移得到的方案必须经过逻辑推演或小规模测试，因为类比只是“启发式”而非“证明”。
5. **保持开放与迭代**：如果第一次类比不理想，回到Step2更换源领域。类比常常需要多次尝试才能找到最佳匹配。

## 自检清单

> 聚焦类比思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**类比思维特有关键检查项**：

- [ ] **目标问题是否被一句话清晰描述？** 问题定义是否模糊导致类比方向错误？
- [ ] **是否列出了至少2个不同的候选源领域？** 单一源领域是否限制了创新空间？
- [ ] **选择是否基于结构相似而非表面相似？** "看起来像"是否被错误地当作"工作原理像"？
- [ ] **源领域的核心结构是否被完整提取？** 元素、关系、流程是否被系统化梳理？
- [ ] **映射表中是否明确了哪些对应、哪些不对应？** 强求完美映射的风险是否被识别？
- [ ] **迁移后的方案是否在目标领域具有逻辑可行性？** 类比启发是否经过了独立验证？
- [ ] **是否考虑了映射不匹配的潜在风险？** 错误类比是否可能导致灾难性结论？
- [ ] **类比是否带来了真正的新见解？** 还是只是已有常识的包装？

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [first-principles-thinking](../thinking/first-principles-thinking/SKILL.md) | 互补/后置 | 当类比方案需要严格验证其基础合理性时，拆解到不可分元素再重构 |
| [lateral-thinking](../thinking/lateral-thinking/SKILL.md) | 并行 | 在搜索源领域时，用横向思维拓宽候选范围，避免思维定式 |
| [mind-mapping](../thinking/mind-mapping/SKILL.md) | 辅助 | 在提取结构时，用思维导图可视化源领域的元素关系 |
| [compound-thinking](../thinking/compound-thinking/SKILL.md) | 可选 | 当类比涉及长期积累效应（如知识复利、网络效应）时结合使用 |

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Hofstadter, D. (2001). *Fluid Concepts and Creative Analogies*. Basic Books.
2. Gentner, D. (1983). Structure-mapping: A theoretical framework for analogy. *Cognitive Science*, 7(2), 155-170.
3. Lakoff, G., & Johnson, M. (1980). *Metaphors We Live By*. University of Chicago Press.
4. Munger, C. T. (2005). *Poor Charlie's Almanack: The Wit and Wisdom of Charles T. Munger*. Donning Company Publishers.
```