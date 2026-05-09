# Gotchas

> 只写云架构容易犯错的**非显而易见的事实**。通用知识不要写。

## Gotcha 1：多区域部署但未设计跨区域故障转移

**问题**：应用在多个可用区（AZ）部署，但数据库是单点，AZ 故障时数据库不可用，整个应用瘫痪。

❌ **Before（错误做法）**
```yaml
# 架构：多 AZ 部署，但数据库单点
Web Servers:
  - AZ-1a: 2 instances
  - AZ-1b: 2 instances
  - AZ-1c: 2 instances

Database:
  - AZ-1a: 1 instance  # 单点！
  
# AZ-1a 故障时：
# - Web Servers 自动切换到 AZ-1b/1c ✅
# - Database 不可用 ❌
# - 整个应用瘫痪
```

✅ **After（正确做法）**
```yaml
# 架构：多 AZ + 数据库高可用
Web Servers:
  - AZ-1a: 2 instances
  - AZ-1b: 2 instances
  - AZ-1c: 2 instances

Database:
  Primary: AZ-1a
  Standby: AZ-1b  # 跨 AZ 副本
  
# 配置自动故障转移
# - RDS Multi-AZ: 自动故障转移（< 60 秒）
# - 应用使用 DNS endpoint，自动指向新主库

# AZ-1a 故障时：
# - Web Servers 切换到 AZ-1b/1c ✅
# - Database 自动切换到 AZ-1b ✅
# - 服务继续可用（短暂中断 < 60 秒）
```

**原因**：多 AZ 部署只解决了计算层的高可用，数据层的高可用需要额外的设计（Multi-AZ、只读副本、跨区域复制）。

## Gotcha 2：过度使用 Serverless 导致成本失控

**问题**：所有功能都用 Lambda/Cloud Functions，冷启动延迟高，且高并发时成本比 VM 还高。

❌ **Before（错误做法）**
```markdown
# 架构：全部 Serverless
- API: Lambda + API Gateway
- 后台任务: Lambda
- 数据处理: Lambda
- 文件处理: Lambda

# 问题
- 冷启动：API 首次请求 2-5 秒
- 高并发：1000 并发 Lambda = 成本爆炸
- 长时间任务：Lambda 最大 15 分钟，复杂任务中断
- 成本：月均 $5000，同等 VM 只需 $800
```

✅ **After（正确做法）**
```markdown
# 架构：Serverless + VM 混合
- API: ECS/Fargate（长期运行，低延迟）
- 事件处理: Lambda（异步，低频次）
- 批处理: ECS Scheduled Task（长时间任务）
- 文件处理: Lambda（事件驱动，快速）

# 选型原则
| 场景 | 推荐 | 原因 |
|------|------|------|
| 高频 API | VM/容器 | 低延迟，成本可控 |
| 低频事件 | Serverless | 按需付费，无闲置 |
| 长时间任务 | VM/容器 | 无超时限制 |
| 突发流量 | Serverless | 自动扩缩容 |

# 成本：月均 $1200（节省 76%）
```

**原因**：Serverless 不是银弹。高频、长时间、高并发的场景用 VM/容器更划算。Serverless 适合低频、事件驱动、快速启动的场景。

## Gotcha 3：未配置资源标签导致成本无法分摊

**问题**：云资源没有统一标签，月度账单无法按团队/项目/环境拆分，不知道钱花在哪。

❌ **Before（错误做法）**
```bash
# 创建资源时不打标签
aws ec2 run-instances --image-id ami-12345 --instance-type t3.medium

# 月底看账单：
# - EC2: $5000（不知道哪个团队用的）
# - RDS: $3000（不知道哪个项目的）
# - S3: $1000（不知道是什么数据）
# 无法优化，因为不知道钱花在哪
```

✅ **After（正确做法）**
```bash
# 强制标签策略
aws ec2 run-instances \
  --image-id ami-12345 \
  --instance-type t3.medium \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Environment,Value=production},{Key=Team,Value=backend},{Key=Project,Value=payment},{Key=CostCenter,Value=cc-1234}]'

# 使用 SCP 强制所有资源必须有标签
# 使用 AWS Cost Explorer 按标签分析

# 月底看账单：
# - backend 团队: $4000
#   - payment 项目: $2500
#   - user 项目: $1500
# - frontend 团队: $2000
# - devops 团队: $1000

# 优化：payment 项目 RDS 过大，可降级实例类型
```

**原因**：标签是成本管理的基础。没有标签，云成本就是黑盒。必须通过 SCP/IAM 策略强制打标签，并使用 Cost Explorer 分析。

## Gotcha 4：IAM 过度授权导致安全风险

**问题**：为了省事，给所有用户和角色 AdministratorAccess，一旦凭证泄露，整个账号被控制。

❌ **Before（错误做法）**
```json
// 所有角色都有管理员权限
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}

// 问题
// - 开发账号可删除生产数据库
// - CI/CD 角色可修改 IAM 策略
// - 泄露一个凭证 = 整个账号沦陷
```

✅ **After（正确做法）**
```json
// 最小权限原则
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::my-app-bucket/*"
    }
  ]
}

// 使用 IAM Role，不用长期凭证
// - EC2 使用 Instance Role
// - Lambda 使用 Execution Role
// - CI/CD 使用 OIDC 联邦身份（无长期密钥）

// 定期审计
// - IAM Access Analyzer：识别外部访问
// - CloudTrail：记录所有 API 调用
// - 每季度审查 IAM 策略
```

**原因**：IAM 是云安全的第一道防线。过度授权是数据泄露的主要原因（如 Capital One 事件）。必须遵循最小权限原则，使用 Role 而非长期凭证，定期审计。
