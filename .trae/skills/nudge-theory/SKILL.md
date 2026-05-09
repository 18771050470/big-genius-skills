---
name: nudge-theory
description: |
  触发：当需要设计行为干预、优化选择架构、推动积极行为改变、或在不限制自由的前提下引导决策时；常见信号包括"助推"、"选择架构"、"行为设计"、"默认选项"、" libertarian paternalism"。
  不触发：当需要强制规定、完全自由放任、或涉及道德敏感的行为控制时。
  Invoke when designing behavioral interventions, optimizing choice architecture, promoting positive behavior change, or guiding decisions without restricting freedom.
  Do NOT invoke for mandatory regulations, complete laissez-faire, or morally sensitive behavior control.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["behavioral-economics", "choice-architecture", "behavioral-design", "libertarian-paternalism"]
---

# 助推理论 (Nudge Theory)

## 核心定义

由理查德·塞勒和卡斯·桑斯坦提出的行为经济学理论，指通过设计选择架构（Choice Architecture），在不禁止任何选项、不改变经济激励的前提下，以可预测的方式改变人们的行为，使其做出更符合自身长远利益的决策。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充目标行为、当前行为模式、环境约束、受众特征
- **发现矛盾**：当助推设计与伦理原则冲突时，标记并重新评估
- **提前终止**：当已确定有效助推策略或发现更适合的其他干预方式时

---

## 思考流程

### Step 1: 定义目标行为

- **行为识别**：
  - 希望促进的积极行为
  - 希望减少的消极行为
  - 行为的可测量性
- **行为动机分析**：
  - 内在动机vs外在动机
  - 当前行为的原因
  - 改变的障碍
- **成功标准**：
  - 行为改变的程度
  - 时间框架
  - 可持续性要求

---

### Step 2: 分析当前选择架构

- **默认选项**：
  - 当前默认设置是什么？
  - 默认选项的影响范围
  - 默认选项的合理性
- **信息呈现**：
  - 信息的可获得性
  - 信息的清晰度
  - 信息的框架方式
- **选择复杂度**：
  - 选项数量
  - 选项间的比较难度
  - 决策成本
- **摩擦成本**：
  - 采取行动的便利程度
  - 时间成本
  - 认知成本

---

### Step 3: 识别行为障碍

- **认知偏差**：
  - 现状偏见（Status Quo Bias）
  - 损失厌恶（Loss Aversion）
  - 拖延倾向（Procrastination）
  - 过度自信（Overconfidence）
- **情境因素**：
  - 时间压力
  - 信息过载
  - 社会压力
  - 环境因素
- **能力限制**：
  - 知识不足
  - 技能缺乏
  - 资源约束
  - 注意力有限

---

### Step 4: 设计助推工具

- **默认选项（Defaults）**：
  - 设置有益的默认选项
  - 简化退出机制
  - 智能默认设置
- **简化选择（Simplify）**：
  - 减少选项数量
  - 分类组织选项
  - 突出关键信息
- **社会规范（Social Norms）**：
  - 展示他人行为
  - 社会认同提示
  - 同伴压力利用
- **及时提醒（Timing）**：
  - 关键时刻干预
  - 新鲜开始效应
  - 习惯养成时机
- **损失框架（Loss Framing）**：
  - 强调不行动的代价
  - 机会成本呈现
  - 后悔预期
- **承诺机制（Commitment）**：
  - 公开承诺
  - 软承诺设计
  - 自我约束工具

---

### Step 5: 遵循伦理原则

- **自由保留（Freedom Preserving）**：
  - 不禁止任何选项
  - 退出机制简便
  - 尊重个人选择
- **透明度（Transparency）**：
  - 助推机制公开
  - 目的明确告知
  - 避免隐藏操纵
- **福利导向（Welfare Oriented）**：
  - 真正符合受众利益
  - 避免家长式过度干预
  - 考虑长期后果
- **选择架构师责任**：
  - 意识到无法中立
  - 主动设计向善
  - 接受问责

---

### Step 6: 测试与优化

- **A/B测试**：
  - 不同助推策略对比
  - 效果量化评估
  - 最优方案识别
- **试点实施**：
  - 小范围试验
  - 问题识别
  - 迭代改进
- **效果评估**：
  - 行为改变程度
  - 意外后果监测
  - 成本效益分析

---

### Step 7: 实施与推广

- **分阶段实施**：
  - 从简单到复杂
  - 从试点到全面
  - 持续优化调整
- **沟通策略**：
  - 向受众解释助推目的
  - 建立信任
  - 减少抵触
- **监测机制**：
  - 实时效果追踪
  - 反馈收集
  - 动态调整

---

### Step 8: 评估长期影响

- **行为持续性**：
  - 短期效果vs长期习惯
  - 行为固化程度
  - 反弹风险
- **溢出效应**：
  - 对其他行为的影响
  - 正面溢出vs负面溢出
  - 系统性影响
- **伦理反思**：
  - 是否真正增进了福利？
  - 是否尊重了自主性？
  - 是否存在滥用风险？

---

### Step 9: 典型应用场景

- **健康领域**：
  - 健康饮食选择（食堂食品摆放）
  - 运动促进（默认加入健身计划）
  - 疫苗接种（默认预约）
- **财务领域**：
  - 退休储蓄（自动加入养老金计划）
  - 储蓄习惯（自动转账）
  - 债务管理（还款提醒）
- **环保领域**：
  - 节能行为（默认绿色选项）
  - 垃圾分类（简化分类标准）
  - 可持续消费（环保产品突出）
- **教育领域**：
  - 学习动机（进度可视化）
  - 课程选择（智能推荐）
  - 作业完成（截止日期提醒）

---

### Step 10: 总结输出

- 明确目标行为和成功标准
- 分析当前选择架构和行为障碍
- 设计符合伦理的助推工具
- 制定测试和优化方案
- 规划实施和推广策略
- 建立长期效果评估机制
- 识别典型应用场景
- 提供具体可执行的助推方案

---

## 关键原则

1. **助推不是强制**：助推保留选择的自由，只是改变选择的成本结构。原因：强制的正当性要求高，助推更易被接受且尊重自主性。

2. **选择架构无法中立**：任何环境都有选择架构，关键是谁来设计、为何目的。原因：不作为也是一种选择，主动设计向善比放任更好。

3. **助推必须符合受众利益**：助推的目的是帮助人们做出更好的决策，而非操纵。原因：伦理底线，避免家长主义滥用。

4. **透明度增强合法性**：公开助推机制，让受众知情。原因：知情同意原则，建立信任关系。

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
- [ ] 考虑了二阶/三阶效应（如助推的长期行为固化效应）
- [ ] 输出具体可执行，不含模糊建议
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [behavioral-economics](../thinking/behavioral-economics/SKILL.md) | 核心 | 行为经济学是助推理论基础 |
| [choice-architecture](../thinking/choice-architecture/SKILL.md) | 核心 | 选择架构是助推的实现方式 |
| [behavioral-design](../thinking/behavioral-design/SKILL.md) | 并行 | 行为设计应用助推理论 |
| [libertarian-paternalism](../thinking/libertarian-paternalism/SKILL.md) | 并行 | 自由家长主义是助推的伦理基础 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 助推理论应用案例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Thaler, R. H., & Sunstein, C. R. (2008). *Nudge: Improving Decisions About Health, Wealth, and Happiness*. Yale University Press.
2. Thaler, R. H., Sunstein, C. R., & Balz, J. P. (2010). *Choice Architecture*.
3. Thaler, R. H. (2018). *Nudge, Not Sludge*. Science.
4. Arab Psychology. (2024). *Choice Architecture: Nudge Theory & Examples*.
5. Stanford University. *Choice Architecture*.
