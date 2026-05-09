---
name: five-whys
description: |
  触发：当需要找到问题的根本原因、分析故障根因、追溯问题源头时调用；常见信号包括"为什么会这样"、"问题出在哪"、"找到根因"、"连续追问为什么"。
  不触发：当仅需表面症状修复、不涉及深层原因追溯、不需要系统性根因分析时，不要调用此 Skill。
  Invoke when finding root causes of problems, analyzing failure origins, or tracing problem sources through continuous why questions.
  Do NOT invoke when only surface symptom fixing is needed, or when no deep cause tracing is required.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["root-cause-analysis", "inverse-thinking", "causal-thinking"]
---

# 连续追问5个为什么

## 核心定义

通过连续追问找到问题的根本原因，而非停留在表面症状。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充因果链信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点
- **提前终止**：若某步已找到可行动的根本原因（通常3-5个为什么），可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 定义表面症状

- 要点1：清晰描述观察到的问题现象（什么、何时、何地、影响范围）
- 要点2：区分症状和原因（症状是可见的，原因是隐藏的）
- 要点3：避免在第一步就跳入原因分析，先充分理解症状

---

### Step 2: 第一次追问——直接原因

- 要点1：问"为什么会出现这个症状？"找到最直接的原因
- 要点2：验证因果关系的合理性（A确实导致B吗？）
- 要点3：注意不要跳过中间环节，保持因果链完整

---

### Step 3: 连续追问——深层原因

- 要点1：对每个原因继续问"为什么"，深入3-5层
- 要点2：区分系统性原因和人为原因（系统原因更可持续修复）
- 要点3：避免归咎于个人，聚焦流程和系统缺陷

---

### Step 4: 识别根本原因

- 要点1：当原因指向可修复的系统/流程缺陷时，停止追问
- 要点2：验证根本原因：修复它是否能防止问题复发？
- 要点3：标注置信度，识别可能的其他因果路径

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步

---

## 关键原则

1. **聚焦系统而非个人**：说明。原因：人为原因是表面原因，系统原因才是根本。修复系统比指责个人更有效。
2. **因果链必须可验证**：说明。原因：每个"为什么"的答案必须有证据支持，不能是猜测。
3. **5不是绝对数字**：说明。原因：有时3个为什么就找到根因，有时需要7个。关键是找到可行动的根因。

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
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

**五问法特有关键检查项**：

- [ ] **五问法特供**：是否清晰区分了症状与原因？第一步是否仅描述现象，未过早跳入原因分析？
- [ ] **五问法特供**：每个"为什么"的答案是否有证据支持？因果链中的每个环节是否可验证，而非猜测？
- [ ] **五问法特供**：是否避免了归咎个人？分析是否聚焦于系统缺陷、流程漏洞和机制问题，而非"某人犯了错"？
- [ ] **五问法特供**：追问深度是否合适？是否停留在表面原因（3层以内），或过度追问至不可行动的抽象层面（7层以上）？
- [ ] **五问法特供**：找到的根本原因是否可行动？修复该根因是否能防止问题复发？是否标注了置信度？
- [ ] **五问法特供**：是否识别了多条因果路径？问题是否可能由多个独立原因共同导致？是否考虑了单一因果谬误？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [root-cause-analysis](../thinking/root-cause-analysis/SKILL.md) | 并行 | 更系统的根因分析方法 |
| [causal-thinking](../thinking/causal-thinking/SKILL.md) | 前置 | 区分相关性和因果性 |
| [inverse-thinking](../thinking/inverse-thinking/SKILL.md) | 后置 | 从根因设计预防措施 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Ohno, T. (1988). *Toyota Production System: Beyond Large-Scale Production*. Productivity Press.
2. Rother, M., & Shook, J. (1999). *Learning to See: Value Stream Mapping to Add Value and Eliminate Waste*. Lean Enterprise Institute.
3. Andersen, B., & Fagerhaug, T. (2006). *Root Cause Analysis: Simplified Tools and Techniques*. ASQ Quality Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
