---
name: cognitive-load-theory
description: |
  触发：当设计学习材料、优化信息呈现、评估任务复杂度、或提升学习效率时；常见信号包括"认知负荷"、"工作记忆"、"学习设计"、"信息过载"、"任务复杂度"。
  不触发：当任务简单、无需学习新知、或资源充足时。
  Invoke when designing learning materials, optimizing information presentation, assessing task complexity, or improving learning efficiency.
  Do NOT invoke for simple tasks, no new learning required, or abundant resources.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["learning-design", "working-memory", "instructional-design", "information-processing"]
---

# 认知负荷理论 (Cognitive Load Theory)

## 核心定义

由约翰·斯威勒（John Sweller）于1988年提出的教学设计理论，基于工作记忆的容量有限性和长期记忆的无限存储能力，提出三种认知负荷类型（内在、外在、相关），指导如何设计教学材料以优化学习效果。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充学习者先验知识、任务复杂度、时间限制、学习目标
- **发现矛盾**：当简化材料与学习目标冲突时，标记并评估取舍
- **提前终止**：当已确定最优设计或发现更适合的其他教学设计框架时

---

## 思考流程

### Step 1: 理解认知架构

- **工作记忆限制**：
  - 容量：7±2个组块（Miller, 1956）
  - 持续时间：约20秒
  - 处理瓶颈：同时处理元素有限
- **长期记忆优势**：
  - 容量：几乎无限
  - 存储：图式（schemas）
  - 自动化：熟练技能减少工作记忆负荷
- **学习本质**：
  - 工作记忆→长期记忆的编码
  - 图式构建与自动化
  - 认知负荷管理是关键

---

### Step 2: 评估内在认知负荷

- **定义**：由学习材料本身的复杂性决定，与学习者的先验知识交互
- **元素交互性**：
  - 低交互性：元素可独立学习
  - 高交互性：元素必须同时处理
- **影响因素**：
  - 材料固有复杂度
  - 学习者专业知识（ expertise reversal effect）
  - 任务类型
- **管理策略**：
  - 分块（chunking）
  - 顺序呈现
  - 先建立基础
  - 逐步增加复杂度

---

### Step 3: 减少外在认知负荷

- **定义**：由不良教学设计产生，不贡献于学习
- **常见来源**：
  - 冗余信息
  - 分散注意（split-attention）
  - 无关装饰
  - 不良格式
  - 不必要的重复
- **减少策略**：
  - 消除冗余
  - 整合信息源
  - 简化格式
  - 信号增强（signaling）
  - 模态效应（modality effect）：视觉+听觉双通道

---

### Step 4: 促进相关认知负荷

- **定义**：投入于图式构建和自动化的认知资源
- **促进策略**：
  - 变式练习（varied practice）
  - 分散练习（spacing）
  - 交错练习（interleaving）
  - 自我解释
  - 生成性学习
- **平衡原则**：
  - 总负荷不超过工作记忆容量
  - 减少外在负荷以释放资源给相关负荷
  - 内在负荷通过专业知识降低

---

### Step 5: 应用教学设计原则

- **样例效应（Worked Example Effect）**：
  - 新手：提供完整样例
  - 专家：减少指导
  - 渐隐（fading）：逐步减少支持
- **完成问题（Completion Problem）**：
  - 部分完成的样例
  - 学习者填补缺失部分
  - 过渡阶段
- **指导消退（Guidance Fading）**：
  - 从完整指导到独立解决
  - 根据学习者进步调整
  -  expertise reversal effect

---

### Step 6: 优化信息呈现

- **多媒体原则**：
  - 文字+图像 > 仅文字
  - 图像应相关而非装饰
- **空间接近原则**：
  - 相关文字和图像靠近
  - 减少视觉搜索
- **时间接近原则**：
  - 同步呈现相关元素
  - 避免时间分离
- **一致性原则**：
  - 消除无关材料
  - 统一设计风格
- **信号原则**：
  - 突出关键信息
  - 引导注意力

---

### Step 7: 评估学习者特征

- **先验知识**：
  - 新手：需要更多指导
  - 专家：需要更少指导
  -  expertise reversal effect
- **认知能力**：
  - 工作记忆容量
  - 处理速度
  - 先备知识
- **动机水平**：
  - 内在动机
  - 外在动机
  - 学习意愿
- **调整策略**：
  - 自适应学习
  - 个性化路径
  - 动态难度调整

---

### Step 8: 测量认知负荷

- **主观测量**：
  - NASA-TLX任务负荷指数
  - Paas量表（9点量表）
  - 心理努力评估
- **客观测量**：
  - 眼动追踪
  - 心率变异性
  - 脑电图（EEG）
  - 双任务范式
- **绩效测量**：
  - 学习效率
  - 迁移测试
  - 保持测试
  - 错误率

---

### Step 9: 迭代优化

- **设计-实施-评估循环**：
  - 基于理论设计
  - 实施教学
  - 测量认知负荷和学习效果
  - 分析结果
  - 优化设计
- **持续改进**：
  - 收集反馈
  - A/B测试
  - 数据驱动决策
  - 最佳实践积累

---

### Step 10: 总结输出

- 认知架构分析
- 内在负荷评估与管理
- 外在负荷减少策略
- 相关负荷促进方法
- 教学设计原则应用
- 信息呈现优化
- 学习者特征评估
- 认知负荷测量
- 迭代优化计划

---

## 关键原则

1. **工作记忆是学习的瓶颈**：容量有限，必须有效管理。原因：所有新信息必须通过工作记忆处理，超载导致学习失败。

2. **三种认知负荷此消彼长**：减少外在负荷可为相关负荷释放资源。原因：工作记忆总容量固定，优化分配是关键。

3. **专业知识逆转效应**：对专家有效的指导对新手可能无效，反之亦然。原因：专家已有图式，额外指导反而成为外在负荷。

4. **双通道处理优势**：视觉和听觉通道可同时使用，增加总容量。原因：工作记忆有独立的视觉空间和语音环路子系统。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**完整检查项**：

- [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
- [ ] 每步思考要点已覆盖，无遗漏
- [ ] 每步结论标注了置信度和反证可能性
- [ ] 考虑了二阶/三阶效应（如教学设计对学习者长期动机的影响）
- [ ] 输出具体可执行，不含模糊建议
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [learning-design](../thinking/learning-design/SKILL.md) | 核心 | 学习设计是CLT的应用 |
| [working-memory](../thinking/working-memory/SKILL.md) | 核心 | 工作记忆是CLT的基础 |
| [instructional-design](../thinking/instructional-design/SKILL.md) | 并行 | 教学设计是CLT的实践 |
| [information-processing](../thinking/information-processing/SKILL.md) | 并行 | 信息处理是CLT的理论基础 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 认知负荷理论应用案例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Sweller, J. (1988). *Cognitive Load During Problem Solving: Effects on Learning*. Cognitive Science.
2. Sweller, J., van Merriënboer, J. J. G., & Paas, F. (2019). *Cognitive Architecture and Instructional Design: 20 Years Later*. Educational Psychology Review.
3. Paas, F., & Sweller, J. (2012). *An Evolutionary Upgrade of Cognitive Load Theory: Using the Human Motor System and Collaboration to Support the Learning of Complex Cognitive Tasks*. Educational Psychology Review.
4. Miller, G. A. (1956). *The Magical Number Seven, Plus or Minus Two*. Psychological Review.
5. SciMath. *Using Sweller's cognitive load theory to improve learning*.
6. PMC. *The Validity of Physiological Measures to Identify Differences in Intrinsic Cognitive Load*.
