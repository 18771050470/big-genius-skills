# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：营销语言而非技术语言

**问题**：使用空洞的营销词汇描述技术产品，开发者不信任且反感。

❌ **Before（错误做法）**
"我们的 revolutionary AI-powered platform 是 industry-leading 的解决方案，提供 unparalleled performance 和 cutting-edge innovation。"

✅ **After（正确做法）**
"我们的推理引擎在ResNet-50上达到每秒10,000次推理，延迟P99 < 50ms。支持ONNX、TensorRT和OpenVINO格式，可在NVIDIA T4和A100上运行。"

**原因**：开发者对营销话术高度敏感，空洞的形容词会降低可信度。用具体的技术指标、benchmark数据、代码示例说话，才能赢得开发者信任。

---

## Gotcha 2：忽视开发者旅程的早期阶段

**问题**：只关注高级功能和架构设计的内容，忽视了新开发者的上手体验。

❌ **Before（错误做法）**
所有内容都是深度技术文章（如"分布式事务的实现原理"），没有快速开始指南，新开发者不知道从何入手。

✅ **After（正确做法）**
内容覆盖完整开发者旅程：快速开始（5分钟上手）→ 基础教程（核心概念）→ 深度文章（高级特性）→ 架构案例（生产实践）。

**原因**：开发者旅程是一个漏斗，大部分用户停留在早期阶段。如果新开发者无法快速获得价值，就不会进入深度使用阶段。

---

## Gotcha 3：示例代码不可运行

**问题**：提供的代码示例有bug、缺少依赖、或假设了不存在的环境，开发者复制后无法运行。

❌ **Before（错误做法）**
```python
# 未提供导入语句、未定义变量、缺少错误处理
result = model.predict(data)
print(result)
```

✅ **After（正确做法）**
```python
# 完整可运行的示例
import requests

API_KEY = "your-api-key"  # 从 https://dashboard.example.com 获取
API_URL = "https://api.example.com/v1/predict"

def predict(text: str):
    headers = {"Authorization": f"Bearer {API_KEY}"}
    payload = {"input": text}
    
    response = requests.post(API_URL, json=payload, headers=headers)
    response.raise_for_status()
    return response.json()["result"]

# 示例
if __name__ == "__main__":
    result = predict("Hello, world!")
    print(f"Prediction: {result}")
```

**原因**：开发者复制示例代码是为了快速验证。不可运行的示例会浪费开发者时间，严重损害产品印象。每个示例都应是完整的、可复制的、经过测试的。

---

## Gotcha 4：只推广不倾听

**问题**：只向开发者推送内容，不收集反馈，不了解开发者的真实需求和痛点。

❌ **Before（错误做法）**
每月发布4篇博客、2个视频，但从不回复评论、不收集反馈、不跟踪内容效果。内容主题由产品团队决定，而非开发者需求。

✅ **After（正确做法）**
建立反馈闭环：定期调研开发者需求→根据需求规划内容→发布后跟踪效果（阅读量、完播率、转化率）→收集评论和反馈→迭代优化。社区中的问题也是内容的源泉。

**原因**：开发者关系是双向的。只推广不倾听会让内容脱离开发者实际需求，最终失去受众。成功的DevRel团队将开发者反馈作为产品改进的重要输入。
