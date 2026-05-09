# 抽象思维分析示例

## 示例1：电商购物车抽象

### 场景
需要设计一个通用的购物车模块，支持在淘宝、京东、亚马逊等不同电商平台上使用。

### 输入
具体实例：淘宝购物车界面、京东购物车界面、亚马逊购物车界面（包括用户操作流程、展示元素、业务规则）。

### Step 1: 收集具体实例
- **淘宝购物车**：显示商品列表，每行有商品图片、名称、单价、数量选择器（+/-）、小计；全选/取消全选；批量删除；结算按钮；优惠券入口；总价计算（含运费）。
- **京东购物车**：类似淘宝，但增加了降价通知、凑单推荐、加入关注；价格显示含预估运费。
- **亚马逊购物车（保存后）**：商品列表，有数量编辑、保存给以后、删除、结算；下方有推荐商品；无全选按钮，每个商品单独操作。

### Step 2: 识别共性特征
- **共性**：商品条目（包含基本信息和数量）、价格计算（单价×数量）、删除/移除操作、结算入口、总价显示。
- **差异维度**：全选功能的有无、是否包含推荐模块、运费计算方式、优惠券入口形式、数量选择器样式。

### Step 3: 剔除次要细节
- **保留本质**：商品条目（id、name、price、quantity）、计算方法（computeSubtotal、computeTotal）、操作（addItem、removeItem、updateQuantity）、提交（checkout）。
- **忽略细节**：图片裁剪比例、按钮颜色、动画效果、是否显示运费、推荐商品显示位置。

### Step 4: 命名与定义
- **抽象名称**：Cart
- **定义**：Cart 是一组商品的集合，每个商品带有数量和单价信息，支持增删改查操作并实时计算总价。
- **接口签名**：
```ts
interface CartItem {
  id: string;
  name: string;
  price: number;
  quantity: number;
}
interface Cart {
  items: CartItem[];
  total: number;
  addItem(productId: string, quantity: number): void;
  removeItem(itemId: string): void;
  updateQuantity(itemId: string, delta: number): void;
  clear(): void;
  checkout(): Order;
}
```

### Step 5: 验证覆盖性
- 淘宝：全选可用实现为调用 `updateQuantity` 批量操作，覆盖。
- 京东：凑单推荐属于购物车外部逻辑，不在抽象内核中，覆盖。
- 亚马逊：保存给以后属于独立状态（可另建 Wishlist），覆盖。
- 结论：全部覆盖，无遗漏。

### Step 6: 建立关系与层级
- Cart 依赖 Product（商品信息源）
- Cart 可组合 ApplyCoupon（优惠券策略）
- Order 是 Cart 的结算结果，两者为装配关系
- 可衍生出 Wishlist（保存以后）、Favorites（收藏）作为同级抽象

### Step 7: 测试可复用性
- 新实例：拼多多购物车——拼多多有砍价、拼团逻辑，但核心增删改查+结算依然适用；砍价可作为策略单独抽象。
- 结论：接口可用，仅需扩展策略模式。

### Step 8: 输出最终模型
- 以 TypeScript 接口+类实现输出，附带 UML 类图（略），并说明如何使用策略模式处理优惠、运费等差异维度。

---

## 示例2：数据导出功能抽象

### 场景
系统需要支持将数据导出为 CSV、PDF、Excel 三种格式，每种格式的生成逻辑不同，但调用方希望统一接口。

### 输入
具体实例：现有 CSV 导出代码、PDF 导出代码、Excel 导出代码（均为独立实现，含不同的参数和返回值）。

### Step 1: 收集具体实例
- **CSV 导出**：输入 DataTable，用 StringBuilder 拼接逗号分隔行，输出文件流。
- **PDF 导出**：输入 DataTable + 模板配置（纸张大小、字体），使用 PDF 库绘制表格，输出文件流。
- **Excel 导出**：输入 DataTable，使用 OpenXML 创建 Workbook、Worksheet，输出文件流。

### Step 2: 识别共性特征
- **共性**：输入均为 DataTable（结构化数据），输出均为文件流（FileStream/Buffer），均需要配置表头样式。
- **差异维度**：CSV 不需要样式配置，PDF 需要模板配置，Excel 需要命名 Sheet；性能不同（CSV 最快，PDF 最慢）。

### Step 3: 剔除次要细节
- **保留本质**：通用方法 `export(data: DataTable, options?: ExportOptions): Buffer`；ExportOptions 可包含 format 类型和格式特定配置。
- **忽略细节**：具体格式内部实现使用的第三方库、文件命名规则（由调用方决定）、压缩方式。

### Step 4: 命名与定义
- **抽象名称**：Exporter（导出器）
- **定义**：Exporter 是一个接口，接收结构化数据，输出二进制文件流，支持通过策略模式切换格式。
```ts
interface Exporter {
  export(data: DataTable, options?: ExportOptions): Promise<Buffer>;
}
type Format = 'csv' | 'pdf' | 'excel';
interface ExportOptions {
  format: Format;
  headers?: boolean;        // 是否包含表头
  additionalOptions?: any;  // 格式特定配置
}
```

### Step 5: 验证覆盖性
- CSV 导出：实现 `export` 方法，忽略 additionalOptions 中与样式无关的内容，覆盖。
- PDF 导出：additionalOptions 里放 paperSize、font 等，覆盖。
- Excel 导出：additionalOptions 里放 sheetName、columnWidths，覆盖。
- 结论：全部覆盖，无遗漏。

### Step 6: 建立关系与层级
- Exporter 是策略接口
- CsvExporter、PdfExporter、ExcelExporter 是实现
- 可增加 ExporterFactory 根据 Format 创建实例
- 若未来增加 JSON、XML 等格式，仅需新增实现类

### Step 7: 测试可复用性
- 新实例：导出为 Markdown 表格——同样输入 DataTable，输出 Markdown 字符串（可转为 Buffer）。
- 结论：接口依然适用，仅需实现 MarkdownExporter。

### Step 8: 输出最终模型
- 以接口+策略类图输出，并在文档中说明如何使用依赖注入选择格式。

---

## 反例：不该触发此 Skill 的场景

### 场景
运维人员在服务器上执行 `tail -f /var/log/nginx/access.log | grep "ERROR"` 来实时查看错误日志。

### 输入
具体指令：一个明确的命令行操作，目的是过滤日志中的 ERROR 级别记录。

### 为什么不该触发抽象思维
- 这是一个具体、精确的操作步骤，不需要提取模式或概念模型。
- 公式化的步骤直接执行即可，任何抽象都会增加不必要的复杂度（例如把 "tail + grep" 抽象成一个通用的 "日志监控器" 接口，在这个场合下只有一种使用方法）。
- 如果强行执行抽象，反而会浪费大量时间定义接口、验证覆盖性，而最终输出与原始命令没有本质区别。

### 正确的处理方式
- 直接执行命令，或封装成简单的 shell 脚本（注意：封装脚本是自动化思维，不是抽象思维）。
- 抽象思维应当保留到需要设计通用的日志收集系统（比如支持多种日志源、多种过滤条件、多种输出目标）时才使用。