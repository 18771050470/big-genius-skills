# SRP - 分析示例

## 示例：员工报表模块

**输入**：一个 `EmployeeReport` 类同时承担"数据查询"（为DBA变化）和"格式渲染"（为管理层UI变化）。

```java
// ❌ SRP违反：两个变化原因
class EmployeeReport {
  List<Employee> queryDB();     // DBA要求改 → 这个类要改
  String renderHTML();          // 管理层要求改 → 这个类也要改
  String renderPDF();
}

// ✅ SRP修复：按Actor拆分
class EmployeeDataAccess {      // 为DBA服务
  List<Employee> queryDB();
}
class EmployeeReportFormatter { // 为管理层服务
  String toHTML(List<Employee>);
  String toPDF(List<Employee>);
}
```

**验证**：DBA要求换数据库连接池 → 只改EmployeeDataAccess，Formatter无感知。

## 示例：用户注册服务

```java
// ❌ 一个类承担了"注册规则"（产品团队变更）和"密码加密"（安全团队变更）
class UserRegistration {
  void register(User user) {
    validateBusinessRules(user);    // 产品团队
    String hash = bcrypt(user.pw); // 安全团队
    repo.save(user);
    sendWelcomeEmail(user);        // 运营团队
  }
}

// ✅ 拆分：
class RegistrationPolicy { void validate(User); }       // 产品
class PasswordEncoder { String hash(String raw); }       // 安全
class WelcomeEmailSender { void send(User); }           // 运营
class UserRegistration { /* 编排调用，非自己实现 */ }   // 单一职责：流程编排
```

## 反例

**输入**："一个User类有name、email和address字段，name和email会变，address也会变→应该拆成Name+Email类和Address类吗？"

**原因**：name/email/address都因同一个Actor（用户自己修改资料）而变化 → 属于同一职责。按功能相似度拆分而非按Actor拆分，是SRP最常见的误用。
