# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：分支模型与团队规模不匹配

**问题**：为小团队设计复杂的Git Flow，或为大型团队使用过于简单的GitHub Flow，导致流程负担或协作混乱。

❌ **Before（错误做法）**
5人小团队采用完整Git Flow（main/develop/feature/release/hotfix），每次发布需要创建release分支、打tag、合并回develop，流程过于繁重。

✅ **After（正确做法）**
5人小团队采用GitHub Flow或简化Git Flow：main分支 + feature分支，PR合并后直接发布。随着团队规模增长再逐步引入release分支。

**原因**：分支模型的复杂度应与团队规模和发布频率匹配。小团队使用复杂模型会增加不必要的流程负担，大团队使用简单模型会导致发布混乱。

---

## Gotcha 2：长期存在的功能分支

**问题**：功能分支存在时间过长（超过1周），导致合并冲突严重、集成困难。

❌ **Before（错误做法）**
开发者创建feature分支后工作2周，期间从未同步main分支，合并时产生大量冲突，花费一整天解决。

✅ **After（正确做法）**
功能分支生命周期控制在1周内，每日从main同步（rebase或merge），及时解决小冲突，避免积累成大冲突。

**原因**：长期分支与主干 diverge 越多，合并成本越高。持续集成实践要求频繁集成，小步快跑比大步慢走更高效。

---

## Gotcha 3：代码审查流于形式

**问题**：PR审查只是走过场，审查者不看代码直接Approve，导致问题代码进入主干。

❌ **Before（错误做法）**
团队规定PR需要1个Approve，但审查者只是扫一眼就点Approve，不检查逻辑、不测试、不提问。

✅ **After（正确做法）**
建立审查checklist（功能正确性、安全性、性能、测试覆盖），要求审查者逐条确认；设置"审查质量"指标（如发现问题数/审查PR数）；对关键PR要求多人审查。

**原因**：代码审查是质量门禁，流于形式会完全丧失价值。需要建立可执行的审查标准和质量反馈机制。

---

## Gotcha 4：忽视提交信息质量

**问题**：提交信息随意编写，导致历史记录无法阅读，问题追溯困难。

❌ **Before（错误做法）**
提交信息："fix bug"、"update"、"123"、"WIP"、"asdf"，无法从提交历史理解变更内容。

✅ **After（正确做法）**
采用Conventional Commits规范：
```
feat(auth): add OAuth2 login support

- Implement Google and GitHub OAuth2 flows
- Add user profile sync
- Update login UI with social buttons

Closes #123
```

**原因**：提交信息是代码历史的重要组成部分，影响CHANGELOG生成、版本号确定、问题追溯、代码审查。规范的提交信息让历史记录成为有价值的知识库。
