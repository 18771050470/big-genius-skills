# 技术交付物模板

> 提供可直接使用的 Markdown/代码模板。

## 交付物模板 1：AI 架构决策记录（AI-ADR）

```markdown
# AI-ADR-XXX: [决策标题]

## 状态
- 提议 / 已通过 / 已废弃

## 背景
[描述促使做出此决策的问题或需求]

## 决策
[明确描述做出的架构决策]

## 候选方案对比

| 维度 | 方案A: [名称] | 方案B: [名称] | 方案C: [名称] |
|------|--------------|--------------|--------------|
| 延迟要求 | 满足/不满足 | 满足/不满足 | 满足/不满足 |
| 吞吐量 | 支持 QPS | 支持 QPS | 支持 QPS |
| 模型复杂度 | 高/中/低 | 高/中/低 | 高/中/低 |
| 运维成本 | 高/中/低 | 高/中/低 | 高/中/低 |
| 扩展性 | 优/良/差 | 优/良/差 | 优/良/差 |
| 训练-服务一致性 | 是/否 | 是/否 | 是/否 |
| 风险 | [描述] | [描述] | [描述] |

## 影响
- **正面影响**：...
- **负面影响**：...
- **风险**：...

## 相关决策
- [AI-ADR-XXX: 相关决策]
```

## 交付物模板 2：模型服务接口规范

```markdown
# Model API Spec: [模型名称]

## 基本信息
- **模型版本**: vX.Y.Z
- **部署环境**: [dev/staging/prod]
- **服务地址**: `https://api.example.com/v1/models/{model_name}/predict`

## 输入规范

### 请求格式
```json
{
  "instances": [
    {
      "feature1": "value1",
      "feature2": 123.45,
      "feature3": [1, 2, 3]
    }
  ]
}
```

### 字段说明

| 字段 | 类型 | 必填 | 说明 | 取值范围 |
|------|------|------|------|----------|
| feature1 | string | 是 | 特征说明 | 枚举值: A, B, C |
| feature2 | float | 是 | 特征说明 | [0.0, 1.0] |
| feature3 | array | 否 | 特征说明 | 长度: 3-10 |

## 输出规范

### 响应格式
```json
{
  "predictions": [
    {
      "label": "positive",
      "probability": 0.95,
      "confidence": 0.92
    }
  ],
  "model_version": "v1.2.3",
  "inference_time_ms": 12.5
}
```

## 错误码

| 状态码 | 说明 | 处理建议 |
|--------|------|----------|
| 400 | 输入格式错误 | 检查请求体是否符合 schema |
| 422 | 特征值非法 | 检查特征取值范围 |
| 429 | 请求限流 | 降低请求频率 |
| 503 | 模型未就绪 | 等待模型加载完成 |
```

## 交付物模板 3：MLOps 流水线配置

```yaml
# mlops-pipeline.yaml
pipeline:
  name: fraud-detection-pipeline
  version: "1.0.0"
  
  stages:
    - name: data_ingestion
      type: batch
      schedule: "0 2 * * *"  # 每天凌晨2点
      output: raw_data
      
    - name: feature_engineering
      type: transform
      input: raw_data
      output: feature_store
      dependencies:
        - feast>=0.35
      
    - name: model_training
      type: training
      input: feature_store
      output: model_artifact
      framework: xgboost
      hyperparameters:
        max_depth: 6
        learning_rate: 0.1
      
    - name: model_evaluation
      type: evaluation
      input: model_artifact
      metrics:
        - accuracy > 0.85
        - precision > 0.80
        - recall > 0.75
        - fairness_disparity < 0.1
      
    - name: model_deployment
      type: deployment
      input: model_artifact
      strategy: canary
      canary_percentage: 10
      
    - name: model_monitoring
      type: monitoring
      input: deployed_model
      alerts:
        - metric: accuracy < 0.80
          action: rollback
        - metric: drift > 0.1
          action: retrain
```

## 交付物模板 4：模型卡片（Model Card）

```markdown
# Model Card: [模型名称]

## 模型详情
- **开发者**: [团队/组织]
- **模型日期**: YYYY-MM-DD
- **模型版本**: vX.Y.Z
- **模型类型**: [分类/回归/生成/...]
- **框架**: [TensorFlow/PyTorch/...]

## 预期用途
- **主要用途**: ...
- **适用场景**: ...
- **不适用场景**: ...

## 训练数据
- **数据集**: ...
- **数据规模**: ...
- **时间范围**: ...
- **预处理**: ...

## 评估结果

| 指标 | 训练集 | 验证集 | 测试集 |
|------|--------|--------|--------|
| Accuracy | 0.95 | 0.92 | 0.91 |
| Precision | 0.93 | 0.90 | 0.89 |
| Recall | 0.91 | 0.88 | 0.87 |
| F1 Score | 0.92 | 0.89 | 0.88 |

## 公平性评估

| 群体 | 准确率 | 差异 |
|------|--------|------|
| 群体A | 0.92 | - |
| 群体B | 0.89 | -0.03 |

## 已知限制
- ...
- ...

## 伦理考量
- ...
```
