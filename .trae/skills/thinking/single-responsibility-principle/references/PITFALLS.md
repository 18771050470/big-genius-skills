# SRP - 常见陷阱

## 陷阱 1: "一个类只做一件事"的教条

**问题**：机械地把每个功能拆成独立类。

❌ **Before**: 一个UserService拆成UserNameUpdater、UserEmailUpdater、UserPasswordUpdater → 10个微型类，组合关系复杂
✅ **After**: 一个UserProfileService包含name/email的更新（同属"用户自己修改资料"这一职责）

**原因**：SRP的"职责"由Actor定义——所有因同一Actor变化而修改的功能属于同一职责。name/email都因用户修改而变化→同一职责。

---

## 陷阱 2: 跟混内聚（Cohesion）

**问题**：不相关的功能凑在一起，却认为它是"一个职责"。

❌ **Before**: "这个UserManager类负责用户相关的所有事情" → 包含注册、登录、权限、资料、通知、统计...
✅ **After**: 按Actor拆分——注册登录(用户)、权限(管理员)、资料(用户自己)、通知(运营)、统计(数据分析)

**原因**："用户相关"不是职责——它只是一个主题标签。真正的职责由变化源定义。
