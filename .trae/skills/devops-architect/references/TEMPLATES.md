# 技术交付物模板

> 提供可直接使用的 Markdown/代码模板。

## 交付物模板 1：CI/CD 流水线配置

```yaml
# .github/workflows/main.yml
name: Build and Deploy

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
      
      - run: npm ci
      - run: npm run lint
      - run: npm run test:coverage
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3

  security-scan:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/checkout@v4
      
      - name: Run Trivy vulnerability scanner
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: 'fs'
          scan-ref: '.'
          format: 'sarif'
          output: 'trivy-results.sarif'

  build:
    runs-on: ubuntu-latest
    needs: [test, security-scan]
    permissions:
      contents: read
      packages: write
    steps:
      - uses: actions/checkout@v4
      
      - name: Log in to Container Registry
        uses: docker/login-action@v3
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      
      - name: Extract metadata
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
          tags: |
            type=sha,prefix={{branch}}-
            type=ref,event=branch
      
      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}

  deploy-staging:
    runs-on: ubuntu-latest
    needs: build
    environment: staging
    steps:
      - name: Deploy to Staging
        run: |
          kubectl set image deployment/app \
            app=${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:sha-${{ github.sha }}
          kubectl rollout status deployment/app
```

## 交付物模板 2：Kubernetes 资源配置

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
  labels:
    app: app
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  selector:
    matchLabels:
      app: app
  template:
    metadata:
      labels:
        app: app
    spec:
      securityContext:
        runAsNonRoot: true
        runAsUser: 1000
        fsGroup: 1000
      containers:
      - name: app
        image: app:latest
        ports:
        - containerPort: 8080
          protocol: TCP
        env:
        - name: NODE_ENV
          value: "production"
        - name: DB_HOST
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: db_host
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: app-secrets
              key: db_password
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        readinessProbe:
          httpGet:
            path: /ready
            port: 8080
          initialDelaySeconds: 5
          periodSeconds: 5
          timeoutSeconds: 3
          failureThreshold: 3
        securityContext:
          allowPrivilegeEscalation: false
          readOnlyRootFilesystem: true
          capabilities:
            drop:
            - ALL
---
apiVersion: v1
kind: Service
metadata:
  name: app
spec:
  selector:
    app: app
  ports:
  - port: 80
    targetPort: 8080
  type: ClusterIP
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    cert-manager.io/cluster-issuer: "letsencrypt"
spec:
  tls:
  - hosts:
    - app.example.com
    secretName: app-tls
  rules:
  - host: app.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: app
            port:
              number: 80
```

## 交付物模板 3：监控告警规则

```yaml
# prometheus-rules.yaml
groups:
- name: application.rules
  rules:
  - alert: HighErrorRate
    expr: |
      (
        sum(rate(http_requests_total{status=~"5.."}[5m]))
        /
        sum(rate(http_requests_total[5m]))
      ) > 0.05
    for: 2m
    labels:
      severity: critical
    annotations:
      summary: "High error rate on {{ $labels.service }}"
      description: "Error rate is {{ $value | humanizePercentage }}"

  - alert: HighLatency
    expr: |
      histogram_quantile(0.99,
        sum(rate(http_request_duration_seconds_bucket[5m])) by (le, service)
      ) > 2
    for: 5m
    labels:
      severity: warning
    annotations:
      summary: "High latency on {{ $labels.service }}"
      description: "P99 latency is {{ $value }}s"

  - alert: PodCrashLooping
    expr: |
      rate(kube_pod_container_status_restarts_total[10m]) > 0
    for: 5m
    labels:
      severity: critical
    annotations:
      summary: "Pod {{ $labels.pod }} is crash looping"

- name: infrastructure.rules
  rules:
  - alert: HighCPUUsage
    expr: |
      100 - (avg by (instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 80
    for: 10m
    labels:
      severity: warning
    annotations:
      summary: "High CPU usage on {{ $labels.instance }}"

  - alert: HighMemoryUsage
    expr: |
      (
        node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes
      ) / node_memory_MemTotal_bytes * 100 > 85
    for: 10m
    labels:
      severity: warning
    annotations:
      summary: "High memory usage on {{ $labels.instance }}"
```

## 交付物模板 4：故障处理 Runbook

```markdown
# Runbook: [故障类型]

## 故障现象
- **告警名称**：[告警名]
- **影响范围**：[描述影响的用户/服务/功能]
- **严重程度**：P0（核心业务中断）/ P1（部分功能异常）/ P2（轻微影响）

## 快速诊断

### 步骤 1: 确认故障范围
```bash
# 检查 Pod 状态
kubectl get pods -n <namespace>

# 检查服务状态
kubectl get svc -n <namespace>

# 查看事件
kubectl get events -n <namespace> --sort-by='.lastTimestamp'
```

### 步骤 2: 查看日志
```bash
# 查看应用日志
kubectl logs -n <namespace> <pod-name> --tail=100

# 查看所有 Pod 日志
kubectl logs -n <namespace> -l app=<app-name> --tail=50
```

### 步骤 3: 检查资源使用
```bash
# 查看资源使用
kubectl top pod -n <namespace>

# 查看节点资源
kubectl top node
```

## 常见原因与处理

### 原因 1: [原因描述]
**识别信号**：...
**处理步骤**：
1. ...
2. ...
3. ...

### 原因 2: [原因描述]
**识别信号**：...
**处理步骤**：
1. ...
2. ...

## 应急回滚
```bash
# 回滚到上一个版本
kubectl rollout undo deployment/<deployment-name> -n <namespace>

# 确认回滚状态
kubectl rollout status deployment/<deployment-name> -n <namespace>
```

## 验证恢复
- [ ] 服务状态正常
- [ ] 监控指标恢复
- [ ] 业务功能验证通过

## 事后分析
- **根因**：...
- **影响时长**：...
- **改进措施**：...
```
