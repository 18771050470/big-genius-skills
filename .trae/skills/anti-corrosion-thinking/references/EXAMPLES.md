# 防腐思维 - 分析示例

## 示例 1: 遗留ERP系统集成

**输入**：新订单系统需要对接公司10年前的ERP系统。ERP提供SOAP接口，数据模型使用德语缩写字段名（如"KND_NR"=客户编号），错误处理是返回"ERROR"字符串。

```
Step 1: 识别腐化源头
→ 产出：SOAP协议腐化 + 德语命名概念腐化 + 粗糙错误处理行为腐化

Step 2: 评估扩散风险
→ 产出：如果不隔离，新订单系统的所有Service都会直接import SOAP客户端、包含德语字段名的DTO，团队新人会认为"SOAP+德语命名"是公司标准

Step 3: 设计防腐层
→ 产出：
  - ERPAdapter：封装SOAP调用，内部处理协议细节
  - ERPTranslator：德语字段→领域语言（KND_NR→customerId）
  - ERPErrorMapper：ERROR字符串→内部异常体系（ERPConnectionException/ERPBusinessException）
  - 对外暴露：ERPFacade接口，只暴露3个方法：getCustomer, createOrder, checkInventory
```

**输出**：

```
## 防腐层设计

### 边界
- 防腐层拥有：ERPAdapter, ERPTranslator, ERPErrorMapper
- 核心领域只依赖：ERPFacade接口（3个方法）
- 核心领域永远不直接引用SOAP客户端或ERP DTO

### 验证
- 如果ERP被替换为新系统：只需重写ERPAdapter内部，核心业务代码0行修改
- 如果ERP字段名变更：只需修改ERPTranslator，核心业务代码0行修改
```

---

## 示例 2: 第三方支付网关防腐

**输入**：接入支付宝/微信支付，两者API风格完全不同。

```
Step 3-4: 设计防腐层
→ 产出：
interface PaymentGateway {
  createPayment(req: CreatePaymentRequest): PaymentResult
  queryPayment(paymentId: string): PaymentStatus
}

class AlipayAdapter implements PaymentGateway {
  // 内部处理支付宝特有的签名、加密、回调验证
  // 对外翻译为统一的PaymentResult
}

class WechatPayAdapter implements PaymentGateway {
  // 内部处理微信特有的XML、nonce、签名
  // 对外翻译为统一的PaymentResult（和支付宝一样）
}
→ 核心OrderService只依赖PaymentGateway接口，不感知具体渠道
```

---

## 反例

**输入**："我们内部两个微服务之间要不要加防腐层？"

**原因**：内部服务架构一致（gRPC+统一Proto定义），不需要防腐层。防腐层主要用于"不可控的外部系统"。
