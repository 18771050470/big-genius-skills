# 技术交付物模板

> 提供可直接使用的 Markdown/代码模板。

## 交付物模板 1：LLM 集成架构设计文档

```markdown
# LLM 集成架构设计: [项目名称]

## 架构概览
[系统架构图描述]

## 组件清单

| 组件 | 职责 | 技术选型 | 部署方式 |
|------|------|----------|----------|
| API Gateway | 请求路由、限流、认证 | Kong/AWS API Gateway | 容器化 |
| LLM Proxy | 负载均衡、Fallback、缓存 | 自研/Helicone | 容器化 |
| RAG Engine | 检索增强生成 | LangChain/LlamaIndex | 容器化 |
| Prompt Manager | 版本管理、A/B 测试 | 自研 | 容器化 |

## 请求流程
1. 客户端 → API Gateway（认证+限流）
2. API Gateway → LLM Proxy（负载均衡）
3. LLM Proxy → RAG Engine（如需检索）
4. RAG Engine → Vector Store（文档检索）
5. LLM Proxy → LLM Provider（生成响应）
6. 响应 → 客户端（流式传输）

## 降级策略

| 故障场景 | 降级方案 | 预期影响 |
|----------|----------|----------|
| 主 LLM 不可用 | 切换备用模型 | 质量可能下降 10-20% |
| RAG 检索失败 | 直接调用 LLM（无检索） | 可能产生幻觉 |
| 速率限制 | 请求队列+指数退避 | 延迟增加 |
| 全部 LLM 不可用 | 返回缓存响应/静态回复 | 功能受限 |
```

## 交付物模板 2：Prompt 版本管理规范

```markdown
# Prompt 版本: [Prompt 名称] v[X.Y.Z]

## 元信息
- **创建日期**: YYYY-MM-DD
- **作者**: [姓名]
- **关联模型**: [gpt-4/claude-3/...]
- **使用场景**: ...

## Prompt 内容
```
[系统提示]

[用户提示模板]
```

## 变量定义

| 变量名 | 类型 | 必填 | 说明 | 示例 |
|--------|------|------|------|------|
| {{user_query}} | string | 是 | 用户原始问题 | "如何重置密码？" |
| {{context}} | string | 否 | 检索到的上下文 | "文档片段..." |

## 性能指标

| 指标 | 目标值 | 实测值 |
|------|--------|--------|
| 平均 Token 数 | < 500 | 450 |
| 平均响应时间 | < 2s | 1.5s |
| 用户满意度 | > 4.0 | 4.2 |

## 变更历史

| 版本 | 日期 | 变更内容 | 作者 |
|------|------|----------|------|
| v1.0.0 | 2024-01-01 | 初始版本 | Alice |
| v1.1.0 | 2024-02-01 | 增加安全过滤指令 | Bob |
```

## 交付物模板 3：RAG 系统配置

```yaml
# rag-config.yaml
rag_system:
  name: knowledge-base-rag
  
  retrieval:
    vector_store:
      type: chroma
      embedding_model: text-embedding-3-large
      collection_name: documents
      
    hybrid_search:
      enabled: true
      vector_weight: 0.7
      keyword_weight: 0.3
      
    reranker:
      enabled: true
      model: cross-encoder/ms-marco-MiniLM-L-6-v2
      top_k: 5
      
  generation:
    model: gpt-4
    temperature: 0.3
    max_tokens: 1000
    
    prompt_template: |
      基于以下参考资料回答问题：
      
      {{context}}
      
      问题：{{question}}
      
      要求：
      1. 仅基于提供的资料回答
      2. 如果资料不足，明确说明
      3. 引用来源编号 [文档1] [文档2]
      
  monitoring:
    metrics:
      - retrieval_latency
      - generation_latency
      - answer_relevance
      - context_precision
      - hallucination_rate
```

## 交付物模板 4：LLM API 调用封装

```python
# llm_client.py
from typing import AsyncGenerator, Optional
import openai
from tenacity import retry, stop_after_attempt, wait_exponential

class LLMClient:
    """LLM 调用封装，包含重试、降级、流式支持"""
    
    def __init__(
        self,
        primary_model: str = "gpt-4",
        fallback_model: str = "gpt-3.5-turbo",
        max_retries: int = 3,
        timeout: float = 30.0
    ):
        self.primary_model = primary_model
        self.fallback_model = fallback_model
        self.client = openai.AsyncOpenAI(timeout=timeout)
    
    @retry(
        stop=stop_after_attempt(3),
        wait=wait_exponential(multiplier=1, min=2, max=10)
    )
    async def chat(
        self,
        messages: list,
        stream: bool = False,
        temperature: float = 0.7,
        max_tokens: Optional[int] = None
    ) -> str | AsyncGenerator[str, None]:
        """调用 LLM，支持流式和非流式"""
        try:
            response = await self.client.chat.completions.create(
                model=self.primary_model,
                messages=messages,
                stream=stream,
                temperature=temperature,
                max_tokens=max_tokens
            )
            
            if stream:
                return self._stream_response(response)
            return response.choices[0].message.content
            
        except openai.RateLimitError:
            # 降级到备用模型
            return await self._fallback_chat(messages, stream, temperature, max_tokens)
    
    async def _fallback_chat(self, messages, stream, temperature, max_tokens):
        """备用模型调用"""
        response = await self.client.chat.completions.create(
            model=self.fallback_model,
            messages=messages,
            stream=stream,
            temperature=temperature,
            max_tokens=max_tokens
        )
        if stream:
            return self._stream_response(response)
        return response.choices[0].message.content
    
    async def _stream_response(self, response):
        """流式响应生成器"""
        async for chunk in response:
            if chunk.choices[0].delta.content:
                yield chunk.choices[0].delta.content
```
```
