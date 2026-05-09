---
name: minimalism-thinking
description: |
  触发：当系统/代码/设计变得臃肿需要精简、当新增功能前需要评估"是否真正必要"、当面对功能蔓延（feature creep）或过度设计时调用；常见信号包括"这个功能能不能砍掉"、"代码太复杂了能不能简化"、"是不是做太多了"、"能不能用更少的东西达到同样效果"。
  不触发：当精简会损害核心功能或安全性时；当简单方案明确无法满足需求时；当"精简"只是审美偏好而非功能需求时；当用户明确要求完整功能时。
  Invoke when a system/code/design becomes bloated and needs trimming, when evaluating whether a new feature is truly necessary, or when facing feature creep or over-engineering.
  Do NOT invoke when trimming would compromise core functionality or safety, when a simple solution clearly cannot meet requirements, when "minimalism" is merely an aesthetic preference, or when users explicitly request full functionality.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["occams-razor", "constraint-thinking", "anti-corrosion", "yagni", "less-is-more"]
---

# 极简思维（Minimalism Thinking）

## 核心定义

通过主动移除不必要的元素来提升质量——"少但是更好"（Less, but better）。不是简单地做少，而是只保留本质，让剩余的部分更精炼、更有力。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充功能的必要性论证
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告"精简"与"功能完整性"的冲突点，等待决策
- **提前终止**：若经评估当前系统已经"恰如其分"——每个元素都必不可少且不可进一步精简，可提前终止并标注"已达到本质最小化"

---

## 思考流程

### Step 1: 列出当前所有元素

- 穷举系统中的所有组件、功能、代码模块、设计元素
- 不预设任何元素"应该存在"，将所有元素放在同等地位审视
- 记录每个元素的来源：为什么被加入？是谁要求的？什么时候加的？
- 警惕"惯性存在"：很多元素之所以存在，只是因为"一直都有"

---

### Step 2: 对每个元素进行必要性评估

- 核心问题：移除这个元素后，系统还能完成核心任务吗？
- 使用"反向测试"：先假设这个元素不存在，然后论证为什么必须加回来
- 对功能：这个功能被多少人使用？使用频率？没有它会有什么影响？
- 对代码：这段代码承担什么职责？是否可以合并到其他地方？是否有更简洁的表达？
- 对设计元素：这个元素传达了什么信息？移除后信息是否仍然完整？
- 区分"核心"（移除后系统失效）、"增强"（移除后体验下降但可用）、"装饰"（移除后无实质影响）

---

### Step 3: 评估移除的代价和风险

- 移除每个非核心元素的直接代价（用户抱怨、数据丢失、兼容性破坏）
- 移除后的替代方案：可以用已有元素替代吗？可以外部化吗？
- 移除的连锁影响：是否会影响其他元素的正常运行？
- 移除的不可逆程度：删除后如果后悔，恢复代价有多大？
- 优先级排序：先移除装饰元素（低风险高收益），再处理增强元素（需谨慎评估）

---

### Step 4: 重新设计"最小必要版本"

- 基于保留的核心元素，重新审视系统架构
- 被保留的元素之间的关系是否可以简化？
- 是否存在"复杂是为了弥补另一个复杂"的循环？（A复杂→B需要弥补A→B复杂→A需要弥补B）
- 核心问题：用更少的元素能否实现同等的本质功能？
- 参考Dieter Rams的第十原则：好的设计是尽量少的设计（Good design is as little design as possible）

---

### Step 5: 建立防止复胖的机制

- 制定"加入标准"：什么条件下才可以向系统加入新元素？
- 每个新增元素必须有明确的移除日期或条件（Chekhov's Gun原则：如果它不是必需的，就应该被移除）
- 定期"春季大扫除"：每个迭代/季度审视一次系统的臃肿程度
- 考核指标不要只奖励"添加"：将"删除代码行数"也作为绩效指标
- 实施YAGNI（You Ain't Gonna Need It）原则：不为"可能用到"而预先添加

---

### Step 6: 总结输出

- 整合前面各步的分析结果
- 输出可以移除的元素清单（按优先级排列）
- 输出精简后系统的"最小必要版本"设计方案
- 明确移除后的风险缓解措施
- 输出应包含：结论 + 移除清单及理由 + 精简方案 + 防复胖机制 + 关键假设 + 风险 + 下一步

---

## 关键原则

1. **精简不是目的，本质是目的**：去除非本质元素是为了让本质更突出。原因：为精简而精简可能走向极简主义的审美极端，失去功能价值——极简思维的目标是"更好"，"更少"只是手段。
2. **加入的代价远高于看起来的**：每增加一个元素，不只是那一个元素的成本，还有它与所有已有元素的交叉复杂度（组合爆炸）。原因：系统的复杂度是O(n²)甚至O(2^n)增长的，不是O(n)。
3. **先证明必要性，再保留**：举证责任应该在"保留方"而非"移除方"。原因：惯性偏见（Status Quo Bias）让我们倾向于保留已有事物，最小主义要求主动举证每个元素的必要性。
4. **减法比加法更需要勇气**：删除已有的东西比拒绝新的东西更难。原因：损失厌恶（Loss Aversion）让我们对移除已有功能感到的痛苦约为新加功能的2倍。
5. **建立防复胖机制重于一次性精简**：没有防护机制的系统必然会重新膨胀。原因：熵增定律——封闭系统自发趋向混乱，信息系统自发趋向复杂化（软件熵/技术债务），需要持续的能量输入来维持秩序。

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
- [ ] 所有元素是否被列出？是否排除了惯性存在？
- [ ] 每个元素的必要性是否被逐项评估？核心/增强/装饰是否被分类？
- [ ] "反向测试"是否被应用于每个待移除元素？
- [ ] 移除的连锁影响是否被完整评估？
- [ ] "最小必要版本"是否仍然满足核心功能？
- [ ] 是否避免了"为了精简而精简"——削减了不该削减的核心功能？
- [ ] 防复胖机制是否被设计？是否有新增元素的门禁标准？
- [ ] 输出具体可执行，不含模糊建议（如"简化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [occams-razor](../occams-razor/SKILL.md) | 互补 | 奥卡姆剃刀在理论层面精简假设/实体，极简思维在实践层面精简功能/代码 |
| [constraint-thinking](../constraint-thinking/SKILL.md) | 前置 | 约束思维设定外部限制条件，极简思维在此基础上主动移除内部冗余 |
| [anti-corrosion](../anti-corrosion/SKILL.md) | 后置 | 极简思维大扫除后，反腐蚀防止系统重新腐化 |
| [paradox-thinking](../paradox-thinking/SKILL.md) | 互补 | 精简和完整有时是悖论——极简思维处理如何少，悖论思维处理如何在两者间整合 |
| [entropy](../entropy/SKILL.md) | 前置 | 熵增思维解释为什么系统必然趋于复杂，极简思维提供对抗复杂化的方法 |

---

## 参考资料（按需加载）

> **参考资料** = 本 Skill 资源文件夹内的文件，包含示例和陷阱。

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

> 外部学术来源，用于追溯思维模型的理论根基。

1. Rams, D. (1995). *Less but Better*. Gestalten. (Dieter Rams的设计哲学："少但是更好")
2. McKeown, G. (2014). *Essentialism: The Disciplined Pursuit of Less*. Crown Business.
3. Kondo, M. (2014). *The Life-Changing Magic of Tidying Up*. Ten Speed Press. (极简生活方法论：只保留"激起喜悦"的事物)
4. Hunt, A., & Thomas, D. (1999). *The Pragmatic Programmer*. Addison-Wesley. (YAGNI, DRY等软件开发极简原则的来源)
5. Beck, K. (2004). *Extreme Programming Explained* (2nd ed.). Addison-Wesley. (XP方法中的YAGNI：You Ain't Gonna Need It)
6. Norman, D. A. (2013). *The Design of Everyday Things* (Revised ed.). Basic Books. ("好的设计实际上是尽可能少的设计")

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
