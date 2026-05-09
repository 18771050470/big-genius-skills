---
name: authority-bias
description: |
  触发：当需要评估判断是否受权威身份影响、需要识别"专家说的肯定对"偏差、需要独立评估论点质量时调用；常见信号包括"专家说的"、"权威机构认证"、"诺贝尔奖得主推荐"。
  不触发：当只需引用权威、无需评估论点质量时；当权威确实提供可靠信息时（经独立验证）；当只需记录来源、无需分析偏差时。
  Invoke when needing to evaluate whether judgments are affected by authority status, identify "expert must be right" bias, or independently assess argument quality.
  Do NOT invoke when only citing authority without evaluating argument quality, when authority truly provides reliable information (verified by independent validation), or when only recording sources without analyzing bias.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["halo-effect", "confirmation-bias", "bandwagon-effect", "critical-thinking"]
---

# 权威偏差思维（Authority Bias Thinking）

## 核心定义

人们因信息来源是权威而接受，而非评估论点质量。Milgram在1963年服从实验证明：65%参与者因权威指令而电击他人。权威身份使论点被不加批判地接受。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充论点独立评估数据、权威领域相关性和反面证据
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别权威偏差影响且校正方案清晰，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 识别权威信号

- 是否出现"专家说的"、"权威机构认证"、"诺贝尔奖得主推荐"等表述？
- 是否因权威身份而接受论点？
- 是否独立评估过论点质量？
- 是否忽视反面证据？

---

### Step 2: 评估权威相关性

- 权威是否在相关领域？（跨领域权威无效）
- 权威是否有利益冲突？（资助、立场）
- 权威观点是否有证据支持？
- 权威观点是否被同行认可？

---

### Step 3: 分析权威机制

- 服从倾向：进化使服从权威提高生存率
- 认知捷径：权威身份替代论点评估
- 社会压力：质疑权威面临社会成本
- 信任转移：对机构的信任转移到论点

---

### Step 4: 校正权威偏差

- 论点独立评估：不看来源，只评估内容
- 领域相关性：权威是否相关领域？
- 利益冲突检查：是否有动机偏差？
- 同行共识：其他专家是否同意？

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **权威≠正确**：权威身份不保证论点正确。原因：权威可能犯错、有利益冲突、或跨领域发言，论点质量需独立评估。
2. **领域相关性关键**：只在相关领域权威有效。原因：诺贝尔物理奖得主谈营养学，权威性为零，领域不匹配。
3. **服从倾向强大**：人们难以质疑权威。原因：进化和社会化使服从权威成为默认反应，质疑需要认知努力。
4. **独立评估是解药**：不看来源，只评估内容。原因：独立评估基于论点和证据，不受权威身份影响。

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
- [ ] **权威偏差特供**：是否识别了"专家说的"、"权威机构认证"等权威偏差信号？是否区分了引用权威和盲信权威？
- [ ] **权威偏差特供**：是否评估了权威的领域相关性？跨领域权威是否被正确识别并降权？
- [ ] **权威偏差特供**：是否检查了权威的利益冲突（资助、立场、声誉绑定）？利益冲突是否被量化影响？
- [ ] **权威偏差特供**：是否实施了"盲评"操作？即不看来源、只评估论点内容和证据质量？
- [ ] **权威偏差特供**：是否验证了同行共识？单一权威观点 vs 领域共识之间是否存在显著分歧？
- [ ] **权威偏差特供**：是否分析了服从倾向的社会成本？质疑权威是否面临隐性惩罚？
- [ ] 考虑了二阶/三阶效应（如果适用）
- [ ] 输出具体可执行，不含模糊建议（如"质疑权威"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [halo-effect](../thinking/halo-effect/SKILL.md) | 并行 | 晕轮效应使权威身份扩散到论点评价 |
| [confirmation-bias](../thinking/confirmation-bias/SKILL.md) | 并行 | 确认偏误使寻找支持权威的证据 |
| [bandwagon-effect](../thinking/bandwagon-effect/SKILL.md) | 并行 | 从众效应使跟随权威观点 |
| [critical-thinking](../thinking/critical-thinking/SKILL.md) | 前置 | 批判性思维提供权威偏差的校正方法 |

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

1. Milgram, S. (1963). Behavioral study of obedience. *Journal of Abnormal and Social Psychology*, 67(4), 371-378.
2. Cialdini, R. B. (2001). The science of persuasion. *Scientific American*, 284(2), 76-81.
3. Henrich, J., & Gil-White, F. J. (2001). The evolution of prestige: Freely conferred deference as a mechanism for enhancing the benefits of cultural transmission. *Evolution and Human Behavior*, 22(3), 169-196.
4. Landemore, H. (2013). *Democratic Reason: Politics, Collective Intelligence, and the Rule of the Many*. Princeton University Press.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
