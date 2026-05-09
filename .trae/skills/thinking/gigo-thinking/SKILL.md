---
name: gigo-thinking
description: |
  触发：当处理数据质量问题、数据清洗、评估数据可靠性或建立数据管道时；常见信号包括"数据质量"、"数据清洗"、"缺失值"、"异常值"、"数据验证"、"数据血缘"。
  不触发：当数据已充分验证且质量可控、当使用合成数据且质量已知、当数据质量非关键因素时。
  Invoke when dealing with data quality issues, data cleaning, assessing data reliability, or building data pipelines.
  Do NOT invoke when data is already validated, when using synthetic data with known quality, or when data quality is not critical.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L1"
  related: ["feature-engineering-thinking", "cross-validation-thinking", "defensive-programming", "observability-thinking"]
---

# GIGO思维 (Garbage In, Garbage Out)

## 核心定义

输出质量严格受限于输入质量——如果输入数据存在偏差、错误或不完整，无论算法多么先进，输出结果也必然是错误或不可靠的。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充数据来源或质量要求
- **发现矛盾**：当数据质量与业务期望严重不符时，标记并寻求决策
- **提前终止**：当数据质量已满足要求或确认无法通过清洗挽救时

---

## 思考流程

### Step 1: 数据质量评估

- **完整性**：缺失值比例、字段填充率
- **准确性**：数据与真实值的一致性
- **一致性**：数据格式、单位、编码的统一性
- **时效性**：数据是否反映当前状态
- **唯一性**：是否存在重复记录
- **有效性**：数据是否在合理范围内

---

### Step 2: 数据问题诊断

- **缺失模式分析**：
  - 完全随机缺失（MCAR）
  - 随机缺失（MAR）
  - 非随机缺失（MNAR）
- **异常值检测**：
  - 统计方法（Z-score、IQR）
  - 业务规则验证
- **偏差识别**：
  - 采样偏差
  - 测量偏差
  - 标签偏差
- **数据漂移**：
  - 概念漂移
  - 数据分布漂移

---

### Step 3: 数据清洗策略

- **缺失值处理**：
  - 删除：缺失比例过高时
  - 填充：均值/中位数/众数、模型预测、插值
  - 标记：保留缺失指示特征
- **异常值处理**：
  - 修正：确认为错误时修正
  - 删除：确认为异常时删除
  - 保留：合理异常时保留并标注
- **重复值处理**：
  - 识别重复记录
  - 根据业务规则去重
- **格式标准化**：
  - 统一编码、单位、日期格式

---

### Step 4: 数据验证与监控

- **输入验证**：在数据入口处设置验证规则
- **过程监控**：监控数据管道的健康状态
- **输出验证**：验证下游使用的数据质量
- **数据血缘追踪**：记录数据来源和转换历史

---

### Step 5: 质量门禁设置

- 定义数据质量SLA（服务等级协议）
- 设置质量检查点（数据进入、转换、输出）
- 建立质量异常告警机制
- 制定质量问题升级流程

---

### Step 6: 持续改进

- 定期评估数据质量指标
- 分析数据质量问题的根因
- 优化数据收集和清洗流程
- 输出应包含：质量评估 + 清洗方案 + 监控机制 + 改进建议

---

## 关键原则

1. **预防优于修复**：在数据源头保证质量，而非事后清洗。原因：事后清洗成本高且无法完全恢复信息损失。

2. **验证前置**：在数据使用前必须验证质量。原因：未经验证的数据可能导致错误决策，且错误成本随流程放大。

3. **全链路质量**：数据质量需要在采集、存储、处理、使用全链路保障。原因：任何环节的质量问题都会影响最终结果。

4. **业务语境理解**：数据质量问题需要结合业务语境判断。原因：统计上的异常可能是业务上的正常，反之亦然。

5. **监控自动化**：建立自动化的数据质量监控。原因：人工监控无法覆盖大规模数据，自动化确保及时发现问题。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**GIGO特有关键检查项**：

- [ ] **数据质量评估是否全面？** 完整性、准确性、一致性、时效性都检查了吗？
- [ ] **缺失值处理是否考虑了缺失模式？** MCAR/MAR/MNAR区分了吗？
- [ ] **异常值是否经过业务验证？** 还是仅凭统计规则删除？
- [ ] **是否设置了数据质量门禁？** 低质量数据能否流入下游？
- [ ] **数据血缘是否可追溯？** 问题发生时能否定位源头？
- [ ] **质量监控是否自动化？** 还是依赖人工检查？

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [feature-engineering-thinking](../thinking/feature-engineering-thinking/SKILL.md) | 后置 | 在确保数据质量后进行特征工程 |
| [cross-validation-thinking](../thinking/cross-validation-thinking/SKILL.md) | 并行 | 验证数据质量对模型性能的影响 |
| [defensive-programming](../thinking/defensive-programming/SKILL.md) | 并行 | 在代码层面防御数据质量问题 |
| [observability-thinking](../thinking/observability-thinking/SKILL.md) | 并行 | 监控数据管道的可观测性 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 完整分析示例（输入→各Step→最终输出） |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. McCallum, J. C. (1985). *Computer Security*. Prentice-Hall. (GIGO概念最早来源)
2. Fisher, M., Kingma, B., Fisher, A., & Fisher, M. (2021). *Data Quality: The Accuracy Dimension*. Elsevier.
3. Kim, W., Choi, B. J., Hong, S. K., & Kim, S. K. (2003). A Taxonomy of Dirty Data. *Data Mining and Knowledge Discovery*, 7(1), 81-99.
4. Schelter, S., Lange, D., Schmidt, P., Celikel, M., Biessmann, F., & Grafberger, A. (2018). Automating Large-Scale Data Quality Verification. *Proceedings of the VLDB Endowment*, 11(12), 1781-1794.

---

*本 Skill 遵循 Agent Skills 规范。通用行为规则参考 AGENT_CORE_RULES.md。*
