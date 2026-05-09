# DIP - 分析示例

## 示例：经典三层架构违反DIP

```java
// ❌ DIP违反：Service直接依赖具体的Repository实现
class OrderService {
  private MySQLOrderRepository repo = new MySQLOrderRepository();
  // Service → MySQLOrderRepository (高层依赖低层具体类)
  // 换PostgreSQL → 必须修改OrderService → 违反DIP
}

// ✅ DIP修复：Service依赖抽象，Repository实现抽象
interface OrderRepository {          // 接口由Service层定义（高层拥有）
  Order save(Order order);
  Order findById(Long id);
}

class OrderService {
  private OrderRepository repo;      // 依赖抽象
  public OrderService(OrderRepository repo) { this.repo = repo; }
}

class MySQLOrderRepository implements OrderRepository { ... }
class PostgreSQLOrderRepository implements OrderRepository { ... }
// 换数据库 = 新实现类 + 注入给Service → Service零修改
```

## 示例：通知服务依赖具体SDK

```typescript
// ❌ DIP违反
class NotificationService {
  private emailSDK = new SendGridSDK("api-key");   // 直接依赖SendGrid
  sendEmail(to: string, body: string) {
    this.emailSDK.send({ to, html: body });        // 如果换成AWS SES → 改这里
  }
}

// ✅ DIP修复
interface EmailProvider {                           // 高层定义
  send(to: string, content: EmailContent): Promise<void>;
}

class SendGridProvider implements EmailProvider {
  send(to, content) { return this.sdk.send({ to, html: content.body }); }
}

class SESProvider implements EmailProvider {
  send(to, content) { return this.ses.sendEmail({ Destination: to, ... }); }
}

class NotificationService {
  constructor(private provider: EmailProvider) {}   // 依赖抽象
  sendEmail(to, body) { return this.provider.send(to, { body }); }
}
// 换AWS SES → 新建SESProvider注入，NotificationService零修改
```
