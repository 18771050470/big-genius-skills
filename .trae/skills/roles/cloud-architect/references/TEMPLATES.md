# 技术交付物模板

## 交付物模板 1：云架构设计文档

```markdown
# 云架构设计：[项目名称]

## 架构概述
- **业务场景**：[描述]
- **预期规模**：[用户量/QPS/数据量]
- **合规要求**：[等保/GDPR/数据本地化]

## 架构图
```
[用户] → [CDN] → [WAF] → [Load Balancer] → [Web Servers]
                                              ↓
                                       [Application Servers]
                                              ↓
                                       [Database Primary]
                                              ↓
                                       [Database Standby]
```

## 组件选型

### 计算
| 组件 | 选型 | 规格 | 数量 | 成本/月 |
|------|------|------|------|---------|
| Web 层 | ECS Fargate | 1 vCPU, 2GB | 4 | $200 |
| 应用层 | ECS Fargate | 2 vCPU, 4GB | 4 | $400 |

### 存储
| 组件 | 选型 | 规格 | 成本/月 |
|------|------|------|---------|
| 数据库 | RDS MySQL | db.r5.large | $300 |
| 缓存 | ElastiCache Redis | cache.r5.large | $150 |
| 对象存储 | S3 | Standard | $100 |

### 网络
| 组件 | 选型 | 成本/月 |
|------|------|---------|
| CDN | CloudFront | $150 |
| WAF | AWS WAF | $50 |
| Load Balancer | ALB | $100 |

## 高可用设计
- **多 AZ**：Web/应用层 3 AZ，数据库 Multi-AZ
- **自动扩缩容**：CPU > 70% 扩容，< 30% 缩容
- **故障转移**：数据库自动故障转移 < 60 秒

## 安全设计
- **网络**：VPC 分段，安全组最小权限
- **身份**：IAM Role，无长期凭证
- **数据**：传输 TLS 1.3，存储 AES-256
- **应用**：WAF，DDoS 防护，输入验证

## 成本估算
- **月度总计**：$[金额]
- **年度总计**：$[金额]
- **优化建议**：[RI/SP/Spot 建议]
```

## 交付物模板 2：多云对比矩阵

```markdown
# 云服务商对比：[项目需求]

## 评估维度

| 维度 | AWS | Azure | GCP | 推荐 |
|------|-----|-------|-----|------|
| 计算服务 | ECS/EKS/Lambda | AKS/Container Apps | GKE/Cloud Run | [推荐] |
| 托管数据库 | RDS/Aurora | Azure SQL | Cloud SQL | [推荐] |
| 成本 | 中等 | 较高 | 较低 | [推荐] |
| 生态成熟度 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | [推荐] |
| 团队技能 | 熟悉 | 不熟悉 | 不熟悉 | [推荐] |

## 推荐方案
- **主云**：[云服务商]
- **理由**：[说明]
- **备选**：[云服务商]

## 风险
| 风险 | 缓解措施 |
|------|---------|
| 供应商锁定 | 使用 Kubernetes + 开源工具 |
| 成本超支 | 预算告警 + 成本分摊 |
```

## 交付物模板 3：Terraform 模块结构

```hcl
# 项目结构
terraform/
├── modules/
│   ├── vpc/           # 网络模块
│   ├── compute/       # 计算模块
│   ├── database/      # 数据库模块
│   └── security/      # 安全模块
├── environments/
│   ├── dev/           # 开发环境
│   ├── staging/       # 测试环境
│   └── prod/          # 生产环境
└── global/            # 全局资源（如 S3 bucket）

# 环境配置示例（environments/prod/main.tf）
module "vpc" {
  source = "../../modules/vpc"
  
  environment = "prod"
  cidr_block  = "10.0.0.0/16"
  azs         = ["us-east-1a", "us-east-1b", "us-east-1c"]
}

module "compute" {
  source = "../../modules/compute"
  
  environment = "prod"
  vpc_id      = module.vpc.vpc_id
  subnet_ids  = module.vpc.private_subnet_ids
  instance_type = "t3.medium"
  desired_count = 4
}

module "database" {
  source = "../../modules/database"
  
  environment = "prod"
  vpc_id      = module.vpc.vpc_id
  subnet_ids  = module.vpc.database_subnet_ids
  instance_class = "db.r5.large"
  multi_az    = true
}
```

## 交付物模板 4：成本优化报告

```markdown
# 云成本优化报告：[月份]

## 当前支出
| 服务 | 本月 | 上月 | 变化 | 占比 |
|------|------|------|------|------|
| EC2 | $2000 | $1800 | +11% | 40% |
| RDS | $1500 | $1500 | 0% | 30% |
| S3 | $500 | $400 | +25% | 10% |
| 其他 | $1000 | $900 | +11% | 20% |
| **总计** | **$5000** | **$4600** | **+9%** | **100%** |

## 优化机会

### 机会 1：Reserved Instance
- **资源**：RDS db.r5.large
- **当前**：On-Demand $1500/月
- **优化**：1 年 RI，节省 40%
- **节省**：$600/月

### 机会 2：存储分层
- **资源**：S3 Standard 10TB
- **当前**：$230/月
- **优化**：7 天后转 Infrequent Access，30 天后转 Glacier
- **节省**：$100/月

### 机会 3：闲置资源
- **资源**：3 台 EC2 非生产环境，夜间运行
- **优化**：自动关机（20:00-08:00）
- **节省**：$200/月

## 预期效果
- **月度节省**：$900（18%）
- **年度节省**：$10,800
```
