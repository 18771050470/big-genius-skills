# DIP - 常见陷阱

## 陷阱 1: 抽象定义在低层

**问题**：接口定义在实现包中，高层还是依赖低层包。

❌ **Before**: com.example.db.MySQLRepository (接口在此包里定义) ← com.example.service.OrderService 依赖db包
✅ **After**: com.example.service.OrderRepository (接口在service包) ← com.example.db.MySQLRepository 依赖service包

**原因**：DIP的核心是"谁拥有接口"。高层拥有接口 = 高层制定契约，低层遵守契约。如果低层拥有接口，低层变更时接口也变更，高层还是被动。

---

## 陷阱 2: 倒置所有依赖（包括标准库）

**问题**：为String、ArrayList也创建接口。

❌ **Before**: interface StringProvider { String getString(); } → 倒置对String的依赖
✅ **After**: 直接使用String。标准库/语言内置类型极不可能变化，不需要倒置

**原因**：DIP针对"容易变化的实现细节"，不是所有具体类。倒置稳定依赖（标准库）纯属过度设计。

---

## 陷阱 3: 过分倒置导致IOC地狱

**问题**：到处注入接口，一个Service注入10个依赖。

❌ **Before**: OrderService构造器接收10个接口参数 → 难以理解、难以测试、难以实例化
✅ **After**: 聚合相关接口为Facade：OrderService接收3个聚合接口而不是10个散接口

**原因**：过度倒置会引发的"接口爆炸"和"构造函数膨胀"——依赖倒置应适度，DIP不是"所有依赖都要倒置然后注入"。
