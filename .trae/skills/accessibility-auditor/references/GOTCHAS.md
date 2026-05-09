# Gotchas

> 只写无障碍审核容易犯错的**非显而易见的事实**。通用知识不要写。

## Gotcha 1：过度使用 ARIA 反而降低可访问性

**问题**：开发者不了解原生 HTML 的无障碍支持，过度使用 ARIA 属性，导致屏幕阅读器播报混乱。

❌ **Before（错误做法）**
```html
<!-- 过度使用 ARIA，原生按钮反而更简单 -->
<div role="button" tabindex="0" aria-label="提交"
     onclick="submit()" onkeydown="if(event.key==='Enter')submit()">
  提交
</div>

<!-- 复杂的导航 ARIA -->
<div role="navigation" aria-label="主导航">
  <div role="list">
    <div role="listitem">
      <a href="/" role="link">首页</a>
    </div>
  </div>
</div>
```

✅ **After（正确做法）**
```html
<!-- 原生按钮自带无障碍支持 -->
<button type="submit">提交</button>

<!-- 原生导航无需多余 ARIA -->
<nav aria-label="主导航">
  <ul>
    <li><a href="/">首页</a></li>
  </ul>
</nav>

<!-- 只有原生 HTML 无法满足时才用 ARIA -->
<!-- 例如：自定义下拉框 -->
<div class="custom-select" role="combobox" aria-expanded="false" aria-haspopup="listbox">
  <input type="text" aria-autocomplete="list" aria-controls="listbox-1">
  <ul id="listbox-1" role="listbox" aria-label="选项">
    <li role="option">选项 1</li>
  </ul>
</div>
```

**原因**：ARIA 的第一原则是"能不用就不用"。原生 HTML 元素（button、nav、ul）自带完整的无障碍支持，包括键盘交互、焦点管理、屏幕阅读器播报。过度使用 ARIA 容易出错且增加维护成本。

## Gotcha 2：焦点管理缺失导致键盘用户迷路

**问题**：模态框、下拉菜单、单页应用切换时焦点丢失或陷阱，键盘用户无法操作。

❌ **Before（错误做法）**
```javascript
// 打开模态框，焦点不管理
function openModal() {
    document.getElementById('modal').style.display = 'block';
    // 焦点仍在触发按钮，用户 Tab 键在模态框后面游走
}

// 关闭模态框，焦点不恢复
function closeModal() {
    document.getElementById('modal').style.display = 'none';
    // 焦点丢失，用户不知道在哪
}
```

✅ **After（正确做法）**
```javascript
let lastFocusedElement = null;

function openModal() {
    lastFocusedElement = document.activeElement;
    const modal = document.getElementById('modal');
    modal.style.display = 'block';
    modal.setAttribute('aria-modal', 'true');
    
    // 焦点移到模态框内第一个可聚焦元素
    const firstFocusable = modal.querySelector('button, [href], input, select, textarea');
    firstFocusable?.focus();
    
    // 限制焦点在模态框内
    modal.addEventListener('keydown', trapFocus);
}

function closeModal() {
    const modal = document.getElementById('modal');
    modal.style.display = 'none';
    modal.removeEventListener('keydown', trapFocus);
    
    // 焦点回到触发元素
    lastFocusedElement?.focus();
}

function trapFocus(e) {
    if (e.key !== 'Tab') return;
    
    const focusableElements = modal.querySelectorAll(
        'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
    );
    const first = focusableElements[0];
    const last = focusableElements[focusableElements.length - 1];
    
    if (e.shiftKey && document.activeElement === first) {
        e.preventDefault();
        last.focus();
    } else if (!e.shiftKey && document.activeElement === last) {
        e.preventDefault();
        first.focus();
    }
}
```

**原因**：键盘用户（包括视障用户和运动障碍用户）依赖焦点导航。焦点丢失会让他们"迷路"，不知道自己在页面的哪个位置。必须管理焦点：打开时移入、关闭时恢复、限制在模态框内。

## Gotcha 3：图片替代文本描述不当

**问题**：所有图片都使用相同的 alt="图片"，或装饰性图片有冗长的 alt，导致屏幕阅读器用户体验差。

❌ **Before（错误做法）**
```html
<!-- 所有图片都是 "图片" -->
<img src="product.jpg" alt="图片">
<img src="icon-search.png" alt="图片">
<img src="banner.jpg" alt="图片">

<!-- 装饰性图片有冗长描述 -->
<img src="decoration-line.png" alt="一条蓝色的波浪线分隔符，宽度 100%，高度 2 像素">
```

✅ **After（正确做法）**
```html
<!-- 信息性图片：描述图片内容 -->
<img src="product.jpg" alt="红色无线蓝牙耳机，带充电盒">

<!-- 功能性图片（如图标）：描述功能 -->
<img src="icon-search.png" alt="搜索">

<!-- 装饰性图片：alt 为空，屏幕阅读器跳过 -->
<img src="decoration-line.png" alt="">

<!-- 复杂图表：提供详细描述 -->
<img src="sales-chart.png" alt="2024 年销售趋势图，详细数据见下方表格">
<table>
  <caption>2024 年销售数据</caption>
  <!-- 表格数据 -->
</table>

<!-- 包含文字的图片：alt 包含图片中的文字 -->
<img src="infographic.png" alt="信息图：2024 年用户增长 150%，收入增长 80%">
```

**原因**：屏幕阅读器会朗读 alt 文本。"图片"对用户无意义，装饰性图片的冗长描述浪费时间。正确的 alt 文本应：信息性图片描述内容、功能性图片描述功能、装饰性图片 alt 为空。

## Gotcha 4：表单错误提示仅通过颜色传达

**问题**：表单验证错误仅用红色边框标识，色盲用户无法感知，屏幕阅读器用户不知道错误内容。

❌ **Before（错误做法）**
```html
<!-- 仅用颜色标识错误 -->
<input type="email" class="error-border">  <!-- 红色边框 -->
<span class="error-text">邮箱格式错误</span>  <!-- 红色文字 -->
```

✅ **After（正确做法）**
```html
<!-- 颜色 + 图标 + 文字 + ARIA -->
<div class="form-field">
  <label for="email">邮箱</label>
  <input 
    type="email" 
    id="email"
    aria-invalid="true"
    aria-describedby="email-error"
    class="error-border"
  >
  <span id="email-error" class="error-text" role="alert">
    <svg aria-hidden="true" class="error-icon">...</svg>
    邮箱格式错误：请输入有效的邮箱地址，如 example@domain.com
  </span>
</div>

<!-- 提交时的错误汇总 -->
<div role="alert" aria-live="polite">
  <h2>表单提交失败，请修正以下错误：</h2>
  <ul>
    <li><a href="#email">邮箱：格式错误</a></li>
    <li><a href="#password">密码：长度至少 8 位</a></li>
  </ul>
</div>
```

**原因**：约 8% 男性有某种形式的色盲。仅依赖颜色传达信息会排斥这部分用户。必须使用多种方式：颜色、图标、文字、ARIA 状态，确保所有用户都能感知错误。
