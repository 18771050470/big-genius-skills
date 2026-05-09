# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：数据泄露（Data Leakage）导致评估结果虚高

**问题**：训练数据中包含了目标变量的信息，或预处理时使用了全量数据的统计信息，导致模型在测试集上表现异常好，但生产环境表现很差。

❌ **Before（错误做法）**
```python
# 错误：先标准化再划分训练/测试集
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)  # 用了全量数据的均值和标准差！

X_train, X_test = train_test_split(X_scaled, test_size=0.2)
model.fit(X_train, y_train)
# 测试集分数虚高，因为 scaler 已经"看到"了测试数据
```

✅ **After（正确做法）**
```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import cross_val_score

# 正确：使用 Pipeline，确保预处理在交叉验证的每一折内独立进行
pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('model', RandomForestClassifier())
])

# 划分原始数据
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# 交叉验证（预处理在训练折内 fit，在测试折内 transform）
scores = cross_val_score(pipeline, X_train, y_train, cv=5)

# 最终评估
pipeline.fit(X_train, y_train)
test_score = pipeline.score(X_test, y_test)
```

**原因**：数据泄露是 ML 中最隐蔽也最常见的错误。任何在划分训练/测试集之前使用全量数据信息的操作（标准化、特征选择、缺失值填充）都会导致泄露。必须使用 Pipeline 确保预处理步骤在交叉验证的每一折内独立进行。

## Gotcha 2：类别不平衡导致模型偏向多数类

**问题**：训练数据中类别分布极不均匀（如 95% 负例，5% 正例），模型倾向于预测多数类，导致少数类召回率极低。

❌ **Before（错误做法）**
```python
# 直接使用原始数据训练
model = RandomForestClassifier()
model.fit(X_train, y_train)

# 准确率 95%，但正例召回率可能只有 10%
print(classification_report(y_test, model.predict(X_test)))
```

✅ **After（正确做法）**
```python
from imblearn.over_sampling import SMOTE
from imblearn.pipeline import Pipeline as ImbPipeline

# 方法1：使用采样技术
pipeline = ImbPipeline([
    ('smote', SMOTE(random_state=42)),  # 过采样少数类
    ('model', RandomForestClassifier(class_weight='balanced'))  # 类别权重
])

# 方法2：调整决策阈值
model.fit(X_train, y_train)
y_proba = model.predict_proba(X_test)[:, 1]

# 找到最佳阈值（如 F1 分数最高）
from sklearn.metrics import f1_score
thresholds = np.arange(0.1, 0.9, 0.05)
best_threshold = max(thresholds, key=lambda t: f1_score(y_test, y_proba > t))

# 方法3：使用合适的评估指标
print(classification_report(y_test, y_proba > best_threshold))
# 关注 Precision、Recall、F1、AUC-ROC、AUC-PR，而非 Accuracy
```

**原因**：在不平衡数据上，准确率（Accuracy）是误导性指标。必须通过类别权重、采样技术、阈值调整等手段平衡模型，并使用 Precision、Recall、F1、AUC-PR 等更合适的指标评估。

## Gotcha 3：未做特征重要性验证导致过拟合

**问题**：使用高维特征或自动特征工程生成的特征未经筛选，模型在训练集上过拟合，泛化能力差。

❌ **Before（错误做法）**
```python
# 生成大量特征，不做筛选
from feature_engine import encoding, imputation

df_encoded = encoding.OneHotEncoder().fit_transform(df)
df_poly = PolynomialFeatures(degree=3).fit_transform(df_encoded)  # 特征爆炸！

model = RandomForestClassifier()
model.fit(df_poly, y)  # 过拟合风险极高
```

✅ **After（正确做法）**
```python
from sklearn.feature_selection import SelectKBest, mutual_info_classif
from sklearn.model_selection import cross_val_score

# 1. 特征重要性筛选
selector = SelectKBest(mutual_info_classif, k=50)  # 保留 Top 50
X_selected = selector.fit_transform(X_train, y_train)

# 2. 正则化模型
from sklearn.linear_model import LogisticRegression
model = LogisticRegression(penalty='l1', C=0.1)  # L1 正则化自动特征选择

# 3. 交叉验证评估泛化能力
scores = cross_val_score(model, X_selected, y_train, cv=5)
print(f"交叉验证分数: {scores.mean():.3f} (+/- {scores.std():.3f})")

# 4. 学习曲线分析
from sklearn.model_selection import learning_curve
train_sizes, train_scores, val_scores = learning_curve(
    model, X_selected, y_train, cv=5, 
    train_sizes=np.linspace(0.1, 1.0, 10)
)
# 如果训练分数 >> 验证分数，说明过拟合
```

**原因**：特征过多（尤其是高基数类别特征的 One-Hot 编码、多项式特征）会导致维度灾难和过拟合。必须通过特征选择、正则化、交叉验证和学习曲线来确保模型的泛化能力。

## Gotcha 4：模型未版本化导致无法复现

**问题**：模型训练代码、数据、超参数未做版本管理，数周后无法复现相同的模型，排查问题困难。

❌ **Before（错误做法）**
```python
# 训练模型后直接保存
model.fit(X_train, y_train)
joblib.dump(model, 'model.pkl')  # 只有模型文件，无版本信息

# 数周后...
model = joblib.load('model.pkl')  # 不知道这是哪个版本，用什么数据训练的
```

✅ **After（正确做法）**
```python
import mlflow
from datetime import datetime

# 启动 MLflow 实验
mlflow.set_experiment("fraud-detection")

with mlflow.start_run():
    # 记录参数
    mlflow.log_params({
        "model_type": "RandomForest",
        "n_estimators": 100,
        "max_depth": 10,
        "random_state": 42
    })
    
    # 记录数据版本
    mlflow.log_param("data_version", "v2.1.0")
    mlflow.log_param("data_hash", hashlib.md5(X_train.tobytes()).hexdigest())
    
    # 训练
    model.fit(X_train, y_train)
    
    # 记录指标
    mlflow.log_metrics({
        "train_accuracy": model.score(X_train, y_train),
        "test_accuracy": model.score(X_test, y_test),
        "cv_mean": scores.mean(),
        "cv_std": scores.std()
    })
    
    # 记录模型 + 环境
    mlflow.sklearn.log_model(
        model, 
        "model",
        registered_model_name="fraud-detection-model"
    )
    mlflow.log_artifact("requirements.txt")
    mlflow.log_artifact("train.py")
```

**原因**：ML 实验的可复现性至关重要。必须通过 MLflow 等工具记录完整的实验信息：代码版本、数据版本、超参数、指标、依赖环境，确保任何模型都可以被完整复现。
