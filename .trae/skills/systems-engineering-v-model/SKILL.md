---
name: systems-engineering-v-model
description: |
  触发：当开发安全关键系统、需要确保需求与验证双向追溯、管理复杂系统全生命周期、或满足航空航天/汽车/医疗等行业的合规要求时；常见信号包括"V模型"、"需求验证"、"安全关键"、"DO-178C"、"ISO 26262"、"系统验证"。
  不触发：当开发小型非关键系统、敏捷快速迭代项目、需求频繁变更且无需严格追溯的场景。
  Invoke when developing safety-critical systems, ensuring requirements-verification traceability, or meeting aerospace/automotive/medical compliance.
  Do NOT invoke for small non-critical systems, agile rapid iteration, or when requirements change frequently without strict traceability needs.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L3"
  related: ["requirements-traceability", "defense-in-depth", "fmea", "iteration-thinking", "contract-thinking"]
---

# 系统工程V模型 (Systems Engineering V-Model)

## 核心定义

一种系统开发生命周期模型，左侧下降分支进行需求分解和系统设计（做什么），右侧上升分支进行集成验证和确认（验证做对），两侧严格对应确保需求到实现的完整追溯。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充系统安全等级、合规要求、验证资源
- **发现矛盾**：当验证成本与安全性要求冲突时，标记并寻求风险接受或缓解方案
- **提前终止**：当已明确系统开发阶段和对应验证策略时

---

## 思考流程

### Step 1: 系统安全等级与合规框架确定

- 识别适用的行业标准：
  - **航空航天**：DO-178C（软件）、DO-254（硬件）
  - **汽车**：ISO 26262（功能安全）、ASIL等级
  - **医疗**：IEC 62304（医疗器械软件）
  - **工业**：IEC 61508（功能安全）
- 确定安全完整性等级（SIL/ASIL）
- 明确合规要求的严格程度和审计需求

---

### Step 2: V模型左侧——需求与设计分解

- **系统需求分析**：定义系统级功能需求和性能指标
- **系统架构设计**：划分子系统，定义接口
- **软件/硬件需求分析**：将系统需求分配到软硬件
- **软件/硬件架构设计**：定义模块结构和数据流
- **详细设计**：单元级别的算法和逻辑设计
- **编码/实现**：实际开发和单元实现
- **关键原则**：每个左侧阶段必须产生可验证的交付物

---

### Step 3: V模型右侧——验证与确认上升

- **单元测试（Unit Testing）**：验证详细设计，对应详细设计阶段
  - 测试单个函数/模块
  - 覆盖率要求（语句覆盖、分支覆盖、MC/DC等）
- **集成测试（Integration Testing）**：验证架构设计，对应架构设计阶段
  - 测试模块间接口
  - 验证数据流和控制流
- **系统测试（System Testing）**：验证需求分析，对应需求分析阶段
  - 端到端功能验证
  - 性能、可靠性、安全性测试
- **验收测试（Acceptance Testing）**：验证系统需求，对应系统需求阶段
  - 用户场景验证
  - 合规性审计

---

### Step 4: 需求-验证双向追溯矩阵构建

- 建立需求追溯链：
  - 系统需求 ↔ 软件需求 ↔ 详细设计 ↔ 代码 ↔ 测试用例
- 确保双向可追溯：
  - **向前追溯**：每个需求都有对应的实现和验证
  - **向后追溯**：每个测试用例都对应特定需求
- 使用工具管理追溯关系（如Jama、DOORS、Polarion）

---

### Step 5: 验证策略与测试用例设计

- **早期测试规划**：在左侧阶段就开始规划右侧验证
- 测试用例设计原则：
  - 正常场景（Nominal Cases）
  - 边界条件（Boundary Conditions）
  - 异常场景（Error Cases）
  - 鲁棒性测试（Robustness）
- 确定测试环境需求（仿真、硬件在环、实车/实机）

---

### Step 6: 风险识别与缓解策略

- 识别V模型各阶段风险：
  - **需求阶段**：需求遗漏、歧义、不一致
  - **设计阶段**：架构缺陷、接口不匹配
  - **实现阶段**：编码错误、标准违规
  - **验证阶段**：测试覆盖不足、环境不真实
- 制定缓解措施：
  - 评审和检查点
  - 形式化方法
  - 冗余设计
  - 独立验证

---

### Step 7: 配置管理与变更控制

- 建立配置管理流程：
  - 基线管理（需求基线、设计基线、代码基线）
  - 版本控制
  - 变更影响分析
- 变更控制委员会（CCB）机制
- 确保变更的可追溯性和影响分析

---

### Step 8: 评审与审计准备

- 关键评审点：
  - 需求评审（Requirements Review）
  - 设计评审（Design Review）
  - 代码评审（Code Review）
  - 测试评审（Test Readiness Review）
- 审计证据准备：
  - 完整的需求文档
  - 设计文档和评审记录
  - 代码和静态分析报告
  - 测试报告和覆盖率数据

---

### Step 9: 总结输出

- 明确V模型各阶段的交付物和验收标准
- 提供验证策略和测试覆盖计划
- 列出关键风险和缓解措施
- 标注合规要求和审计准备状态
- 建议下一步行动（如启动需求分析阶段）

---

## 关键原则

1. **左侧决定右侧**：验证策略必须在设计阶段早期规划，而非编码完成后才考虑。原因：后期发现需求或设计缺陷的修复成本呈指数级增长。

2. **双向追溯是核心**：每个需求必须有实现和验证，每个验证必须对应特定需求。原因：确保无遗漏、无多余，满足安全关键系统的完整性要求。

3. **文档即证据**：所有工程活动必须产生可审计的文档记录。原因：合规审计和事故调查依赖完整的工程证据链。

4. **独立验证原则**：验证活动应由独立于开发的团队执行。原因：避免开发者偏见，提高缺陷发现率。

5. **早期缺陷捕获**：通过评审、静态分析等手段在设计阶段捕获缺陷。原因：设计阶段修复缺陷的成本是编码后的1/10，是部署后的1/100。

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
- [ ] 考虑了二阶/三阶效应（如验证延迟对项目进度的影响）
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [requirements-traceability](../thinking/requirements-traceability/SKILL.md) | 并行 | 建立需求到验证的完整追溯链 |
| [defense-in-depth](../thinking/defense-in-depth/SKILL.md) | 并行 | 设计多层防御机制满足安全要求 |
| [fmea](../thinking/fmea/SKILL.md) | 后置 | 识别潜在失效模式并制定缓解措施 |
| [iteration-thinking](../thinking/iteration-thinking/SKILL.md) | 对比 | V模型与敏捷迭代的权衡选择 |
| [contract-thinking](../thinking/contract-thinking/SKILL.md) | 并行 | 定义清晰的接口契约 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整V模型应用示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | V模型理论背景与标准详解（可选） |

---

## 参考文献

1. Inovasense. (2024). *V-Model: Verification and Validation Model*. Systems Engineering Glossary.
2. Grokipedia. *V-model (software development)*. Software Development Methodology.
3. RTCA. (2011). *DO-178C: Software Considerations in Airborne Systems and Equipment Certification*.
4. ISO. (2018). *ISO 26262: Road vehicles — Functional safety*.
