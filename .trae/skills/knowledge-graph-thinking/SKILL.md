---
name: knowledge-graph-thinking
description: |
  触发：当需要组织复杂知识、构建语义网络、实现智能问答、或进行知识推理时；常见信号包括"知识图谱"、"实体关系"、"语义网络"、"本体"、"知识推理"、"智能搜索"。
  不触发：当数据结构简单关系明确、无需语义理解、或传统数据库已满足需求时。
  Invoke when organizing complex knowledge, building semantic networks, or enabling intelligent reasoning.
  Do NOT invoke for simple structured data, when semantic understanding is unnecessary, or traditional databases suffice.
license: MIT
metadata:
  type: "thinking-model"
  category: "thinking"
  layer: "L3"
  related: ["dikw-pyramid", "seci-model", "system-thinking", "information-architecture"]
---

# 知识图谱思维 (Knowledge Graph Thinking)

## 核心定义

一种用图结构表示知识的方法，通过实体（节点）和关系（边）构建语义网络，捕捉现实世界中事物间的复杂关联，支持知识推理、智能问答和语义搜索。

---

## 思考流程控制

### 中断处理

- **信息不足**：用 AskUserQuestion 向用户提问补充知识领域范围、目标应用场景、现有数据源
- **发现矛盾**：当知识表示需求与图模型能力冲突时，标记并寻求替代方案
- **提前终止**：当已确定知识图谱适用性或确认需要其他方案时

---

## 思考流程

### Step 1: 知识领域界定

- **领域范围确定**：
  - 垂直领域（医疗、金融、法律等）
  - 通用领域（百科知识、常识）
  - 企业内部知识
- **应用场景明确**：
  - 智能问答
  - 推荐系统
  - 知识推理
  - 语义搜索
  - 风险评估
- **边界设定**：明确包含和不包含的内容范围

---

### Step 2: 实体识别与定义

- **实体类型识别**：
  - 人物（Person）
  - 组织（Organization）
  - 地点（Location）
  - 概念（Concept）
  - 事件（Event）
  - 产品/物品（Product/Item）
- **实体属性定义**：
  - 唯一标识符
  - 名称和别名
  - 类型标签
  - 描述信息
- **实体粒度确定**：
  - 粗粒度（类别级）
  - 细粒度（实例级）
  - 混合粒度策略

---

### Step 3: 关系设计与定义

- **关系类型识别**：
  - 层级关系（is-a, part-of）
  - 属性关系（has-attribute）
  - 关联关系（related-to）
  - 因果关系（causes, leads-to）
  - 时空关系（located-in, happens-at）
- **关系属性定义**：
  - 关系方向性
  - 关系强度/权重
  - 关系时间范围
  - 关系来源/置信度
- **关系约束**：
  - 定义域和值域
  - 基数约束（一对一、一对多、多对多）
  - 传递性、对称性等特性

---

### Step 4: 本体（Ontology）构建

- **本体作用**：
  - 定义概念层次结构
  - 规范术语使用
  - 支持逻辑推理
- **本体组件**：
  - 类（Class）定义
  - 属性（Property）定义
  - 约束（Constraint）定义
  - 实例（Instance）规范
- **本体工程方法**：
  - 自顶向下（从概念到实例）
  - 自底向上（从实例归纳概念）
  - 混合方法

---

### Step 5: 知识抽取与获取

- **结构化数据转换**：
  - 关系数据库映射
  - CSV/Excel数据导入
  - API数据接入
- **半结构化数据抽取**：
  - HTML/XML解析
  - JSON数据提取
  - 表格数据识别
- **非结构化数据抽取**：
  - 命名实体识别（NER）
  - 关系抽取（RE）
  - 事件抽取
- **知识融合**：
  - 实体对齐（Entity Alignment）
  - 关系融合
  - 冲突消解

---

### Step 6: 知识存储与建模

- **图数据库选择**：
  - Neo4j（属性图模型）
  - Amazon Neptune（多模型）
  - JanusGraph（分布式）
  - RDF Store（语义网）
- **数据模型设计**：
  - 属性图模型（节点+边+属性）
  - RDF三元组（Subject-Predicate-Object）
- **存储优化**：
  - 索引策略
  - 分区策略
  - 缓存机制

---

### Step 7: 知识推理与查询

- **推理类型**：
  - 基于本体的推理（类层次、属性传递）
  - 基于规则的推理（IF-THEN规则）
  - 基于图算法的推理（路径分析、社区发现）
  - 基于嵌入的推理（知识图谱嵌入）
- **查询语言**：
  - Cypher（Neo4j）
  - SPARQL（RDF）
  - Gremlin（Apache TinkerPop）
- **查询优化**：
  - 查询计划优化
  - 索引利用
  - 结果缓存

---

### Step 8: 应用层设计

- **智能问答系统**：
  - 自然语言理解
  - 知识图谱查询生成
  - 答案生成与验证
- **推荐系统**：
  - 基于路径的推荐
  - 基于嵌入的推荐
  - 混合推荐策略
- **可视化展示**：
  - 图可视化
  - 关系探索界面
  - 知识导航

---

### Step 9: 质量评估与维护

- **质量维度**：
  - 准确性（Accuracy）
  - 完整性（Completeness）
  - 一致性（Consistency）
  - 时效性（Timeliness）
  - 可信度（Credibility）
- **评估方法**：
  - 人工抽样检查
  - 自动一致性验证
  - 应用效果评估
- **维护策略**：
  - 定期更新机制
  - 增量更新策略
  - 版本管理

---

### Step 10: 总结输出

- 提供知识图谱架构设计
- 给出实体和关系定义方案
- 列出技术选型和实施路径
- 标注关键挑战和风险
- 建议下一步行动（如启动本体构建）

---

## 关键原则

1. **本体是知识图谱的宪法**：良好的本体设计决定知识图谱的质量和可用性。原因：本体定义了知识表示的基本规则和结构框架。

2. **质量优于数量**：准确的少量知识比大量噪声知识更有价值。原因：错误知识会导致错误推理，质量问题是知识图谱的最大风险。

3. **持续演化是常态**：知识图谱不是一次性项目，需要持续维护和更新。原因：知识会过时，新知识不断产生。

4. **多源融合是挑战**：不同来源知识的融合是最大的技术难点。原因：实体歧义、关系冲突、格式差异需要复杂的融合算法。

5. **应用驱动设计**：知识图谱设计应服务于具体应用场景。原因：通用知识图谱难以构建，聚焦应用可提高实用性和投资回报率。

---

## 自检清单

**执行规则**：
- **执行方**：Agent 自检，在最终输出前逐项确认
- **未通过处理**：任一检查项未通过，必须修正后重新自检，禁止跳过
- **强制停止项**：以下检查项未通过时，必须停止输出并修正：
  - [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
  - [ ] 输出具体可执行，不含模糊建议
  - [ ] 标注了关键假设和不确定性

**完整检查项**：

- [ ] 已按思考流程完成全部步骤，无跳过（或已标注提前终止原因）
- [ ] 每步思考要点已覆盖，无遗漏
- [ ] 每步结论标注了置信度和反证可能性
- [ ] 考虑了二阶/三阶效应（如知识图谱维护成本）
- [ ] 输出具体可执行，不含模糊建议
- [ ] 标注了关键假设和不确定性
- [ ] 识别了最大风险点和缓解措施
- [ ] 建议按优先级排序，不是平铺罗列

---

## 相关思维模型

| Skill | 关系 | 使用场景 |
|-------|------|---------|
| [dikw-pyramid](../thinking/dikw-pyramid/SKILL.md) | 前置 | 理解知识在认知层次中的位置 |
| [seci-model](../thinking/seci-model/SKILL.md) | 前置 | 理解知识创造过程 |
| [system-thinking](../thinking/systems-thinking/SKILL.md) | 并行 | 从系统角度理解知识关联 |
| [information-architecture](../thinking/information-architecture/SKILL.md) | 并行 | 设计知识组织和导航结构 |

---

## 参考资料（按需加载）

| 文件 | 类型 | 何时加载 | 说明 |
|------|------|---------|------|
| [references/EXAMPLES.md](references/EXAMPLES.md) | 示例 | 需要理解如何使用此思维模型时 | 知识图谱构建示例 |
| [references/PITFALLS.md](references/PITFALLS.md) | 陷阱 | 需要规避常见错误时 | 常见陷阱（含反例+正例+原因） |

---

## 参考文献

1. Hogan, A., et al. (2021). *Knowledge Graphs*. ACM Computing Surveys.
2. IBM. (2024). *What is a knowledge graph?*.
3. 百科. *知识图谱[使用图结构存储实体信息与关系的知识库]*.
4. Patterns Journal. (2022). *A glossary of commonly used terms in knowledge graphs*.
