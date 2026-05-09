# 极简思维 - 分析示例

> 至少 2 个示例，展示从输入到输出的完整推理链。

## 示例质量验证标准

| 检查项 | 标准 |
|--------|------|
| **完整性** | 包含输入→每步动作→每步输出→最终结论 |
| **可追踪性** | 最终结论必须能追溯到具体步骤的产出 |
| **具体性** | 输出含具体数据/代码/指标，非泛泛而谈 |
| **优先级** | 建议必须按优先级排序，说明排序依据 |
| **边界覆盖** | 包含至少 1 个"不该触发此 Skill"的失败案例 |

---

## 示例 1：React组件过度设计精简

**输入**：一个用户信息展示组件，经过多次迭代后变得臃肿。

```tsx
// 当前组件（经过3个人各加功能后）
interface UserCardProps {
  user: User;
  showAvatar?: boolean;
  showEmail?: boolean;
  showPhone?: boolean;
  showAddress?: boolean;
  avatarSize?: 'sm' | 'md' | 'lg' | 'xl';
  onAvatarClick?: (user: User) => void;
  onEmailClick?: (email: string) => void;
  className?: string;
  style?: React.CSSProperties;
  theme?: 'light' | 'dark' | 'auto';
  compact?: boolean; // 紧凑模式
  withBorder?: boolean;
  loading?: boolean;
}

// 组件内部200多行，处理各种组合
```

```
Step 1: 列出所有元素
→ 产出：14个props + 200行渲染逻辑
  来源：showAvatar是A加的，showEmail是B加的，theme是C加的，compact是D加的

Step 2: 必要性评估
→ 产出：
  - 核心（移除后组件失效）：user, avatarSize
  - 增强（移除后体验下降）：showAvatar, showEmail, onAvatarClick, loading
  - 装饰（移除后无实质影响）：theme（实际只用了1次）、withBorder（CSS替代）、compact（用CSS media query替代）、showPhone（从未使用）、showAddress（从未使用）
  
  反向测试：
  - 假设没有theme → 组件仍然正常工作
  - 假设没有withBorder → 可以用className传入CSS控制，组件更灵活
  - 假设没有showPhone → 搜索代码库，0处调用

Step 3: 移除代价评估
→ 产出：
  - showPhone/showAddress：0处调用 → 零代价移除
  - theme：1处调用（暗色模式）→ 改为用CSS变量继承，不通过props传
  - withBorder：3处调用 → 改为className="bordered" + CSS
  - compact：2处调用 → 改为CSS @media (max-width: 768px)自动紧凑

Step 4: 最小必要版本
→ 产出：
  - 新的props：{ user, showAvatar?, showEmail?, onAvatarClick?, loading?, className? }
  - 从14个减少到6个props，代码从200行减少到80行
  - 自检：是否有功能丢失？ → 无，theme/compact/withBorder通过CSS实现，功能等价

Step 5: 防复胖机制
→ 产出：
  - 新增props的准入门槛：必须被至少2个调用方使用 + 无法通过CSS或组合实现
  - 代码审查时标注：新增props需说明"为什么不能通过组合实现"
```

**输出**：

```
## 分析结论

### 移除清单（按优先级）
1. [立即] showPhone, showAddress — 从未使用，直接删除
2. [本周] theme — 改为CSS变量继承
3. [本周] withBorder — 改为className + CSS
4. [本周] compact — 改为CSS media query自动适配

### 精简后方案
props从14个减到6个，代码从200行减到80行，功能等价

### 防复胖
- props准入：≥2调用方 + 非CSS可实现
- 每个props必须有"为什么存在"的注释
```

---

## 示例 2：API接口精简

**输入**：一个用户管理API，提供以下端点：

```
GET    /api/users                # 用户列表
GET    /api/users/:id            # 用户详情
POST   /api/users                # 创建用户
PUT    /api/users/:id            # 更新用户（全量）
PATCH  /api/users/:id            # 更新用户（部分）
DELETE /api/users/:id            # 删除用户
POST   /api/users/:id/activate   # 激活用户
POST   /api/users/:id/deactivate # 停用用户
GET    /api/users/:id/orders     # 用户订单
GET    /api/users/:id/settings   # 用户设置
PUT    /api/users/:id/settings   # 更新用户设置
```

```
Step 1: 列出所有元素
→ 产出：11个端点，8个方法

Step 2: 必要性评估
→ 产出：
  - PUT和PATCH都支持更新 → 保留PATCH（部分更新更安全），移除PUT。如果客户端需要全量更新，用PATCH传全部字段
  - activate/deactivate是PATCH /users/:id {status: 'active'/'inactive'} 的特例
    → 移除activate和deactivate，统一用PATCH
  - /users/:id/settings和PUT /users/:id/settings → settings是什么？如果就是用户记录的一部分字段，那就是PATCH /users/:id的子集
    → 移除settings独立端点，用PATCH /users/:id传对应字段

Step 3: 移除代价
→ 产出：
  - PUT有3处调用 → 改为PATCH，改动量<10行
  - settings端点被1个新功能使用 → 改为PATCH /users/:id，改动量<5行
  
Step 4: 最小必要版本
→ 产出：6个端点（从11个精简到6个，减少45%）
  GET    /api/users
  GET    /api/users/:id
  POST   /api/users
  PATCH  /api/users/:id      # 统一：更新、激活/停用、设置修改
  DELETE /api/users/:id
  GET    /api/users/:id/orders

Step 5: 防复胖
→ 产出：
  - 新增端点的判断标准：是否能用已有端点的参数/字段表达？能则不新增
  - 规则：字段已在已有资源中 → 用PATCH，不新建子资源端点
```

**输出**：

```
## 分析结论
11个端点精简到6个，减少45%。
核心原则：能用PATCH + 字段表达的就不新建端点。
移除PUT（用PATCH替代）、移除独立的子资源写端点（合并到主资源PATCH）

### 关键假设
- PATCH合并字段不会造成权限问题（activate权限应该通过字段级权限控制，而非端点级）
```

---

## 反例：不该触发极简思维的场景

**输入**："这个登录页面的密码输入框要不要删掉？把用户名输入框做大一点，密码用别的方式验证。好像还可以删掉'忘记密码'链接..."

**原因**：安全性和用户体验必需的组件不是"多余"的。极简思维的目标是移除"非本质"的东西，不是移除"你觉得不够优雅"的东西。密码输入框是登录的本质组件，不能因为想"更少"而删除。
