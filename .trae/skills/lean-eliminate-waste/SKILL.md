---
name: lean-eliminate-waste
description: |
  触发：当需要优化流程效率、降低成本、缩短交付周期、或提升价值流动时；常见信号包括"精益"、"浪费"、"价值流"、"Muda"、"JIT"、"流动"、"拉动"。
  不触发：当流程已高度优化、创新比效率更重要、或一次性项目无需持续流动时。
  Invoke when optimizing process efficiency, reducing costs, shortening lead time, or improving value flow.
  Do NOT invoke when process is already optimized, innovation matters more than efficiency, or for one-time projects.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L2"
  related: ["kaizen", "six-sigma", "just-in-time", "value-stream-mapping"]
---

# 精益消除浪费 (Lean / Eliminate Waste)

## 核心定义

源自丰田生产系统的管理哲学，通过识别和消除八大浪费（Muda），最大化客户价值，最小化资源消耗，实现价值流的连续流动和持续改进。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充价值流现状、客户价值定义、流程瓶颈、资源约束
- **发现矛盾**：当消除浪费与质量/安全冲突时，标记并寻求平衡方案
- **提前终止**：当已识别主要浪费源或确认需要更多流程数据时

---

## 思考流程

### Step 1: 价值定义与客户识别

- **客户识别**：
  - 直接客户（下一工序/最终用户）
  - 内部客户与外部客户
  - 客户需求和期望
- **价值定义**：
  - 客户愿意付费的活动
  - 改变产品形态/功能的作业
  - 第一次就做对的正确行动
- **价值标准**：
  - 质量（符合规格）
  - 交付（准时交付）
  - 成本（合理价格）
  - 服务（响应速度）

---

### Step 2: 价值流图绘制（VSM）

- **当前状态图**：
  - 识别所有工序和活动
  - 标注增值/非增值时间
  - 显示库存和信息流
  - 计算增值比（增值时间/总周期时间）
- **数据收集**：
  - 周期时间（Cycle Time）
  - 换型时间（Changeover Time）
  - 正常运行时间（Uptime）
  - 库存水平（WIP）
- **浪费可视化**：
  - 标注等待时间
  - 显示库存堆积点
  - 识别返工和返修

---

### Step 3: 八大浪费识别

- **过量生产浪费（Overproduction）**：
  - 生产早于需求
  - 生产多于需求
  - 最大浪费，隐藏其他浪费
- **等待浪费（Waiting）**：
  - 人员等待设备/物料
  - 设备等待任务
  - 信息等待审批
- **搬运浪费（Transportation）**：
  - 不必要的物料移动
  - 长距离搬运
  - 多次搬运
- **过度加工浪费（Over-processing）**：
  - 超出客户需求的加工
  - 不必要的精度
  - 重复检查
- **库存浪费（Inventory）**：
  - 原材料库存
  - 在制品库存
  - 成品库存
- **动作浪费（Motion）**：
  - 不必要的人员动作
  - 寻找工具/物料
  - 不良布局导致的动作
- **不良品浪费（Defects）**：
  - 返工和返修
  - 报废
  - 质量检查成本
- **人才浪费（Unused Talent）**：
  - 未利用员工智慧
  - 缺乏培训
  - 不参与改善

---

### Step 4: 浪费根因分析

- **5Why分析**：
  - 针对每种浪费追问根因
  - 区分表面原因和深层原因
  - 找到系统性问题
- **系统性因素识别**：
  - 批量生产思维
  - 职能部门壁垒
  - 预测驱动而非需求拉动
  - 缺乏标准化
- **浪费关联分析**：
  - 过量生产导致库存
  - 库存掩盖问题
  - 批量导致等待

---

### Step 5: 消除浪费对策制定

- **流动化（Flow）**：
  - 单件流（One-piece Flow）
  - 小批量生产
  - 连续流布局
- **拉动化（Pull）**：
  - 看板系统（Kanban）
  - 准时化（JIT）
  - 按需生产
- **均衡化（Heijunka）**：
  - 生产平准化
  - 混线生产
  - 减少波动
- **自动化（Jidoka）**：
  - 自动停机（Andon）
  - 防错（Poka-Yoke）
  - 源头质量控制
- **标准化（Standardization）**：
  - 标准作业程序
  - 作业指导书
  - 最佳实践固化

---

### Step 6: 未来状态设计

- **未来状态图绘制**：
  - 基于消除浪费的理想流程
  - 标注改进后的指标
  - 显示流动和拉动机制
- **改进优先级排序**：
  - 影响-难度矩阵
  - 快速见效 vs 长期改进
  - 资源投入与收益平衡
- **实施路线图**：
  - 短期（0-3个月）
  - 中期（3-12个月）
  - 长期（1-3年）

---

### Step 7: 实施与持续改进

- **试点实施**：
  - 选择试点区域
  - 快速验证效果
  - 收集反馈调整
- **标准化与推广**：
  - 将成功经验标准化
  - 横向展开到其他区域
  - 建立维持机制
- **持续改善**：
  - 定期价值流分析
  - 建立浪费识别机制
  - 培养全员改善文化

---

### Step 8: 总结输出

- 提供价值流现状分析
- 列出识别的八大浪费及根因
- 给出消除浪费对策（流动、拉动、均衡、自动化）
- 绘制未来状态价值流图
- 制定实施路线图
- 说明预期收益和维持机制

---

## 关键原则

1. **价值由客户定义**：只有客户愿意付费的活动才是增值。原因：内部视角容易误判价值，客户视角是终极标准。

2. **流动是理想状态**：价值应该连续流动，无中断、无等待。原因：中断和等待产生浪费，流动最大化效率。

3. **拉动优于推动**：根据实际需求生产，而非预测推动。原因：预测必然有误差，拉动减少过量生产和库存。

4. **暴露问题而非隐藏**：库存是问题的藏身之处，减少库存暴露问题。原因：只有暴露问题才能解决问题，持续改进。

5. **全员参与持续改善**：一线员工最了解浪费，全员参与释放智慧。原因：改善是每个人的责任，非专家专属。

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
- [ ] 考虑了二阶/三阶效应（如消除浪费对质量的影响）
- [ ] 输出具体可执行，不含模糊建议
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [kaizen](../thinking/kaizen/SKILL.md) | 核心 | 改善是消除浪费的持续过程 |
| [six-sigma](../thinking/six-sigma/SKILL.md) | 并行 | 六西格玛降低变异，精益消除浪费 |
| [just-in-time](../thinking/just-in-time/SKILL.md) | 后置 | JIT是实现流动和拉动的具体方法 |
| [value-stream-mapping](../thinking/value-stream-mapping/SKILL.md) | 前置 | VSM是识别浪费的工具 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 精益消除浪费案例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Womack, J.P., & Jones, D.T. (1996). *Lean Thinking: Banish Waste and Create Wealth in Your Corporation*. Free Press.
2. Ohno, T. (1988). *Toyota Production System: Beyond Large-Scale Production*. Productivity Press.
3. Rother, M., & Shook, J. (2003). *Learning to See: Value Stream Mapping to Add Value and Eliminate Muda*. Lean Enterprise Institute.
4. Kaizen.com. (2024). *Muda, Mura, Muri*.
5. Learn QC Tools. (2024). *The 8 Wastes of Lean Manufacturing & How to Eliminate Them*.
