---
name: curse-of-knowledge
description: |
  触发：当需要评估沟通是否受知识诅咒影响、需要识别"这很简单你肯定懂"偏差、需要优化专家-新手沟通时调用；常见信号包括"这很明显"、"不用说你也懂"、"这么简单怎么不会"。
  不触发：当只需描述知识水平、无需分析沟通效果时；当听众确实具备相同背景知识时（经测试验证）；当只需记录信息、无需评估理解度时。
  Invoke when needing to evaluate whether communication is affected by curse of knowledge, identify "this is obvious you must know" bias, or optimize expert-novice communication.
  Do NOT invoke when only describing knowledge levels without analyzing communication effectiveness, when audience truly has same background knowledge (verified by testing), or when only recording information without evaluating comprehension.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["dunning-kruger-effect", "hindsight-bias", "false-consensus-effect", "empathy-gap"]
---

# 知识诅咒思维（Curse of Knowledge Thinking）

## 核心定义

专家难以想象不知道某事的状态，导致沟通障碍。Camererer等人在1989年提出：一旦知道某事，就很难想象不知道的状态。这使专家高估听众理解力，使用行话、跳过步骤、假设背景知识。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充听众背景知识、理解测试反馈和沟通效果数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别知识诅咒影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别诅咒信号

- 是否出现"这很明显"、"不用说你也懂"、"这么简单怎么不会"等表述？
- 是否使用行话而不解释？
- 是否跳过"显而易见"的步骤？
- 是否假设听众有相同背景知识？

---

### Step 2: 评估知识差距

- 专家知道什么？（概念、术语、背景）
- 听众知道什么？（实际水平）
- 知识差距在哪里？（概念、术语、背景）
- 听众可能误解什么？

---

### Step 3: 分析沟通障碍

- 行话使用频率和必要性
- 跳过的步骤是否真的明显？
- 假设的背景知识是否存在？
- 听众反馈：困惑、沉默、错误理解

---

### Step 4: 校正知识诅咒

- 新手测试：让真正新手试用沟通内容
- 术语表：解释所有专业术语
- 步骤完整：不跳过任何步骤
- 反馈循环：定期检查理解度

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **知道后无法忘记**：一旦知道某事，就很难想象不知道的状态。原因：知识改变认知结构，无法"卸载"已知信息，导致高估他人理解力。
2. **行话是障碍**：专业术语对专家是捷径，对新手是障碍。原因：行话压缩信息，新手缺乏解码能力，导致沟通失败。
3. **明显是相对的**：专家觉得明显的，新手可能完全不懂。原因：专家经过长期学习形成直觉，新手缺乏基础，"明显"不共享。
4. **新手测试是解药**：让真正新手试用沟通内容。原因：新手提供真实反馈，识别知识盲点，校正专家假设。

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
- [ ] **知识诅咒特供**：是否识别了知识诅咒信号？是否出现"这很明显"、"不用说你也懂"等表述？是否使用行话而不解释？
- [ ] **知识诅咒特供**：是否评估了知识差距？专家知道什么 vs 听众知道什么？知识差距在概念、术语、背景哪个层面？
- [ ] **知识诅咒特供**：是否分析了沟通障碍？行话使用频率和必要性是否被评估？跳过的步骤是否真的明显？听众反馈（困惑、沉默）是否被收集？
- [ ] **知识诅咒特供**：是否使用新手测试校正？是否让真正新手试用沟通内容？是否根据反馈调整了解释深度？
- [ ] **知识诅咒特供**：是否解释了所有术语和步骤？是否提供了术语表？是否确保步骤完整无跳过？是否建立了反馈循环定期检查理解度？
- [ ] 输出具体可执行，不含模糊建议（如"简单说明"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [dunning-kruger-effect](../thinking/dunning-kruger-effect/SKILL.md) | 并行 | 达克效应使新手高估自己，知识诅咒使专家高估听众 |
| [hindsight-bias](../thinking/hindsight-bias/SKILL.md) | 并行 | 后见之明使结果看起来可预测，知识诅咒使知识看起来明显 |
| [false-consensus-effect](../thinking/false-consensus-effect/SKILL.md) | 并行 | 错误共识效应假设他人与自己相同 |
| [empathy-gap](../thinking/empathy-gap/SKILL.md) | 并行 | 共情差距使预测他人理解困难 |

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

1. Camerer, C., Loewenstein, G., & Weber, M. (1989). The curse of knowledge in economic settings: An experimental analysis. *Journal of Political Economy*, 97(5), 1232-1254.
2. Birch, S. A., & Bloom, P. (2007). The curse of knowledge in reasoning about false beliefs. *Psychological Science*, 18(5), 382-386.
3. Heath, C., & Heath, D. (2007). *Made to Stick: Why Some Ideas Survive and Others Die*. Random House.
4. Keysar, B., Lin, S., & Barr, D. J. (2003). Limits on theory of mind use in adults. *Cognition*, 89(1), 25-41.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
