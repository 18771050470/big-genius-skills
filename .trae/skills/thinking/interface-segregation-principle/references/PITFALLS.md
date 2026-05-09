# ISP - 常见陷阱

## 陷阱 1: 接口碎片化

**问题**：把接口拆得太细。

❌ **Before**: UserSaver（单方法save）、UserLoader（单方法load）、UserDeleter（单方法delete）→ 使用者需要import 3个接口
✅ **After**: UserRepository（save+load+delete都在里面）→ 因为这3个操作永远被同一客户端同时需要

**原因**：ISP的目标是"精准匹配客户端"，不是"每个方法一个接口"。如果3个操作永远一起用，它们属于同一接口。

---

## 陷阱 2: 接口为"将来"预留方法

**问题**：设计接口时把"未来可能用到"的方法也放进去了。

❌ **Before**: interface UserRepository { save(); load(); export(); import(); backup(); restore(); sync(); }
→ 当前只有save/load真正被使用
✅ **After**: interface UserRepository { save(); load(); } → 当确实需要export时，再加新的Exporter接口

**原因**：YAGNI——你不一定需要它。预留方法让接口变胖，ISP被违反。
