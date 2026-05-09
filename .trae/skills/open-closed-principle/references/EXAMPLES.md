# OCP - 分析示例

## 示例：报表导出格式扩展

```java
// ❌ 违反OCP：每加一种格式都要修改导出方法
class ReportExporter {
  String export(Report r, String format) {
    if ("PDF".equals(format)) return exportPDF(r);
    else if ("Excel".equals(format)) return exportExcel(r);
    else if ("CSV".equals(format)) return exportCSV(r);
    // 加HTML → 修改这个类 → 违反OCP
  }
}

// ✅ OCP修复：策略模式
interface ReportFormatter { String format(Report r); }
class PDFFormatter implements ReportFormatter { ... }
class ExcelFormatter implements ReportFormatter { ... }
class CSVFormatter implements ReportFormatter { ... }

class ReportExporter {
  String export(Report r, ReportFormatter formatter) {
    return formatter.format(r);
  }
}

// 加HTML = 新增HTMLFormatter类，不修改ReportExporter → OCP满足
```

## 示例：通知渠道扩展

```typescript
// ✅ OCP通过组合实现
interface Notifier { send(msg: Message): void; }

class NotificationService {
  constructor(private notifiers: Notifier[]) {}
  notify(msg: Message) {
    this.notifiers.forEach(n => n.send(msg));
  }
}
// 加飞书通知 = new FeishuNotifier() 注入数组，NotificationService零修改
```

## 反例

**输入**："一个简单的工具函数只有10行，要不要为它加接口以备未来可能扩展？"

**原因**：YAGNI——函数极简且无明确扩展需求时，不值得为"可能"做准备。OCP应在真实变化压力下应用，而非预先防御。
