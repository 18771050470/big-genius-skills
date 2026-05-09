---
name: kaizen
description: |
  触发：当需要持续改进流程、提升质量和效率、建立学习型组织、或推动全员参与改善时；常见信号包括"改善"、"持续改进"、"小步快跑"、"PDCA"、"标准化"、"浪费消除"。
  不触发：当仅需一次性变革、组织文化不支持参与、或改进资源极度匮乏时。
  Invoke when pursuing continuous improvement, optimizing processes, or building learning organization.
  Do NOT invoke for one-time transformation, when culture doesn't support participation, or resources are extremely scarce.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["pdca-cycle", "lean-eliminate-waste", "standardization-thinking", "iteration-thinking"]
---

# 改善思维 (Kaizen)

## 核心定义

源自丰田生产系统的持续改进哲学，强调通过全员参与、小步快跑、标准化和PDCA循环，不断消除浪费、提升质量、优化流程，实现渐进式卓越。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充当前流程现状、主要痛点、改进资源、团队参与意愿
- **发现矛盾**：当改进方向与战略目标冲突时，标记并寻求澄清
- **提前终止**：当已识别关键改进点或确认需要更多数据时

---

## 思考流程

### Step 1: 现状分析与浪费识别

- **现状把握**：
  - 现场观察（Gemba Walk）
  - 数据收集与可视化
  - 流程图绘制
  - 识别增值与非增值活动
- **七大浪费识别（Muda）**：
  - 过量生产浪费
  - 等待浪费
  - 搬运浪费
  - 过度加工浪费
  - 库存浪费
  - 动作浪费
  - 不良品浪费
- **三不原则检查**：
  - 不合理（Muri）：超负荷、过度要求
  - 不均衡（Mura）：波动、不稳定
  - 浪费（Muda）：不增值活动

---

### Step 2: 问题定义与目标设定

- **问题描述**：
  - 用数据描述现状
  - 明确问题范围和影响
  - 区分症状与根因
- **目标设定（SMART）**：
  - 具体、可衡量、可达成
  - 与战略目标对齐
  - 设定挑战性但可实现的目标
- **成功标准定义**：
  - 量化指标（效率、质量、成本）
  - 定性指标（员工满意度、客户体验）
  - 时间节点

---

### Step 3: 根因分析

- **5Why分析法**：
  - 连续追问5个为什么
  - 从表象深入到根因
  - 避免停留在表面原因
- **鱼骨图（Ishikawa）**：
  - 人、机、料、法、环、测六维度
  - 头脑风暴可能原因
  - 筛选关键原因
- **数据验证**：
  - 收集数据验证假设
  - 区分主观判断与客观事实
  - 确定主要根因

---

### Step 4: 对策制定与实施

- **对策生成**：
  - 头脑风暴多种方案
  - 评估可行性与效果
  - 选择最优方案
- **快速试行**：
  - 小范围试点
  - 快速验证效果
  - 收集反馈
- **标准化准备**：
  - 制定标准作业程序
  - 准备培训材料
  - 设定检查机制

---

### Step 5: 效果验证与标准化

- **效果测量**：
  - 对比改进前后数据
  - 验证目标达成情况
  - 量化收益（成本、效率、质量）
- **标准化**：
  - 更新作业标准
  - 培训相关人员
  - 建立维持机制
- **横向展开**：
  - 将成功经验推广
  - 复制到其他区域/流程
  - 建立最佳实践库

---

### Step 6: 持续改善循环

- **PDCA循环**：
  - Plan（计划）：设定改进目标
  - Do（执行）：实施改进措施
  - Check（检查）：验证效果
  - Act（处置）：标准化或调整
- **改善文化建立**：
  - 鼓励员工提出改善建议
  - 建立改善提案制度
  - 认可和奖励改善行为
- **长期机制**：
  - 定期改善活动（改善周、改善月）
  - 建立改善指标跟踪
  - 持续培训和能力建设

---

### Step 7: 总结输出

- 提供现状分析和浪费识别结果
- 给出根因分析和对策方案
- 列出改进效果量化数据
- 说明标准化和维持机制
- 建议下一步改善方向

---

## 关键原则

1. **改善是每个人的工作**：从CEO到一线员工，全员参与改善。原因：最接近问题的人最清楚问题，全员参与释放集体智慧。

2. **小步快跑优于大爆炸**：小步改进降低风险，快速验证。原因：大变革失败成本高，小改进可持续积累。

3. **标准化是改善的基础**：没有标准就无法衡量改善。原因：标准是现状的最佳实践，是下一个改善的起点。

4. **现场现物（Gemba）**：去现场看实物，掌握真实情况。原因：数据可能失真，现场观察获取第一手信息。

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
- [ ] 考虑了二阶/三阶效应（如改进的副作用）
- [ ] 输出具体可执行，不含模糊建议
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [pdca-cycle](../thinking/pdca-cycle/SKILL.md) | 核心 | PDCA是改善的基本方法论 |
| [lean-eliminate-waste](../thinking/lean-eliminate-waste/SKILL.md) | 并行 | 精益消除浪费是改善的核心内容 |
| [standardization-thinking](../thinking/standardization-thinking/SKILL.md) | 后置 | 标准化是改善成果的固化 |
| [iteration-thinking](../thinking/iteration-thinking/SKILL.md) | 并行 | 迭代思维支持小步快跑 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 改善案例分析 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Ohno, T. (1988). *Toyota Production System: Beyond Large-Scale Production*. Productivity Press.
2. Imai, M. (1986). *Kaizen: The Key to Japan's Competitive Success*. McGraw-Hill.
3. Toyota Motor Corporation. *Toyota Production System*.
4. Lean TPS. (2024). *Reclaiming Kaizen: Governance, Architecture, and the Discipline of Learning in the Toyota Production System*.
