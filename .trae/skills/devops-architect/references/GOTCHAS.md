# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：容器镜像使用 root 用户运行应用

**问题**：Dockerfile 中未创建专用用户，容器以 root 运行，一旦容器被入侵，攻击者直接获得宿主机 root 权限。

❌ **Before（错误做法）**
```dockerfile
FROM node:18
COPY . /app
WORKDIR /app
RUN npm install
EXPOSE 3000
CMD ["node", "server.js"]
# 默认以 root 用户运行！
```

✅ **After（正确做法）**
```dockerfile
FROM node:18-alpine
# 创建专用用户和组
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

WORKDIR /app
# 先拷贝依赖文件，利用缓存层
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

# 拷贝应用代码，并修改所有者
COPY --chown=nodejs:nodejs . .

USER nodejs  # 切换到非 root 用户
EXPOSE 3000
CMD ["node", "server.js"]
```

**原因**：容器与宿主机共享内核，容器内 root 就是宿主机 root（除非启用 User Namespace）。创建专用用户并限制权限是容器安全的基础要求。同时多阶段构建和缓存层优化能显著减小镜像体积。

## Gotcha 2：K8s 资源限制缺失导致集群雪崩

**问题**：Pod 没有设置 Resource Request 和 Limit，某个应用内存泄漏耗尽节点资源，导致节点上所有 Pod 被驱逐。

❌ **Before（错误做法）**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-server
spec:
  replicas: 3
  template:
    spec:
      containers:
      - name: api
        image: api:latest
        # 没有资源限制！
```

✅ **After（正确做法）**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-server
spec:
  replicas: 3
  template:
    spec:
      containers:
      - name: api
        image: api:latest
        resources:
          requests:
            memory: "256Mi"   # 保证调度时有这些资源
            cpu: "250m"
          limits:
            memory: "512Mi"   # 超过会被 OOMKilled
            cpu: "500m"       # CPU 可压缩，不会杀死 Pod
        livenessProbe:
          httpGet:
            path: /health
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8080
          initialDelaySeconds: 5
          periodSeconds: 5
```

**原因**：没有资源限制的 Pod 是集群的"噪音邻居"，会无限制消耗节点资源。Request 用于调度决策，Limit 是硬上限。同时必须配置健康探针，让 K8s 知道何时重启或移出流量。

## Gotcha 3：CI/CD 流水线没有安全扫描门禁

**问题**：流水线只跑单元测试，没有安全扫描，将包含漏洞的代码和依赖直接部署到生产。

❌ **Before（错误做法）**
```yaml
# .github/workflows/deploy.yml
jobs:
  deploy:
    steps:
      - uses: actions/checkout@v3
      - run: npm test          # 只有测试
      - run: npm run build
      - run: docker build -t app .
      - run: docker push app   # 直接推送，没有扫描！
      - run: kubectl apply -f k8s/
```

✅ **After（正确做法）**
```yaml
jobs:
  security-scan:
    steps:
      - uses: actions/checkout@v3
      # 依赖漏洞扫描
      - run: npm audit --audit-level=moderate
      # 代码安全扫描
      - uses: securecodewarrior/github-action-add-sarif@v1
      # 镜像扫描
      - run: docker build -t app .
      - uses: aquasecurity/trivy-action@master
        with:
          image-ref: 'app'
          format: 'sarif'
          exit-code: '1'  # 发现漏洞就失败
          severity: 'CRITICAL,HIGH'

  deploy:
    needs: [security-scan]  # 安全扫描通过才能部署
    steps:
      - run: kubectl apply -f k8s/
```

**原因**：安全左移（Shift Left）要求在开发早期发现漏洞。流水线中必须集成依赖扫描（npm audit）、代码扫描（SAST）和镜像扫描，高危漏洞必须阻断部署。

## Gotcha 4：密钥直接写在环境变量或配置文件中

**问题**：将数据库密码、API Token 直接写在 K8s YAML 的 env 或 ConfigMap 中，提交到 Git，造成密钥泄露。

❌ **Before（错误做法）**
```yaml
apiVersion: v1
kind: Deployment
spec:
  template:
    spec:
      containers:
      - name: app
        env:
        - name: DB_PASSWORD
          value: "SuperSecret123!"  # 直接写在 YAML 中！
        - name: API_KEY
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: api-key  # ConfigMap 也不安全！
```

✅ **After（正确做法）**
```yaml
# 使用 External Secrets Operator 从云厂商 Secret Manager 同步
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: app-secrets
spec:
  refreshInterval: 1h
  secretStoreRef:
    kind: ClusterSecretStore
    name: aws-secrets-manager
  target:
    name: app-secrets
    creationPolicy: Owner
  data:
  - secretKey: DB_PASSWORD
    remoteRef:
      key: production/app
      property: db_password

---
# Deployment 引用同步后的 Secret
apiVersion: apps/v1
kind: Deployment
spec:
  template:
    spec:
      containers:
      - name: app
        env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: app-secrets
              key: DB_PASSWORD
```

**原因**：Git 历史永久保存，一旦提交密钥就无法彻底删除。正确做法是使用专门的密钥管理服务（AWS Secrets Manager、Azure Key Vault、HashiCorp Vault），通过 External Secrets Operator 同步到 K8s Secret，并定期轮换。

## Gotcha 5：监控只关注基础设施忽略业务指标

**问题**：监控只配置 CPU/内存/磁盘，没有业务指标监控，导致业务出问题（如订单下降）时无法及时发现。

❌ **Before（错误做法）**
```yaml
# 只有基础设施监控
groups:
- name: infrastructure
  rules:
  - alert: HighCPU
    expr: cpu_usage > 80
  - alert: HighMemory
    expr: memory_usage > 80
  # 没有业务指标！
```

✅ **After（正确做法）**
```yaml
groups:
- name: infrastructure
  rules:
  - alert: HighCPU
    expr: cpu_usage > 80

- name: business  # 业务指标监控
  rules:
  - alert: OrderDrop
    expr: rate(orders_total[5m]) < 0.8 * rate(orders_total[5m] offset 1d)
    for: 5m
    annotations:
      summary: "订单量下降超过 20%"
      
  - alert: PaymentFailure
    expr: rate(payments_failed[5m]) / rate(payments_total[5m]) > 0.05
    for: 2m
    annotations:
      summary: "支付失败率超过 5%"

- name: user_experience
  rules:
  - alert: HighLatency
    expr: histogram_quantile(0.99, http_request_duration_seconds) > 2
    annotations:
      summary: "P99 延迟超过 2 秒"
```

**原因**：基础设施健康 ≠ 业务健康。业务指标（订单量、支付成功率、用户注册数）才是用户真正关心的。RED 方法（Rate/Errors/Duration）是服务指标，必须结合业务指标才能全面观测系统状态。
