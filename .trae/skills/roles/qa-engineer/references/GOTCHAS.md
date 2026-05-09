# Gotchas

> 只写 QA 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：测试用例过度依赖 UI 定位

**问题**：使用绝对 XPath 或动态 ID 定位元素，导致测试脚本频繁因 UI 微调而失败。

❌ **Before（错误做法）**
```python
# 使用绝对 XPath，极易因页面结构微调而失败
driver.find_element(By.XPATH, "/html/body/div[3]/div[1]/div[2]/button")
# 使用动态生成的 ID（如 react-id-123）
driver.find_element(By.ID, "react-id-123")
```

✅ **After（正确做法）**
```python
# 使用 data-testid 或语义化定位
driver.find_element(By.CSS_SELECTOR, "[data-testid='submit-order-btn']")
# 或基于用户可见文本（多语言时需调整）
driver.find_element(By.XPATH, "//button[contains(text(), '提交订单')]")
```

**原因**：UI 经常因设计调整而变化，但业务语义相对稳定。使用 `data-testid` 或语义化定位将测试与实现解耦，降低维护成本。

## Gotcha 2：自动化测试无等待机制

**问题**：使用固定 `time.sleep()` 等待页面加载，导致测试不稳定且执行缓慢。

❌ **Before（错误做法）**
```python
# 固定等待，既不高效也不可靠
time.sleep(5)  # 等 5 秒，希望页面加载完
assert driver.find_element(By.ID, "result").text == "成功"
```

✅ **After（正确做法）**
```python
# 显式等待，条件满足立即继续
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
element = wait.until(
    EC.text_to_be_present_in_element((By.ID, "result"), "成功")
)
```

**原因**：网络延迟和服务器响应时间不确定，固定睡眠要么太慢（浪费时间）要么太快（导致失败）。显式等待根据实际条件继续，既快又稳。

## Gotcha 3：缺陷报告缺少环境信息

**问题**：缺陷报告只描述现象，缺少复现环境和版本信息，开发人员无法复现。

❌ **Before（错误做法）**
```markdown
## Bug：登录失败
点击登录按钮后没有反应。
```

✅ **After（正确做法）**
```markdown
## Bug：登录失败 - 特定浏览器下无响应

**复现步骤**：
1. 使用 Chrome 120 / macOS 14
2. 访问 https://example.com/login
3. 输入用户名 "test@example.com"，密码 "123456"
4. 点击"登录"按钮

**实际结果**：按钮点击后无反应，页面无跳转
**期望结果**：跳转到首页

**环境信息**：
- 浏览器：Chrome 120.0.6099.129
- OS：macOS 14.2.1
- 分辨率：2560x1440
- 网络：WiFi，无代理
- 账号：test@example.com（测试账号）

**附件**：
- 录屏：login-bug.mp4
- 控制台日志：console.log
- HAR 文件：network.har
```

**原因**：缺陷的复现往往依赖特定环境（浏览器版本、OS、网络、账号状态）。完整的环境信息能将复现时间从数小时缩短到数分钟。

## Gotcha 4：回归测试范围过大或过小

**问题**：每次代码变更都执行全量回归（成本过高），或只测试修改点（遗漏关联影响）。

❌ **Before（错误做法）**
```markdown
# 方案 A：每次发布执行 2000 个用例的全量回归，耗时 3 天
# 方案 B：只测试修改的页面，其他页面不测
```

✅ **After（正确做法）**
```markdown
# 基于代码变更影响分析确定回归范围
1. 通过代码 diff 识别变更文件
2. 通过依赖分析识别受影响模块
3. 通过用例-需求追溯矩阵确定相关用例
4. 高风险区域（核心交易流程）每次必测
5. 低风险区域（静态页面）抽样测试

回归策略：
- 冒烟测试：30 个核心用例（每次必执行）
- 受影响模块：根据影响分析动态确定
- 全量回归：仅在大版本发布时执行
```

**原因**：全量回归成本随项目增长而指数上升，但过小的范围会遗漏关联缺陷。基于影响分析的精准回归能在质量和效率间取得平衡。
