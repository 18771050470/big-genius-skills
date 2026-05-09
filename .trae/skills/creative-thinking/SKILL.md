---
name: creative-thinking
description: |
  触发：当需要产生新颖想法、突破常规方案、解决前所未见的问题、团队思维僵化、或明确要求头脑风暴时调用。常见信号包括"需要创新方案"、"现有方法失效"、"从0到1构建"、"如何差异化"。
  不触发：当已有成熟标准解且只需执行时；当时间极短需要立即行动时；当场景要求严格合规不允许偏离标准流程时；当问题为纯事实性查询时。
  Invoke when needing novel ideas, breakthrough solutions, or facing unprecedented problems. Do NOT invoke when standard solutions exist and only execution is needed; when time is extremely limited requiring immediate action; when the scenario requires strict compliance without deviation; when the problem is a purely factual query.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["analogical-thinking", "lateral-thinking", "first-principles", "design-thinking"]
---

# 创造性思维 Creative Thinking

## 核心定义

创造性思维是一种通过打破常规联想路径，运用重组、跨界、变异等方法产生新颖想法，并在发散与收敛之间交替迭代的底层认知思维模型。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若某步已得出明确结论且后续步骤无增量价值，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

本流程体现发散与收敛的交替运用，共6步。

### Step 1: 定义问题与边界（收敛）

- 准确描述问题，明确约束条件（时间、资源、技术、用户等），设定创新目标（如"生成至少10个可行的方案"）
- 清晰的问题陈述文档（含约束清单和目标）

### Step 2: 打破常规联想（发散）

- 采用以下任意组合方法：
  - **重组**：将现有元素重新排列组合
  - **跨界**：引入其他领域的概念、技术或模式
  - **变异**：对现有方案进行夸张、缩小、替代等变异操作
  - **反向**：从相反方向思考
  - **随机**：随机挑选关联词进行强制联想
- 一个或多个思路方向（记录每一条）

### Step 3: 大量生成想法（发散）

- 在每一个方向下快速生成想法，不评判、不筛选，追求数量。可以使用亲和图、头脑书写等方法
- 至少20个原始想法（可以是关键词、句子或草图）

### Step 4: 初步筛选与分类（收敛）

- 根据可行性（技术/时间）、新颖性（相比现有方案）、价值性（用户/商业）进行初步评分
- 将想法分组归类（如"直接可用"、"需要组合"、"未来可能"）
- 保留每组中评分最高的前3-5个
- 筛选后的候选想法（约5-10个）

### Step 5: 深化与组合（发散+收敛交替）

- 对每个候选想法进行扩展（发散）：补充细节、考虑实现路径、预测效果
- 尝试将不同候选想法组合（发散）：产生新的混合方案
- 快速评估组合方案（收敛）：比较优劣，选择1-2个最具潜力者
- 深化后的2-3个完整方案草稿

### Step 6: 最终评估与确定（收敛）

- 建立评估标准（如：创新程度、可行性、投入产出比、风险）
- 对每个方案进行全面评估
- 选择最终方案，并制定实施路线图
- 选定方案（含理由）及初步实施计划

## 关键原则

### 原则1：数量先于质量（Quantity before Quality）
**原因**：创造性思维的早期阶段，数量是孕育质量的条件。大量想法增加了找到突破性方案的概率，且早期评判会抑制想法产生。

### 原则2：跨界借鉴（Cross-domain Borrowing）
**原因**：跨领域类比是创新的主要来源之一。将看似无关领域的原理、模式或技术引入当前问题，往往能产生意想不到的解决方案。

### 原则3：延迟评判（Defer Judgment）
**原因**：在发散阶段过早评判会扼杀创新。一个看似荒谬的想法可能成为灵感火花，或与其他想法组合产生价值。

### 原则4：明确交替节奏（Explicit Alternation Rhythm）
**原因**：发散和收敛是完全不同的思维状态，混在一起会导致既没有充分发散又没有有效收敛。明确分离二者能让每种状态发挥最大效果。

### 原则5：安全试错环境（Safe-to-fail Environment）
**原因**：创造本质是探索未知，失败是必经之路。只有不被惩罚的失败，才会鼓励冒险尝试和真正颠覆性创新。

## 自检清单

> 聚焦创造性思维最容易被误用的环节

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**创造性思维特有关键检查项**：

- [ ] **发散阶段是否真正做到了延迟评判？** 是否在生成想法时过早排除了"荒谬"的选项？
- [ ] **是否尝试了至少两种打破常规的方法？** （重组、跨界、变异、反向、随机刺激）
- [ ] **跨界借鉴时是否检查了类比源与目标的核心差异？** 避免生搬硬套
- [ ] **收敛阶段的筛选标准是否明确且量化？** 还是凭直觉筛选？
- [ ] **是否尝试过将看似不相关的想法进行组合？** 组合往往是突破性创新的来源
- [ ] **最终方案是否经过"反向假设"检验？** 即：如果完全相反的做法会怎样？

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [first-principles](../thinking/first-principles/SKILL.md) | 前置 | 分解问题至最基础元素，为跨界重组提供原材料 |
| [analogical-thinking](../thinking/analogical-thinking/SKILL.md) | 并行 | 在跨界借鉴时提供系统化的类比推理方法 |
| [lateral-thinking](../thinking/lateral-thinking/SKILL.md) | 并行 | 提供打破思维定式的具体技巧（如挑战假设、随机刺激） |
| [design-thinking](../thinking/design-thinking/SKILL.md) | 后置 | 将创新想法转化为以用户为中心的验证和迭代流程 |

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Guilford, J. P. (1950). Creativity. *American Psychologist*, 5(9), 444-454.
2. Osborn, A. F. (1953). *Applied Imagination*. Scribner.
3. Runco, M. A., & Jaeger, G. J. (2012). The standard definition of creativity. *Creativity Research Journal*, 24(1), 92-96.
4. Csikszentmihalyi, M. (1996). *Creativity: Flow and the Psychology of Discovery and Invention*. HarperCollins.

---
