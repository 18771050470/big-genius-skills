# LSP - 分析示例

## 示例：经典的"正方形不是矩形"

```java
// ❌ LSP违反
class Rectangle {
  void setWidth(int w) { this.width = w; }
  void setHeight(int h) { this.height = h; }
  int getArea() { return width * height; }
  // 隐式契约：setWidth(w) 后 getHeight() 不变
}

class Square extends Rectangle {
  void setWidth(int w) { this.width = w; this.height = w; } // 改了height!
  // 调用方：rect.setWidth(5) → 期望height不变，实际height被改了
}

// 调用方代码会出错：
void resize(Rectangle rect) {
  rect.setWidth(10);
  rect.setHeight(5);
  assert rect.getArea() == 50; // 如果是Square → area=25，断言失败
}
```

## 示例：鸟和企鹅

```java
// ❌ LSP违反：企鹅会飞吗？
class Bird {
  void fly() { /* 飞 */ }
}
class Penguin extends Bird {
  void fly() { throw new UnsupportedOperationException("企鹅不会飞"); }
  // 调用方遍历 Bird[] 调用 fly() → 遇到Penguin就崩
}

// ✅ 方案：组合替代继承
interface Flying { void fly(); }
class Sparrow implements Flying { void fly() {...} }
class Penguin { void swim() {...} } // 不实现Flying
```

## 示例：文件存储

```java
// ❌ LSP违反
class FileStore {
  void save(String path, byte[] data);
  // 隐式契约：save后立即可以read
}
class S3Store extends FileStore {
  void save(String key, byte[] data) {
    // S3是最终一致性！save后立即read可能返回旧数据
    // 违反父类契约
  }
}

// ✅ 修复：明确契约差异
interface Storage {
  void save(String key, byte[] data);
  // 契约明确：保存后不保证立即可读（最终一致性）
}
```

## 反例

**输入**："List和Set都实现了Collection接口，但Set不允许重复元素→是不是LSP违反？"

**原因**：不是。Collection接口的前置条件是"add接受任何元素"，Set收紧了前置条件（拒绝重复元素），这确实是LSP违反的历史案例。但Java通过文档+抛出异常来约定此行为，实践中被接受。这提醒我们：LSP是理想目标，有时因实用性做妥协。
