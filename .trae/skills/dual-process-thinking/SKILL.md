---
name: dual-process-thinking
description: |
  触发：当需要评估决策是否受认知偏差影响、需要区分直觉和理性判断、需要设计防偏差机制时调用；常见信号包括"我是不是太冲动了"、"这个判断是凭感觉还是凭数据"、"有没有认知偏差在影响我"。
  不触发：当决策基于明确数据和逻辑推导时；当只需执行已验证的标准化流程时；当时间极紧迫、必须依赖直觉时。
  Invoke when needing to evaluate whether decisions are affected by cognitive biases, distinguish intuitive from rational judgment, or design anti-bias mechanisms.
  Do NOT invoke when decisions are based on clear data and logical reasoning, when only executing validated standardized processes, or when time is extremely tight and intuition must be relied upon.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["confirmation-bias", "anchoring-effect", "critical-thinking", "probabilistic-thinking"]
---

# 双过程思维（Dual Process Thinking）

## 核心定义

识别并管理两种思维模式：系统1（快速、直觉、自动）和系统2（慢速、理性、费力），在适当场景调用适当系统，并防止系统1的认知偏差影响重要决策。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充决策背景、时间压力和可用数据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已明确判断应由系统2主导且切换机制清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别当前思维模式

- 当前判断是直觉反应（系统1）还是理性分析（系统2）？
- 判断信号：是否感到轻松确定（系统1）还是感到费力思考（系统2）？
- 评估决策重要性：这个决策的影响有多大？
- 如果决策重要但当前是系统1主导，必须切换到系统2

---

### Step 2: 评估系统1的适用性

- 当前场景是否适合依赖直觉？
- 系统1适用的条件：高规律性环境 + 长期练习 + 即时反馈
- 国际象棋大师的直觉可靠，但股票预测的直觉不可靠（环境规律性不同）
- 如果环境不规律或缺乏练习，系统1的判断不可信

---

### Step 3: 识别认知偏差

- 检查常见偏差：确认偏误、锚定效应、可得性偏差、过度自信、损失厌恶
- 哪些偏差可能影响当前判断？
- 偏差是否被情绪放大？（愤怒、恐惧、兴奋都会增强偏差）
- 标注每个偏差的影响方向和程度

---

### Step 4: 激活系统2校正

- 针对识别的偏差，设计校正机制
- 校正方法：外部视角（基准数据）、预验尸分析、魔鬼代言人、决策清单
- 强制系统2介入：延迟决策、写下推理过程、寻求独立第二意见
- 评估校正后的判断与初始直觉的差异

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **系统1不是敌人**：在适用场景下，直觉比分析更快更准。原因：系统1是进化优化的模式识别引擎，在规律性环境中表现卓越。
2. **知道何时切换是关键**：重要决策必须用系统2，日常决策可以用系统1。原因：系统2消耗认知资源，不能也不应该用于所有决策。
3. **偏差不可消除只能管理**：认知偏差是系统1的固有特性。原因：偏差是启发式思维的副产品，消除偏差等于消除直觉，不现实也不可取。
4. **外部视角是最强校正**：基准数据和独立意见能有效对抗内部视角偏差。原因：内部视角天然乐观，外部视角提供现实校准。

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
- [ ] 是否正确识别了当前主导的思维模式？
- [ ] 系统1适用性评估是否考虑了环境规律性？
- [ ] 认知偏差是否被具体识别（而非泛泛而谈）？
- [ ] 校正机制是否针对具体偏差设计？
- [ ] 是否评估了校正后判断与初始直觉的差异？
- [ ] 输出具体可执行，不含模糊建议（如"理性思考"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误是系统1的典型偏差，双过程思维提供整体框架 |
| [anchoring-effect](../thinking/anchoring-effect/SKILL.md) | 并行 | 锚定效应是系统1的启发式，双过程思维提供校正机制 |
| [critical-thinking](../thinking/critical-thinking/SKILL.md) | 并行 | 批判性思维是系统2的结构化应用 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维提供系统2的量化分析工具 |

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

1. Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux.
2. Stanovich, K. E., & West, R. F. (2000). Individual differences in reasoning: Implications for the rationality debate. *Behavioral and Brain Sciences*, 23(5), 645-665.
3. Evans, J. S. B. (2008). Dual-process accounts of reasoning, judgment, and social cognition. *Annual Review of Psychology*, 59, 255-278.
4. Klein, G. (2009). *Streetlights and Shadows: Searching for the Keys to Adaptive Decision Making*. MIT Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
