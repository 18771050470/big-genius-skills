---
name: red-team-thinking
description: |
  触发：当需要主动发现系统漏洞、验证安全方案有效性、模拟攻击者视角时调用；常见信号包括"有没有我们没想到的攻击路径"、"这个方案能不能被绕过"、"最坏情况下会怎样"。
  不触发：当只需正向验证功能正常时；当系统处于早期原型阶段、尚未需要安全审查时；当攻击面极小、风险可忽略时。
  Invoke when proactively discovering system vulnerabilities, validating security方案 effectiveness, or simulating attacker perspectives.
  Do NOT invoke when only forward validation of normal functionality is needed, when the system is in early prototype stage not yet requiring security review, or when the attack surface is minimal and risk is negligible.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["inverse-thinking", "boundary-thinking", "second-order-thinking", "probabilistic-thinking"]
---

# 红队思维（Red Team Thinking）

## 核心定义

以攻击者视角主动寻找系统弱点，模拟真实威胁场景，验证防御体系的有效性。核心信念：最好的防御是理解攻击。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统架构、信任边界或已知威胁信息
- **发现矛盾**：停止思考，用 AskUserQuestion 向用户报告矛盾点，等待决策
- **提前终止**：若已识别出关键攻击路径且修复方案明确，可提前进入总结输出，但须标注"提前终止，跳过 Step N+1"

---

## 思考流程

### Step 1: 定义攻击面

- 列出系统的所有暴露面：API、UI、网络端口、物理接口、供应链
- 识别信任边界：系统内外部的信任分界线
- 标注高价值目标：攻击者最想要获取的数据或能力
- 绘制攻击面地图，标注每个入口的暴露程度

---

### Step 2: 构建威胁模型

- 识别潜在攻击者类型：脚本小子、有组织的犯罪团伙、国家支持、内部人员
- 评估每种攻击者的能力、动机和资源
- 使用 STRIDE 框架分类威胁：Spoofing、Tampering、Repudiation、Information Disclosure、DoS、Elevation of Privilege
- 标注每个威胁的严重等级和可能性

---

### Step 3: 模拟攻击路径

- 从每个攻击面入口出发，构建到达高价值目标的完整路径
- 考虑组合攻击：单个漏洞无害，但组合起来可造成重大损害
- 模拟攻击者的决策树：如果防御A生效，攻击者会尝试B还是C
- 标注每条路径的难度、检测概率和影响程度

---

### Step 4: 评估防御有效性

- 现有防御能否检测或阻止每条攻击路径？
- 防御是否存在单点故障？绕过一个防御是否就完全暴露？
- 评估纵深防御：多层防御是否真正独立？
- 识别检测盲区：哪些攻击行为不会被监控到

---

### Step 5: 总结输出

- 整合前面各步的分析结果，形成完整结论
- 不遗漏关键发现、核心假设和重大风险
- 明确下一步应该调用哪个 Skill（如果需要）
- 输出应包含：结论 + 建议 + 假设 + 风险 + 下一步
- 不规定输出格式，由调用方或 [structured-output](../../tools/structured-output/SKILL.md) 决定如何呈现

---

## 关键原则

1. **攻击者不遵守规则**：不要假设攻击者会按预期使用系统。原因：防御方常犯的错误是基于"正常用户行为"设计安全策略。
2. **最弱链决定安全性**：系统安全性取决于最薄弱的环节。原因：攻击者会选择阻力最小的路径，而非正面攻击最强防御。
3. **纵深防御必须独立**：多层防御如果共享相同弱点，等于单层。原因：一个漏洞可能同时绕过所有依赖相同假设的防御层。
4. **检测与阻止同等重要**：无法阻止所有攻击，但必须检测到所有攻击。原因：快速响应可以将损失降到最低。

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
- [ ] 攻击面是否完整识别？是否有遗漏的暴露面？
- [ ] 威胁模型是否覆盖内部和外部攻击者？
- [ ] 攻击路径是否考虑了组合攻击？
- [ ] 防御评估是否识别了检测盲区？
- [ ] 是否验证了纵深防御的独立性？
- [ ] 输出具体可执行，不含模糊建议（如"加强安全"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [inverse-thinking](../thinking/inverse-thinking/SKILL.md) | 并行 | 逆向思维提供"如何失败"的视角，红队思维提供结构化攻击模拟 |
| [boundary-thinking](../thinking/boundary-thinking/SKILL.md) | 前置 | 边界思维识别信任边界，红队思维在边界上寻找突破口 |
| [second-order-thinking](../thinking/second-order-thinking/SKILL.md) | 并行 | 二阶思维评估修复方案的间接后果，红队思维评估修复是否引入新漏洞 |
| [probabilistic-thinking](../thinking/probabilistic-thinking/SKILL.md) | 并行 | 概率思维量化攻击成功率和检测率 |

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

1. Shostack, A. (2014). *Threat Modeling: Designing for Security*. Wiley.
2. Howard, M., & LeBlanc, D. (2003). *Writing Secure Code* (2nd ed.). Microsoft Press.
3. Schneier, B. (2023). *A Hacker's Mind: How the Powerful Bend Society's Rules, and How to Bend them Back*. W. W. Norton.
4. MITRE. (2024). *MITRE ATT&CK Framework*. https://attack.mitre.org/

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
