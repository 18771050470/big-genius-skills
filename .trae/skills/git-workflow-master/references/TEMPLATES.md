# 技术交付物模板

## Git工作流文档模板

```markdown
# [团队/项目] Git工作流规范

## 分支策略

### 分支模型
[Git Flow / GitHub Flow / GitLab Flow / Trunk-based]

### 分支定义

| 分支 | 用途 | 创建来源 | 合并目标 | 保护规则 |
|------|------|----------|----------|----------|
| main | 生产代码 | - | - | ✅ 禁止直接推送 |
| develop | 集成分支 | main | main | ✅ 需要PR+审查 |
| feature/* | 功能开发 | develop | develop | ✅ 需要PR+审查 |
| release/* | 发布准备 | develop | main+develop | ✅ 仅维护者可创建 |
| hotfix/* | 紧急修复 | main | main+develop | ✅ 需要PR+紧急审查 |

### 分支命名规范
- 功能分支：`feature/[issue-id]-[简短描述]`，如 `feature/123-add-oauth`
- 修复分支：`bugfix/[issue-id]-[简短描述]`，如 `bugfix/456-fix-login`
- 发布分支：`release/[版本号]`，如 `release/1.2.0`
- 热修复分支：`hotfix/[版本号]`，如 `hotfix/1.2.1`

## 提交规范

### 格式
```
<type>(<scope>): <subject>

<body>

<footer>
```

### 类型
| 类型 | 用途 |
|------|------|
| feat | 新功能 |
| fix | 修复 |
| docs | 文档 |
| style | 格式（不影响代码逻辑） |
| refactor | 重构 |
| test | 测试 |
| chore | 构建/工具 |

### 示例
```
feat(auth): add OAuth2 login

- Implement Google OAuth2 flow
- Add GitHub OAuth2 flow
- Update login UI

Closes #123
```

## 代码审查流程

### 审查标准
- [ ] 功能正确性：代码实现了预期功能
- [ ] 安全性：无SQL注入、XSS等漏洞
- [ ] 性能：无明显的性能问题
- [ ] 测试：新增功能有对应测试
- [ ] 规范：符合代码风格规范

### 审查流程
1. 开发者创建PR，填写描述模板
2. CI自动运行测试和检查
3. 分配审查者（按模块或轮询）
4. 审查者逐条检查并提交评论
5. 开发者修改并回复
6. 审查者Approve
7. 合并到目标分支

## 发布流程

### 版本规范
采用 [SemVer / CalVer]：
- 主版本：不兼容的API变更
- 次版本：向下兼容的功能添加
- 修订号：向下兼容的问题修复

### 发布步骤
1. 从develop创建release分支
2. 版本号更新和CHANGELOG生成
3. 回归测试
4. 合并到main并打tag
5. 合并回develop
6. 部署到生产

### 回滚策略
- **触发条件**：生产故障且无法在15分钟内修复
- **操作步骤**：
  1. 执行回滚命令：[具体命令]
  2. 验证回滚结果
  3. 通知团队
  4. 在release分支修复问题
```

---

## 分支策略对比表模板

```markdown
# 分支策略对比

## 团队特征
- 团队规模：[X] 人
- 发布频率：[每日/每周/每月/按需]
- 项目类型：[Web/移动/嵌入式/AI]
- 质量要求：[高/中/低]

## 候选策略对比

| 维度 | Git Flow | GitHub Flow | Trunk-based |
|------|----------|-------------|-------------|
| 复杂度 | 高 | 低 | 中 |
| 适用团队 | >10人 | <10人 | 任意（需CI/CD） |
| 发布节奏 | 计划发布 | 持续部署 | 持续部署 |
| 分支数量 | 多 | 少 | 极少 |
| 学习成本 | 高 | 低 | 中 |
| 与CI/CD集成 | 中 | 高 | 高 |

## 推荐策略
[推荐策略及理由]

## 实施计划
1. [步骤1]
2. [步骤2]
3. [步骤3]
```
