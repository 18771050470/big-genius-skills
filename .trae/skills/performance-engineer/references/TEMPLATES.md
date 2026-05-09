# 技术交付物模板

## 交付物模板 1：性能测试方案

```markdown
# 性能测试方案：[系统名称]

## 测试目标
- **业务场景**：[描述]
- **性能目标**：
  - 吞吐量：[QPS/TPS]
  - 响应时间：P50 < [X]ms, P95 < [Y]ms, P99 < [Z]ms
  - 错误率：< [N]%
  - 并发用户：[N]

## 测试场景
| 场景 | 并发 | 持续时间 | 目标 QPS |
|------|------|---------|---------|
| 基线 | 10 | 10min | 100 |
| 正常负载 | 100 | 30min | 1000 |
| 峰值负载 | 200 | 15min | 2000 |
| 压力测试 | 500 | 10min | 找到拐点 |
| 稳定性 | 100 | 8h | 1000 |

## 测试数据
- **数据量**：[N] 条（生产环境的 [N]%）
- **数据分布**：[描述]
- **热点数据**：[描述]

## 监控指标
- **应用**：QPS、响应时间、错误率、GC
- **数据库**：QPS、慢查询、连接数、锁等待
- **系统**：CPU、内存、磁盘 IO、网络
```

## 交付物模板 2：性能测试脚本（k6）

```javascript
// performance-test.js
import http from 'k6/http';
import { check, sleep, group } from 'k6';
import { Trend, Rate } from 'k6/metrics';

const apiTrend = new Trend('api_response_time');
const errorRate = new Rate('errors');

export const options = {
  stages: [
    { duration: '5m', target: 100 },   // 渐进
    { duration: '10m', target: 100 },  // 稳定
    { duration: '5m', target: 200 },   // 峰值
    { duration: '5m', target: 200 },   // 峰值稳定
    { duration: '5m', target: 0 },     // 降载
  ],
  thresholds: {
    http_req_duration: ['p(95)<200', 'p(99)<500'],
    http_req_failed: ['rate<0.01'],
    errors: ['rate<0.05'],
  },
};

export default function () {
  group('首页', () => {
    const res = http.get('https://example.com/');
    apiTrend.add(res.timings.duration);
    const success = check(res, {
      '首页状态 200': (r) => r.status === 200,
      '首页 < 200ms': (r) => r.timings.duration < 200,
    });
    errorRate.add(!success);
  });

  group('商品列表', () => {
    const res = http.get('https://example.com/api/products?page=1');
    apiTrend.add(res.timings.duration);
    const success = check(res, {
      '列表状态 200': (r) => r.status === 200,
      '列表 < 300ms': (r) => r.timings.duration < 300,
    });
    errorRate.add(!success);
  });

  sleep(1);
}
```

## 交付物模板 3：性能测试报告

```markdown
# 性能测试报告：[系统名称] [版本号]

## 测试概况
- **测试时间**：[起止时间]
- **测试环境**：[配置]
- **测试工具**：k6 + Grafana + Prometheus

## 性能指标

### 吞吐量
| 场景 | 目标 QPS | 实际 QPS | 状态 |
|------|---------|---------|------|
| 正常负载 | 1000 | 1200 | ✅ |
| 峰值负载 | 2000 | 1800 | ⚠️ |
| 压力极限 | - | 2500 | - |

### 响应时间
| 场景 | P50 | P95 | P99 | 状态 |
|------|-----|-----|-----|------|
| 正常负载 | 45ms | 120ms | 200ms | ✅ |
| 峰值负载 | 80ms | 300ms | 800ms | ⚠️ |

### 资源使用
| 指标 | 正常负载 | 峰值负载 | 瓶颈 |
|------|---------|---------|------|
| CPU | 40% | 85% | 接近瓶颈 |
| 内存 | 60% | 75% | 正常 |
| DB CPU | 50% | 90% | 🔴 瓶颈 |

## 瓶颈分析
1. **数据库 CPU 90%**：慢查询导致，需优化索引
2. **峰值 P99 800ms**：连接池耗尽，需扩容

## 优化建议
1. 优化 SQL 查询，添加复合索引
2. 连接池从 50 扩容到 100
3. 引入 Redis 缓存热点数据

## 附件
- [详细监控图表]
- [火焰图]
- [慢查询日志]
```

## 交付物模板 4：容量规划文档

```markdown
# 容量规划：[系统名称]

## 当前容量
| 指标 | 当前值 | 峰值 | 利用率 |
|------|--------|------|--------|
| QPS | 1000 | 1500 | 67% |
| 存储 | 500GB | 600GB | 83% |
| 并发连接 | 500 | 800 | 63% |

## 增长预测
| 时间 | 用户增长 | QPS 预测 | 存储预测 |
|------|---------|---------|---------|
| 3 个月 | 50% | 1500 | 750GB |
| 6 个月 | 100% | 2000 | 1TB |
| 12 个月 | 200% | 3000 | 1.5TB |

## 扩容方案
| 时间 | 扩容内容 | 成本 | 风险 |
|------|---------|------|------|
| 3 个月 | DB 升级 4核→8核 | ¥5000/月 | 低 |
| 6 个月 | 加 2 台应用服务器 | ¥8000/月 | 中 |
| 12 个月 | 分库分表 | ¥15000/月 | 高 |

## 触发条件
- CPU > 70% 持续 5 分钟 → 扩容
- 磁盘 > 80% → 清理或扩容
- P99 > 500ms → 优化或扩容
```
