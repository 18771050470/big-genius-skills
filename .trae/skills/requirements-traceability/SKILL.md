---
name: requirements-traceability
description: |
  触发：当管理复杂项目需求、确保需求完整实现、进行影响分析、满足合规审计要求或管理需求变更时；常见信号包括"需求追溯"、"RTM"、"变更影响"、"需求矩阵"、"合规审计"、"需求管理"。
  不触发：当项目规模极小需求简单、敏捷项目无需正式追溯、无合规或审计要求时。
  Invoke when managing complex requirements, ensuring complete implementation, impact analysis, or compliance audits.
  Do NOT invoke for small simple projects, informal agile contexts, or when no compliance requirements exist.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L3"
  related: ["systems-engineering-v-model", "contract-thinking", "iteration-thinking", "root-cause-analysis"]
---

# 需求追溯思维 (Requirements Traceability)

## 核心定义

通过建立需求与需求、需求与设计、需求与实现、需求与验证之间的双向链接，确保每个需求都可追溯到其来源、实现和验证，支持变更影响分析和合规审计的系统工程实践。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充需求来源、项目范围、追溯目标
- **发现矛盾**：当追溯成本与价值冲突时，标记并寻求优先级排序方案
- **提前终止**：当已建立关键追溯链或确认追溯策略时

---

## 思考流程

### Step 1: 追溯目标与范围确定

- **明确追溯目的**：
  - 证明合规性（Compliance Demonstration）
  - 确保测试覆盖（Test Coverage）
  - 支持变更管理（Change Management）
  - 便于影响分析（Impact Analysis）
  - 项目状态跟踪（Project Tracking）
- **确定追溯粒度**：
  - 高层需求（业务需求）
  - 功能需求
  - 非功能需求（性能、安全、可靠性）
  - 设计元素
  - 代码单元
  - 测试用例
- **识别追溯边界**：哪些需求需要追溯，哪些可以豁免

---

### Step 2: 需求层级结构建立

- **需求分类与分层**：
  - **业务需求**（Business Requirements）：高层业务目标
  - **用户需求**（User Requirements）：用户视角的功能描述
  - **系统需求**（System Requirements）：系统视角的技术规格
  - **软件需求**（Software Requirements）：软件层面的详细需求
- **建立层级关系**：
  - 父子关系（分解关系）
  - 依赖关系（一个需求依赖另一个）
  - 派生关系（从其他需求派生）
- **唯一标识**：为每个需求分配唯一ID（如REQ-001, SR-002）

---

### Step 3: 追溯矩阵设计与构建

- **选择矩阵类型**：
  - **正向追溯**（Forward Traceability）：需求 → 设计 → 代码 → 测试
  - **反向追溯**（Backward Traceability）：测试 → 代码 → 设计 → 需求
  - **双向追溯**（Bidirectional）：同时支持正向和反向
- **矩阵维度设计**：
  - 需求 ↔ 需求（层级关系）
  - 需求 ↔ 设计（架构元素、接口）
  - 需求 ↔ 实现（代码模块、函数）
  - 需求 ↔ 验证（测试用例、验证方法）
  - 需求 ↔ 风险（风险项、缓解措施）
- **工具选择**：Excel（简单项目）、专业ALM工具（Jama、DOORS、Polarion）

---

### Step 4: 追溯链接建立

- **正向链接建立**：
  - 每个需求链接到实现它的设计元素
  - 每个设计元素链接到对应的代码单元
  - 每个代码单元链接到验证它的测试用例
- **反向链接建立**：
  - 每个测试用例追溯到验证的需求
  - 每个代码单元追溯到实现的设计
  - 每个设计元素追溯到满足的需求
- **链接属性记录**：
  - 链接类型（实现、验证、派生等）
  - 链接强度（强相关、弱相关）
  - 链接状态（已验证、待验证）

---

### Step 5: 追溯完整性检查

- **孤儿需求检测**：识别无下游链接的需求（未实现）
- **金匠检测**：识别无上游链接的实现元素（无需求依据）
- **覆盖分析**：
  - 需求覆盖率：有多少需求有测试覆盖
  - 测试冗余度：有多少测试不对应任何需求
- **一致性检查**：确保双向链接的一致性

---

### Step 6: 变更影响分析流程

- **变更请求接收**：记录变更的原因、来源、优先级
- **影响范围识别**：
  - 直接影响：被修改的需求本身
  - 二级影响：依赖该需求的其他需求
  - 实现影响：需要修改的设计和代码
  - 验证影响：需要更新的测试用例
- **影响评估**：
  - 工作量估算
  - 风险识别
  - 进度影响
- **变更决策支持**：为CCB（变更控制委员会）提供数据支持

---

### Step 7: 追溯维护与更新

- **变更时更新**：任何需求变更必须同步更新追溯链
- **定期审查**：定期检查追溯矩阵的准确性和完整性
- **版本控制**：追溯矩阵与需求文档版本同步
- **自动化支持**：
  - 集成开发环境自动链接
  - 测试工具自动关联
  - 静态分析工具辅助验证

---

### Step 8: 报告与审计支持

- **追溯报告生成**：
  - 需求覆盖报告
  - 变更影响报告
  - 合规性报告
- **审计证据准备**：
  - 完整的追溯矩阵
  - 变更历史记录
  - 评审和批准记录
- **可视化展示**：追溯图、依赖图、覆盖热力图

---

### Step 9: 总结输出

- 提供追溯策略和实施计划
- 列出关键追溯链和覆盖状态
- 给出变更管理流程建议
- 标注追溯工作的成本和收益
- 建议下一步行动（如工具选型、流程建立）

---

## 关键原则

1. **双向追溯是标准**：正向追溯确保需求被实现，反向追溯确保实现有依据。原因：单向追溯无法发现无需求依据的实现（金匠问题）。

2. **追溯成本与价值平衡**：不是所有需求都需要同等粒度追溯。原因：追溯有成本，应优先保障高风险、高价值需求的追溯完整性。

3. **工具自动化是关键**：手工维护追溯矩阵在大项目中不可持续。原因：需求变更频繁，手工更新容易出错且工作量巨大。

4. **追溯是活文档**：追溯矩阵必须随项目进展持续更新。原因：过时的追溯信息比没有追溯更危险，会误导决策。

5. **追溯支持决策而非替代判断**：追溯数据为决策提供依据，但最终决策仍需人工判断。原因：追溯无法捕捉所有隐性依赖和上下文因素。

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
- [ ] 考虑了二阶/三阶效应（如追溯工作量对项目进度的影响）
- [ ] 输出具体可执行，不含模糊建议（如"优化一下"）
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列
- [ ] 明确了下一步应该调用哪个 Skill（如果需要）

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [systems-engineering-v-model](../thinking/systems-engineering-v-model/SKILL.md) | 并行 | V模型各阶段交付物的追溯管理 |
| [contract-thinking](../thinking/contract-thinking/SKILL.md) | 并行 | 需求作为系统与外部的契约 |
| [iteration-thinking](../thinking/iteration-thinking/SKILL.md) | 对比 | 敏捷迭代中的轻量级追溯策略 |
| [root-cause-analysis](../thinking/root-cause-analysis/SKILL.md) | 后置 | 利用追溯链进行问题根因分析 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整追溯矩阵示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |
| [references/THEORY.md](references/THEORY.md) | 理论 | 需要深入理解理论渊源时 | 需求工程理论详解（可选） |

---

## 参考文献

1. Jama Software. (2024). *How to Create Requirements Traceability Matrix (RTM)*.
2. TestRail. (2024). *Requirements Traceability Matrix (RTM): A How-To Guide*.
3. Perforce. (2024). *How to Create a Requirements Traceability Matrix*.
4. IEEE. (1998). *IEEE Std 830-1998: Recommended Practice for Software Requirements Specifications*.
