# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：可解释性方案未匹配业务场景导致无效

**问题**：为所有模型统一使用 SHAP/LIME 解释，未考虑业务场景对解释深度和形式的要求，导致解释结果无法被业务方理解或使用。

❌ **Before（错误做法）**
```python
# 对所有模型使用同样的解释方法
import shap

explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(X_test)

# 生成复杂的力图和瀑布图
shap.force_plot(explainer.expected_value, shap_values[0], X_test.iloc[0])
# 业务方看不懂，无法用于客户沟通
```

✅ **After（正确做法）**
```python
def generate_explanation(model, input_data, scenario):
    """根据场景生成合适的解释"""
    
    if scenario == "customer_facing":
        # 面向客户：简单、直观的解释
        top_features = get_top_features(model, input_data, n=3)
        return {
            "type": "natural_language",
            "content": f"您的申请被拒绝，主要原因是：{top_features[0]['reason']}",
            "factors": [
                {"factor": f["name"], "impact": "高" if f["importance"] > 0.3 else "中"}
                for f in top_features
            ]
        }
    
    elif scenario == "regulatory_audit":
        # 监管审计：详细、可追溯的解释
        return {
            "type": "technical_report",
            "shap_values": shap_values,
            "feature_contributions": feature_contributions,
            "decision_path": model.decision_path(input_data),
            "confidence_intervals": confidence_intervals
        }
    
    elif scenario == "model_developer":
        # 模型开发：全局解释
        return {
            "type": "global_analysis",
            "feature_importance": model.feature_importances_,
            "partial_dependence": pdp_results,
            "interaction_effects": interaction_results
        }
```

**原因**：不同场景对可解释性的要求完全不同。面向客户需要自然语言解释，监管审计需要技术细节，模型开发需要全局分析。必须根据场景选择合适的解释方法和呈现形式。

## Gotcha 2：算法公平性评估忽略间接歧视

**问题**：只检查直接使用的敏感属性（如性别、种族），未考虑代理变量（如邮编、教育背景）可能带来的间接歧视。

❌ **Before（错误做法）**
```python
# 只检查直接敏感属性
sensitive_attrs = ['gender', 'race']
for attr in sensitive_attrs:
    if attr in features:
        print(f"⚠️ 模型使用了敏感属性: {attr}")

# 但未检查：邮编（与种族高度相关）、教育背景（与性别相关）
```

✅ **After（正确做法）**
```python
from scipy.stats import chi2_contingency

def detect_proxy_variables(df, sensitive_attr, threshold=0.3):
    """检测与敏感属性高度相关的代理变量"""
    proxies = []
    
    for col in df.columns:
        if col == sensitive_attr:
            continue
        
        # 计算 Cramér's V（类别变量关联度）
        contingency = pd.crosstab(df[col], df[sensitive_attr])
        chi2, _, _, _ = chi2_contingency(contingency)
        n = contingency.sum().sum()
        cramers_v = np.sqrt(chi2 / (n * (min(contingency.shape) - 1)))
        
        if cramers_v > threshold:
            proxies.append({
                "feature": col,
                "correlation": cramers_v,
                "type": "proxy"
            })
    
    return proxies

# 检查所有特征的代理风险
proxy_features = detect_proxy_variables(df, sensitive_attr='race')
for proxy in proxy_features:
    print(f"⚠️ 代理变量风险: {proxy['feature']} (Cramér's V: {proxy['correlation']:.3f})")
```

**原因**：即使模型不直接使用敏感属性，代理变量（与敏感属性高度相关的特征）仍可能导致间接歧视。必须通过统计方法（如 Cramér's V）检测代理变量，并在特征工程阶段处理。

## Gotcha 3：合规检查只在模型上线前做一次

**问题**：只在模型开发和上线阶段进行合规审查，未建立持续监控机制，导致模型在生产环境退化后违反合规要求。

❌ **Before（错误做法）**
```python
# 只在上线前审查
if model_passes_compliance_check(model):
    deploy(model)
# 上线后不再检查合规性
```

✅ **After（正确做法）**
```python
class ContinuousComplianceMonitor:
    """持续合规监控"""
    
    def __init__(self):
        self.checks = {
            "fairness": self.check_fairness,
            "explainability": self.check_explainability,
            "data_privacy": self.check_data_privacy,
            "model_drift": self.check_model_drift
        }
    
    def check_fairness(self, model, data):
        """公平性持续监控"""
        metric_frame = MetricFrame(
            metrics=accuracy_score,
            y_true=data.y,
            y_pred=model.predict(data.X),
            sensitive_features=data.sensitive_attrs
        )
        
        max_disparity = metric_frame.difference(method='between_groups')
        if max_disparity > 0.05:
            self.trigger_alert(
                type="fairness_violation",
                severity="high",
                details={"disparity": max_disparity}
            )
    
    def periodic_check(self, model, data, frequency='daily'):
        """定期检查"""
        for check_name, check_func in self.checks.items():
            try:
                result = check_func(model, data)
                self.log_check_result(check_name, result)
            except Exception as e:
                self.trigger_alert(
                    type="check_failed",
                    severity="medium",
                    details={"check": check_name, "error": str(e)}
                )
```

**原因**：合规不是一次性的检查，而是持续的要求。模型在生产环境中会面临数据分布变化、概念漂移等问题，可能导致原本合规的模型变得不合规。必须建立持续监控和定期审计机制。

## Gotcha 4：模型卡片信息不完整导致无法审计

**问题**：模型卡片只记录了基本性能指标，未记录训练数据细节、已知限制、伦理考量等关键信息，导致后续审计和问责困难。

❌ **Before（错误做法）**
```markdown
# Model Card

## 模型信息
- 名称: Fraud Detection Model
- 版本: v1.0
- 准确率: 95%
```

✅ **After（正确做法）**
```markdown
# Model Card

## 模型信息
- 名称: Fraud Detection Model
- 版本: v1.0
- 创建日期: 2024-01-15
- 创建团队: Risk AI Team
- 模型类型: XGBoost Classifier

## 预期用途
- **主要用途**: 识别信用卡交易中的欺诈行为
- **适用场景**: 在线支付实时风控
- **不适用场景**: 
  - 非支付场景（如贷款审批）
  - 低于 100 元的交易（准确率不足）

## 训练数据
- **数据集**: Transaction Dataset v3.2
- **时间范围**: 2022-01 ~ 2023-06
- **样本数**: 10M（正负比例 1:100）
- **数据来源**: 内部交易日志
- **预处理**: 
  - 移除了 PII（姓名、身份证号）
  - 对金额做了 log 变换
  - 对类别特征做了 Target Encoding

## 性能指标

| 指标 | 整体 | 男性 | 女性 | 年龄<30 | 年龄>=30 |
|------|------|------|------|---------|----------|
| 准确率 | 0.95 | 0.96 | 0.94 | 0.93 | 0.96 |
| 召回率 | 0.85 | 0.87 | 0.83 | 0.80 | 0.88 |

## 已知限制
- 对新型欺诈模式（如 AI 生成的虚假交易）检测能力不足
- 在节假日期间误报率上升 15%
- 对跨境交易的特征覆盖不完整

## 伦理考量
- 模型未直接使用性别、种族等敏感属性
- 但使用了邮编作为特征，可能存在地域偏见
- 对低收入群体的误报率较高（需要人工复核机制）

## 更新历史
| 版本 | 日期 | 变更 | 作者 |
|------|------|------|------|
| v1.0 | 2024-01-15 | 初始版本 | Alice |
```

**原因**：模型卡片是 AI 治理的核心文档，是审计、问责、复现的基础。必须包含完整的模型信息、数据详情、性能指标（按子群体）、已知限制、伦理考量和更新历史。
