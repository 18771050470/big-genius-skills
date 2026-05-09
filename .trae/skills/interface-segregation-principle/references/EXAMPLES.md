# ISP - 分析示例

## 示例：多功能打印机

```java
// ❌ 胖接口：普通打印机被迫实现扫描和传真的方法
interface MultiFunctionPrinter {
  void print(Document doc);
  void scan(Document doc);
  void fax(Document doc);
}

class SimplePrinter implements MultiFunctionPrinter {
  void print(Document doc) { /* 实现 */ }
  void scan(Document doc) { throw new UnsupportedOperationException(); }
  void fax(Document doc) { throw new UnsupportedOperationException(); }
  //胖接口症状：空实现
}

// ✅ ISP修复
interface Printer { void print(Document doc); }
interface Scanner { void scan(Document doc); }
interface Fax { void fax(Document doc); }

class SimplePrinter implements Printer { ... }              // 只实现需要的
class AllInOne implements Printer, Scanner, Fax { ... }     // 全实现
```

## 示例：用户服务接口拆分

```java
// ❌ 胖接口
interface UserService {
  User getUser(Long id);
  void updateProfile(User user);
  void resetPassword(Long userId);       // 只有管理后台需要
  List<User> exportAllUsers();           // 只有数据组需要
  void sendMarketingEmail(Long userId);  // 只有运营需要
}

// ✅ 按客户端角色拆分
interface UserBasicService {              // 普通用户
  User getUser(Long id);
  void updateProfile(User user);
}
interface UserAdminService {              // 管理员
  void resetPassword(Long userId);
}
interface UserDataService {               // 数据组
  List<User> exportAllUsers();
}
```

## 反例

**输入**："Collection接口有add、remove、contains、iterator这么多方法→应该拆成Adder、Remover、Searcher、Iterator四个接口吗？"

**原因**：过度拆分。Collection的所有方法都是所有客户端需要的——你不会只add而不需要iterator。ISP的目标是"精准匹配"，不是"最小化"——当所有客户端都需要所有方法时，一个接口就够了。
