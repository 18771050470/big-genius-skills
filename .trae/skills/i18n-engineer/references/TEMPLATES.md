# 国际化(i18n)工程师技术交付物模板

## 翻译文件模板

```json
{
  "common": {
    "confirm": "确定",
    "cancel": "取消",
    "save": "保存",
    "delete": "删除",
    "loading": "加载中..."
  },
  "order": {
    "title": "订单管理",
    "submit": {
      "button": "提交订单",
      "success": "订单提交成功",
      "error": "订单提交失败，请重试"
    },
    "status": {
      "pending": "待处理",
      "paid": "已支付",
      "shipped": "已发货",
      "completed": "已完成"
    }
  },
  "validation": {
    "required": "{{field}} 不能为空",
    "email": "请输入有效的邮箱地址",
    "minLength": "{{field}} 至少需要 {{min}} 个字符"
  }
}
```

## RTL 检查清单模板

```markdown
## RTL 适配检查清单

### 布局检查
- [ ] 使用 CSS 逻辑属性（inline-start/end）
- [ ] Flexbox/Grid 布局在 RTL 下正确
- [ ] 文本对齐正确（start/end 替代 left/right）
- [ ] 边距和填充使用逻辑属性

### 组件检查
- [ ] 按钮图标方向正确
- [ ] 输入框光标位置正确
- [ ] 下拉菜单方向正确
- [ ] 轮播图滑动方向正确

### 内容检查
- [ ] 文本方向正确（dir="rtl"）
- [ ] 数字和英文混合显示正确
- [ ] 标点符号位置正确
- [ ] 图标方向性处理（箭头/手势）

### 测试检查
- [ ] 阿拉伯语界面完整测试
- [ ] 希伯来语界面完整测试
- [ ] 文本长度最长情况测试
- [ ] 混合 LTR/RTL 内容测试
```
