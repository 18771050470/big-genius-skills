# 抽象思维常见陷阱

## 陷阱1：过度抽象导致信息丢失

### 问题描述
在抽象过程中，为了追求简洁而剔除了太多细节，导致抽象模型无法区分原本需要区分的变量，失去了实际使用价值。这违背了"目的驱动抽象层次"原则——忽略了"关键细节"的定义。

### ❌ 反例
假设我们要抽象不同支付方式（支付宝、微信支付、信用卡）的核心模型。某团队定义如下接口：
```ts
interface Payment {
  pay(amount: number): boolean;
}
```
这个抽象忽略了**交易凭证**、**支付状态回调**、**退款支持**、**货币差异**、**异步支付确认**等关键细节。结果在集成时发现无法处理支付宝的付款码支付（需要同步返回支付结果），也无法处理信用卡的3D验证（需要跳转页面）。接口过于抽象，导致所有具体实现在内部做了一大堆 hack，破坏了抽象一致性。

### ✅ 正例
根据实际业务需求，保留必要的差异维度：支付方式可分为"即时同步型"（余额、扫码）和"异步型"（银行转账、3D验证）。定义更精确的抽象：
```ts
interface Payment {
  // 同步方法，对于异步支付返回 pending 状态码
  pay(amount: number): PaymentResult;
  cancel(orderId: string): boolean;
  queryStatus(orderId: string): PaymentStatus;
}
enum PaymentResult { SUCCESS, FAILED, PENDING }
enum PaymentStatus { SUCCESS, FAILED, PENDING, REFUNDED }
```
同时针对不同支付方式，增加可选的额外接口（如跳转支付）。

### 原因分析
过度抽象通常是因为过早忽略了"看起来不必要"的细节。检查方法是：用抽象模型去模拟所有原始实例，如果某个实例需要特别的条件判断（if 处理自家逻辑），说明抽象不够。正确的抽象应当让每个实现都天然符合接口契约，而不需要额外工作区或特殊分支。

---

## 陷阱2：过早抽象，样本不足导致模式错误

### 问题描述
仅从一两个实例中提取模式，错误推断出"共性"，然后基于这个共性建立抽象，导致抽象无法覆盖更广泛的实例。这违反了"步骤1收集足够实例"和"步骤7测试新实例"的原则。

### ❌ 反例
一位开发者在接手两个前端表单后，认为所有表单都只有三个字段：姓名、邮箱、密码。于是他抽象出一个 `GenericForm` 组件，只支持文本输入和密码输入。当第三个表单需要上传图片和选择日期时，`GenericForm` 完全无法扩展，必须重写。
```jsx
// 错误抽象：假设所有表单只有文本和密码
function GenericForm({ fields }) {
  return fields.map(f => 
    f.type === 'password' ? <PasswordInput /> : <TextInput />
  );
}
// 新表单需要 FileInput、DatePicker 时无法使用
```

### ✅ 正例
先收集至少5个以上不同功能的表单实例（登录、注册、商品发布、用户设置、搜索表单），发现了字段类型的多样性：文本、数字、邮箱、密码、单选、多选、文件、日期、颜色等。然后抽象出基于"字段类型 + 配置"的渲染模式，并预留自定义组件扩展点：
```jsx
// 良好抽象：支持多种字段类型+自定义组件
function DynamicForm({ schema, customComponents }) {
  return schema.map(field => {
    const Component = customComponents[field.type] || FieldComponents[field.type];
    return <Component key={field.name} {...field} />;
  });
}
// 设计时支持 TextField、SelectField、FileField、DateField 等
// 新类型只需注册组件，无需改动核心抽象
```

### 原因分析
抽象思维需要足够的样本量才能识别真正的共性。一两个实例往往带有偶然性，错误地排除了重要维度。正确的做法是在抽象完整前至少收集3-5个差异较大的实例，并且预留扩展机制。如果实例不够，先保持实现级复用（复制+调整），待更多实例出现后再进行抽象——这符合"重构-抽象"的节奏，而非"超前设计"。