# LSP - 常见陷阱

## 陷阱 1: 为代码复用而继承

**问题**：用继承复用代码，但子类在行为上不是真正的父类。

❌ **Before**: Stack extends ArrayList → Stack可以调用ArrayList的add(index)在任意位置插入，破坏LIFO契约
✅ **After**: Stack持有ArrayList作为内部实现，只暴露push/pop/peek，不暴露ArrayList的其他方法

**原因**：继承 = is-a关系。Stack is-not-a ArrayList（行为契约不同）。代码复用用组合。

---

## 陷阱 2: 子类"选择性覆盖"父类方法

**问题**：子类覆盖了父类方法但改变了其语义。

❌ **Before**: 父类removeUser(id)删除用户记录，子类Override为"软删除"（标记而非真删）→ 调用方期望真删但实际没删
✅ **After**: 不要覆盖改变语义。如果子类需要软删除→新增softRemoveUser方法，不覆盖removeUser
