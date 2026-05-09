# 分析示例

## 示例 1：后端 API 响应缓慢问题

### 输入场景
某电商后端 `/checkout` 接口在高峰期平均响应时间从 200ms 暴涨到 2.5s，用户反馈超时。团队初看觉得系统复杂，不知道瓶颈在哪。

### Step 1: 整体边界界定
- 系统：`/checkout` 端到端请求链路（从 API 网关 → 应用服务器 → 订单服务 → 支付服务 → 库存服务 → 数据库/缓存）
- 输入：用户购物车、优惠码、支付信息
- 输出：订单创建成功/失败、支付结果
- 期望行为：<500ms 响应

### Step 2: 层次划分
- 应用层：控制器 → 业务服务 → 领域模型
- 基础设施层：缓存 (Redis)、数据库 (PostgreSQL)、外部支付 API

### Step 3: 组件识别
- 控制器：`CheckoutController.checkout()`
- 业务服务：`CheckoutService.createOrder()`，内部调用：
  - `OrderService.generateOrder()`
  - `PaymentService.charge()`
  - `InventoryService.confirm()`
- 数据访问：`OrderRepository`、`InventoryRepository`
- 外部依赖：Payment Gateway API (Stripe)

### Step 4: 独立分析
- 使用 APM (如 New Relic) 给每个组件打点，记录耗时:
  - `CheckoutService.createOrder()`: 2.3s (总)
  - `PaymentService.charge()`: 2.0s
  - `InventoryService.confirm()`: 0.2s
  - `OrderRepository.save()`: 0.1s
- 单独调用 `PaymentService.charge()` 直接测试：耗时 1.9s，返回正常。
- 排查 Payment 内部：发现它连续调用了三次 `getPaymentGatewayToken()`（每次都发起 HTTPS 请求），实际只需要一次。

### Step 5: 交互关系建模
- 时序图显示：`CheckoutController` → `CheckoutService` → `PaymentService` → `Stripe API` (3次)
- 依赖矩阵：PaymentService 强依赖 Stripe 网络延迟，且无缓存

### Step 6: 全局综合
- **根因**：`PaymentService.charge()` 内部冗余调用 `getPaymentGatewayToken()`，导致额外 2*300ms = 600ms 延迟，加上网络波动上升到 2s。
- **建议**：优化 token 获取为缓存逻辑，仅首次请求令牌，后续复用。

### Step 7: 验证
- 修改后本地模拟：token 缓存后，`charge()` 耗时降为 600ms，总接口降到 800ms。
- 灰度上线后监控：P95 响应时间从 2.5s 降为 500ms。

### 最终输出
- 根因分析报告 + 代码变更（token 缓存 + 重试策略优化）
- 新增单元测试覆盖 token 缓存场景

---

## 示例 2：前端内存泄漏排查

### 输入场景
单页应用（React + Redux）运行 1 小时后，浏览器 tab 占用内存从 200MB 增长到 1.2GB，页面卡顿。开发人员怀疑是内存泄漏，但代码庞大，不知从何查起。

### Step 1: 整体边界界定
- 系统：SPA 应用生命周期（首页加载 → 用户操作 → 路由切换 → 离开页面）
- 输入：用户交互事件、API 响应
- 输出：UI 更新、组件挂载/卸载
- 表现：内存持续增长，GC 不释放

### Step 2: 层次划分
- 路由级：各个页面（Home, Product, Cart, OrderHistory）
- 组件级：每个页面内的子组件（列表、详情弹窗、图表）
- 数据层：Redux store、异步请求缓存

### Step 3: 组件识别
- 高频切换的组件：`ProductList`（列表）、`OrderHistory`（无限滚动）、`Chart`（ECharts 图表）
- 全局组件：`Header`、`NotificationCenter`

### Step 4: 独立分析
- 使用 Chrome DevTools Memory 录制快照：
  - 进入 `OrderHistory` 页面 → 离开 → 快照对比：发现大量 `OrderRow` 组件实例未被销毁。
  - 进一步查看 `OrderRow` 组件内部：`useEffect` 中订阅了 `WebSocket`，但未在 return 的 cleanup 中取消订阅。
  - 检查其他组件：`Chart` 组件在 `useEffect` 中创建了 ECharts 实例并挂载到 DOM，但卸载时未调用 `dispose()`。

### Step 5: 交互关系建模
- `OrderHistory` → `OrderRow` (多个) → WebSocketManager (全局单例)
- WebSocketManager 保存所有订阅回调数组，`OrderRow` 卸载时未从数组中移除回调，导致闭包引用保留组件 DOM。

### Step 6: 全局综合
- **根因**：两处泄漏：
  1. `OrderRow` 未取消 WebSocket 订阅，导致组件实例无法被 GC。
  2. `Chart` 未 dispose ECharts 实例，Canvas 资源未释放。
- **建议**：修复 cleanup 函数；在 `OrderRow` unmount 时调用 `unsubscribe()`；在 `Chart` useEffect cleanup 中调用 `chart.dispose()`。

### Step 7: 验证
- 修复后使用同样操作序列，内存稳定在 250MB 左右，不再增长。
- 添加 E2E 内存测试（Puppeteer）验证无泄漏。

### 最终输出
- 根因定位 + 代码修复 PR
- 新增 lint 规则强制 `useEffect` 必须包含 cleanup

---

## 反例：不应该使用还原论的场景

### 输入
团队要决定是否从单体架构迁移到微服务架构，成员提出了大量技术细节（每个函数、每个 SQL 查询），希望用还原论一一分析。

### 为什么不使用还原论
- 该决策本质是**系统架构选型**，关注的是整体演化性、团队组织（康威定律）、运维复杂度等涌现特性。过度拆解函数级细节反而会忽略整体权衡。
- 正确的做法：先用**系统思维**画出当前架构的耦合度、变更影响半径、部署瓶颈；再使用**权衡分析**评估微服务带来的收益与代价；最后只在决定迁移后再用还原论细化拆分步骤。

### 若错误使用还原论：
- 团队花费两周分析每个接口的代码实现，发现 80% 的接口都很简单，得出结论"可以微服务化"，但实际上忽略了数据一致性、服务发现、分布式事务等涌现问题，导致迁移失败。

### 正确做法：
- 使用**系统思维**识别核心问题域边界，用**DDD**（领域驱动设计）划分限界上下文，最终决定是否拆分、如何拆分。