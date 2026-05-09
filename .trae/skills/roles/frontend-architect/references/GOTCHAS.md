# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。
> **筛选标准**：只有满足以下条件的坑才值得写：
> 1. 非显而易见（不是"要处理空指针"这种常识）
> 2. 有实际危害（会导致 Bug、性能问题或安全漏洞）
> 3. 有明确规避方法（不能只是"小心点"）

## Gotcha 1：Context 层层传递导致渲染性能灾难

**问题**：在深层组件树中通过 Props 逐层传递数据，导致中间组件不必要的重渲染，性能急剧下降。

❌ **Before（错误做法）**
```typescript
// 顶层组件传递 user 给深层 Avatar 组件
function App() {
  const [user, setUser] = useState({ name: 'Alice', avatar: 'url' });
  return <Layout user={user} />;  // Layout 不需要 user，但必须传递
}
function Layout({ user }) {
  return <Sidebar><Main user={user} /></Sidebar>;  // Sidebar 重渲染了！
}
```

✅ **After（正确做法）**
```typescript
// 使用 Context 或状态管理库，避免层层传递
const UserContext = createContext(null);

function App() {
  const [user, setUser] = useState({ name: 'Alice', avatar: 'url' });
  return (
    <UserContext.Provider value={user}>
      <Layout />  // Layout 不需要知道 user
    </UserContext.Provider>
  );
}

function Avatar() {
  const user = useContext(UserContext);  // 只在需要的地方消费
  return <img src={user.avatar} />;
}
```

**原因**：Props drilling 会导致中间组件不必要的重渲染，即使它们不直接使用数据。React Context 或 Redux/Zustand 等状态管理方案可以让数据消费组件直接订阅，跳过中间层。

## Gotcha 2：useEffect 依赖数组遗漏导致闭包陷阱

**问题**：useEffect 依赖数组不完整，导致回调函数引用过期状态，产生难以调试的 Bug。

❌ **Before（错误做法）**
```typescript
function Counter() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    const timer = setInterval(() => {
      console.log(count);  // 永远输出 0！
      setCount(count + 1); // 永远设置为 1！
    }, 1000);
    return () => clearInterval(timer);
  }, []); // 遗漏 count 依赖
}
```

✅ **After（正确做法）**
```typescript
function Counter() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    const timer = setInterval(() => {
      setCount(c => c + 1);  // 使用函数式更新，不依赖外部 count
    }, 1000);
    return () => clearInterval(timer);
  }, []); // 空依赖正确，因为不引用外部变量
}
```

**原因**：React 的闭包机制会捕获 effect 创建时的状态值。遗漏依赖会导致使用过期值。解决方案：使用函数式更新 setState，或使用 useRef 保存最新值。

## Gotcha 3：Bundle 体积失控—— tree-shaking 失效

**问题**：导入整个库而不是具体模块，导致 tree-shaking 失效，Bundle 体积暴增。

❌ **Before（错误做法）**
```typescript
import _ from 'lodash';  // 导入全部 70KB+
import * as Icons from '@ant-design/icons';  // 导入全部 500+ 图标
```

✅ **After（正确做法）**
```typescript
import debounce from 'lodash/debounce';  // 只导入需要的函数
import { SearchOutlined, UserOutlined } from '@ant-design/icons';  // 按需导入
// 或使用 babel-plugin-import 自动按需加载
```

**原因**：Webpack/Rollup 的 tree-shaking 对 `import *` 和默认导入优化有限。按需导入可以确保只打包使用的代码，减少 50%-90% 的 Bundle 体积。

## Gotcha 4：CSS-in-JS 运行时性能损耗

**问题**：在性能敏感场景使用运行时 CSS-in-JS（如 styled-components），导致大量运行时计算和插入样式标签。

❌ **Before（错误做法）**
```typescript
// 每次渲染都生成新类名，运行时计算样式
const DynamicButton = styled.button<{ priority: 'high' | 'low' }>`
  background: ${props => props.priority === 'high' ? 'red' : 'gray'};
  padding: 10px;
`;
```

✅ **After（正确做法）**
```typescript
// 使用零运行时方案：CSS Modules 或 Tailwind
// 或编译时 CSS-in-JS：Linaria
import styles from './Button.module.css';

function Button({ priority }: { priority: 'high' | 'low' }) {
  return (
    <button className={`${styles.button} ${styles[priority]}`}>
      Click me
    </button>
  );
}
```

**原因**：运行时 CSS-in-JS 在每次渲染时都要计算哈希、生成类名、插入样式表。在高频更新场景（如动画、滚动）中会造成明显卡顿。编译时方案或原子类 CSS 可以避免运行时开销。

## Gotcha 5：路由懒加载导致瀑布请求

**问题**：过度使用路由懒加载，导致页面切换时串行加载多个 Chunk，白屏时间过长。

❌ **Before（错误做法）**
```typescript
// 每个路由都懒加载，造成瀑布请求
const Home = lazy(() => import('./pages/Home'));
const Dashboard = lazy(() => import('./pages/Dashboard'));
const Settings = lazy(() => import('./pages/Settings'));

// 用户访问 /dashboard 时：加载 Dashboard chunk → Dashboard 渲染 → 
// Dashboard 内部组件再触发新的懒加载请求
```

✅ **After（正确做法）**
```typescript
// 预加载关键路由，合并相关 chunk
const Home = lazy(() => import('./pages/Home'));
const Dashboard = lazy(() => import(/* webpackPrefetch: true */ './pages/Dashboard'));

// 或使用预加载策略
function handleMouseEnter() {
  const Dashboard = import('./pages/Dashboard');  // 悬停时预加载
}

// 对强关联页面使用命名 chunk 合并
const Admin = lazy(() => import(/* webpackChunkName: "admin" */ './pages/Admin'));
const AdminUsers = lazy(() => import(/* webpackChunkName: "admin" */ './pages/AdminUsers'));
```

**原因**：懒加载减少了首屏 Bundle 大小，但过度拆分会导致页面切换时串行请求多个 Chunk。使用 `webpackPrefetch`、预加载策略、合理合并 Chunk 可以平衡首屏性能和切换性能。
