---
name: fundamental-attribution-error
description: |
  触发：当需要评估对他人行为的归因是否过度归因于性格、需要识别情境因素影响、需要纠正人际判断偏差时调用；常见信号包括"他就是这种人"、"她性格有问题"、"这人能力不行"。
  不触发：当只需描述行为、无需归因时；当情境因素确实不影响行为时（经实验验证）；当分析自己行为时（自我服务偏差更相关）。
  Invoke when needing to evaluate whether attributions of others' behavior overemphasize personality, identify situational factors, or correct interpersonal judgment bias.
  Do NOT invoke when only describing behavior without attribution, when situational factors truly do not affect behavior (experimentally verified), or when analyzing one's own behavior (self-serving bias is more relevant).
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["confirmation-bias", "self-serving-bias", "empathy", "systems-thinking"]
---

# 基本归因错误思维（Fundamental Attribution Error Thinking）

## 核心定义

人们倾向于将他人的行为归因于性格特质，忽视情境因素。Ross在1977年提出：观察者高估性格因素、低估情境因素对行为的影响。经典实验：即使知道演讲者是被分配立场，听众仍认为演讲内容反映演讲者真实观点。对自己行为则相反：归因于情境。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充情境因素、历史行为数据和外部视角
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别基本归因错误影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别归因信号

- 是否出现"他就是这种人"、"她性格有问题"、"这人能力不行"等表述？
- 是否将行为归因于性格而非情境？
- 是否考虑了情境压力、角色要求、外部约束？
- 是否对同样行为，对自己和他人有不同归因？

---

### Step 2: 评估情境因素

- 行为发生时的情境是什么？
- 情境压力有多大？（时间压力、社会压力、资源约束）
- 角色要求是什么？（职位要求、社会期望）
- 外部约束有哪些？（规则、资源、信息限制）

---

### Step 3: 分析归因偏差

- 观察者偏差：看到行为，看不到情境
- 性格归因更简单：性格解释比情境解释更省力
- 文化因素：个人主义文化更倾向性格归因
- 自我服务偏差：对自己归因于情境，对他人归因于性格

---

### Step 4: 校正归因

- 使用情境视角：如果我在同样情境下会怎样？
- 考虑角色要求：行为是否由角色驱动？
- 寻找历史模式：此人在不同情境下行为一致吗？
- 平衡归因：性格和情境各占多少权重？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **行为是性格×情境**：任何行为都是性格和情境的交互结果。原因：同样性格的人在不同情境下行为不同，同样情境下不同性格的人行为也不同。
2. **观察者看不到情境**：观察者看到行为，但看不到行为者面临的情境压力。原因：情境往往不可见，行为显而易见，大脑依赖可见信息。
3. **角色驱动行为**：社会角色和职位要求强烈影响行为。原因：角色提供行为脚本，人们按角色期望行动，不一定反映性格。
4. **换位思考校正偏差**：问"如果我在同样情境下会怎样？"。原因：这个问题激活情境视角，减少性格归因偏差。

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
- [ ] 是否识别了归因信号？
- [ ] 是否评估了情境因素？
- [ ] 是否分析了归因偏差？
- [ ] 是否使用情境视角校正？
- [ ] 是否考虑了角色要求？
- [ ] 输出具体可执行，不含模糊建议（如"客观看待"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误寻找支持性格归因的证据 |
| [self-serving-bias](../thinking/self-serving-bias/SKILL.md) | 并行 | 自我服务偏差解释为何对自己和他人有不同归因 |
| [empathy](../thinking/empathy/SKILL.md) | 前置 | 共情帮助理解他人情境和感受 |
| [systems-thinking](../thinking/systems-thinking/SKILL.md) | 前置 | 系统思维提供情境分析框架 |

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

1. Ross, L. (1977). The intuitive psychologist and his shortcomings: Distortions in the attribution process. *Advances in Experimental Social Psychology*, 10, 173-220.
2. Jones, E. E., & Harris, V. A. (1967). The attribution of attitudes. *Journal of Experimental Social Psychology*, 3(1), 1-24.
3. Gilbert, D. T., & Malone, P. S. (1995). The correspondence bias. *Psychological Bulletin*, 117(1), 21-38.
4. Nisbett, R. E. (2003). *The Geography of Thought: How Asians and Westerners Think Differently... and Why*. Free Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
