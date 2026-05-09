# 技术交付物模板

> 提供可直接使用的 Markdown/代码模板。

## 交付物模板 1：ML 模型开发文档

```markdown
# ML 模型开发文档: [模型名称]

## 问题定义
- **任务类型**: [分类/回归/聚类/...]
- **业务目标**: ...
- **成功指标**: ...

## 数据说明

| 数据集 | 样本数 | 特征数 | 时间范围 | 存储位置 |
|--------|--------|--------|----------|----------|
| 训练集 | 10000 | 50 | 2023-01 ~ 2023-06 | s3://... |
| 验证集 | 2000 | 50 | 2023-07 | s3://... |
| 测试集 | 2000 | 50 | 2023-08 | s3://... |

## 特征工程

| 特征名 | 类型 | 来源 | 变换 | 说明 |
|--------|------|------|------|------|
| feature1 | 数值 | 原始 | 标准化 | ... |
| feature2 | 类别 | 原始 | One-Hot | ... |
| feature3 | 数值 | 派生 | log变换 | ... |

## 模型对比

| 模型 | 准确率 | 精确率 | 召回率 | F1 | AUC | 训练时间 |
|------|--------|--------|--------|----|-----|----------|
| Logistic Regression | 0.85 | 0.83 | 0.80 | 0.81 | 0.90 | 10s |
| Random Forest | 0.92 | 0.91 | 0.89 | 0.90 | 0.95 | 2min |
| XGBoost | 0.94 | 0.93 | 0.92 | 0.92 | 0.97 | 5min |

## 最终模型
- **模型**: XGBoost
- **关键超参数**: ...
- **特征重要性 Top 5**: ...

## 部署信息
- **部署方式**: [REST API/批处理/边缘]
- **推理延迟**: P99 < 50ms
- **资源需求**: 2 CPU, 4GB RAM
```

## 交付物模板 2：特征工程规范

```markdown
# 特征工程规范: [特征集名称]

## 特征分类

### 原始特征（Raw）
| 特征名 | 数据类型 | 来源表 | 字段 | 说明 |
|--------|----------|--------|------|------|
| user_age | INT | users | age | 用户年龄 |
| order_amount | FLOAT | orders | amount | 订单金额 |

### 派生特征（Derived）
| 特征名 | 计算方式 | 依赖特征 | 更新频率 |
|--------|----------|----------|----------|
| avg_order_amount_30d | AVG(amount) OVER 30d | order_amount | 每日 |
| order_frequency_7d | COUNT(*) OVER 7d | order_id | 每日 |

### 编码特征（Encoded）
| 特征名 | 编码方式 | 原特征 | 维度 |
|--------|----------|--------|------|
| category_encoded | Target Encoding | category | 1 |
| city_onehot | One-Hot | city | 100 |

## 特征存储配置

```yaml
feature_view:
  name: user_behavior_features
  entities: [user_id]
  ttl: 24h
  
  features:
    - name: avg_order_amount_30d
      type: FLOAT
      transformation:
        type: aggregation
        function: AVG
        column: order_amount
        window: 30d
    
    - name: order_frequency_7d
      type: INT
      transformation:
        type: aggregation
        function: COUNT
        window: 7d
```

## 质量监控

| 检查项 | 阈值 | 告警方式 |
|--------|------|----------|
| 缺失率 | < 5% | 邮件 |
| 异常值比例 | < 1% | 邮件 |
| 分布漂移 | PSI < 0.2 | 短信 |
```

## 交付物模板 3：模型评估报告

```markdown
# 模型评估报告: [模型名称] v[X.Y.Z]

## 评估环境
- **评估日期**: YYYY-MM-DD
- **评估数据集**: [数据集名称]
- **样本数**: [N]

## 性能指标

| 指标 | 值 | 基准 | 状态 |
|------|----|------|------|
| Accuracy | 0.92 | 0.85 | ✅ |
| Precision | 0.91 | 0.80 | ✅ |
| Recall | 0.89 | 0.80 | ✅ |
| F1 Score | 0.90 | 0.82 | ✅ |
| AUC-ROC | 0.95 | 0.90 | ✅ |
| AUC-PR | 0.88 | 0.85 | ✅ |

## 混淆矩阵

| 实际\预测 | 正例 | 负例 |
|-----------|------|------|
| 正例 | 890 | 110 |
| 负例 | 90 | 910 |

## 公平性评估

| 群体 | 准确率 | 差异 | 状态 |
|------|--------|------|------|
| 群体A | 0.93 | - | ✅ |
| 群体B | 0.90 | -0.03 | ✅ |
| 群体C | 0.85 | -0.08 | ⚠️ |

## 结论
- [ ] 模型通过评估，可以部署
- [ ] 模型未通过评估，需要优化（原因：...）
```

## 交付物模板 4：MLOps 流水线定义

```yaml
# ml-pipeline.yaml
pipeline:
  name: model-training-pipeline
  version: "1.0.0"
  
  stages:
    data_ingestion:
      type: batch
      source: s3://data/raw/
      output: raw_data
      validation:
        - schema_check
        - null_check
        - range_check
      
    data_preprocessing:
      type: transform
      input: raw_data
      steps:
        - missing_value_imputation
        - outlier_handling
        - feature_encoding
        - feature_scaling
      output: processed_data
      
    feature_engineering:
      type: transform
      input: processed_data
      steps:
        - feature_creation
        - feature_selection
        - feature_validation
      output: feature_set
      
    model_training:
      type: training
      input: feature_set
      algorithm: xgboost
      hyperparameters:
        max_depth: 6
        learning_rate: 0.1
        n_estimators: 100
      cross_validation:
        method: stratified_kfold
        folds: 5
      output: trained_model
      
    model_evaluation:
      type: evaluation
      input: trained_model
      metrics:
        - accuracy
        - precision
        - recall
        - f1
        - auc_roc
        - fairness_metrics
      thresholds:
        accuracy: "> 0.85"
        fairness_disparity: "< 0.1"
      
    model_deployment:
      type: deployment
      input: trained_model
      strategy: canary
      canary_percentage: 10
      rollback_trigger:
        - accuracy_drop > 0.05
        - latency_p99 > 100ms
```
