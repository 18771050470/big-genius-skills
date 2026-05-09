# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：标注指南模糊导致标注者间一致性低

**问题**：标注指南使用模糊词汇（如"适当"、"合理"），不同标注者对同一数据的标注结果差异巨大，导致标注质量不可信。

❌ **Before（错误做法）**
```markdown
# 情感标注指南

## 规则
- 如果评论是正面的，标注为"正面"
- 如果评论是负面的，标注为"负面"
- 如果评论情感不明显，标注为"中性"

## 示例
- "这个产品很好" → 正面
- "这个产品很差" → 负面
```

✅ **After（正确做法）**
```markdown
# 情感标注指南 v2.1

## 定义
- **正面**：明确表达满意、推荐、赞扬，或包含正面词汇（好、棒、满意、推荐）
- **负面**：明确表达不满、抱怨、批评，或包含负面词汇（差、烂、失望、后悔）
- **中性**：仅陈述事实、提问、或无明显情感倾向

## 决策流程
```
1. 是否包含正面词汇？
   ├─ 是 → 是否包含负面词汇？
   │      ├─ 是 → 看主导情感（正面词汇数量 vs 负面词汇数量）
   │      └─ 否 → 正面
   └─ 否 → 是否包含负面词汇？
          ├─ 是 → 负面
          └─ 否 → 中性
```

## 边界案例（必看）

| 评论 | 标注 | 理由 |
|------|------|------|
| "性价比很高" | 正面 | "很高"是明确正面评价 |
| "性价比很高，但物流慢" | 正面 | 正面词汇1个，负面词汇1个，但"很高"程度强于"慢" |
| "不知道好不好" | 中性 | 无明确情感，只是疑问 |
| "还行吧" | 中性 | "还行"表示勉强接受，无明显正负面 |
| "比预期的好" | 正面 | 明确表达超出预期 |

## 常见错误
- ❌ "物流慢但产品好" → 只标注"负面"（忽略了正面）
- ✅ "物流慢但产品好" → "正面"（正面为主）
```

**原因**：标注质量的核心是标注者间一致性（Inter-annotator Agreement）。模糊的指南会导致一致性低于 70%，使标注数据无法用于训练。必须通过决策流程图、边界案例、常见错误来消除歧义。

## Gotcha 2：未做标注者间一致性检验直接合并标注

**问题**：多个标注者对同一数据标注后，未计算一致性系数（如 Cohen's Kappa、Fleiss' Kappa）就直接合并或投票，导致低质量标注进入训练集。

❌ **Before（错误做法）**
```python
# 直接投票，不检查一致性
annotations = [
    ["正面", "负面", "正面"],  # 3个标注者
    ["负面", "负面", "负面"],
]

final_labels = [Counter(a).most_common(1)[0][0] for a in annotations]
# 未检查：第一组的一致性很差（2正1负），可能指南有问题
```

✅ **After（正确做法）**
```python
from sklearn.metrics import cohen_kappa_score
import numpy as np

def check_annotation_quality(annotations, min_kappa=0.7):
    """检查标注质量"""
    
    # 1. 计算两两 Kappa
    n_annotators = len(annotations[0])
    kappas = []
    for i in range(n_annotators):
        for j in range(i+1, n_annotators):
            kappa = cohen_kappa_score(
                [a[i] for a in annotations],
                [a[j] for a in annotations]
            )
            kappas.append(kappa)
    
    avg_kappa = np.mean(kappas)
    
    # 2. 质量判断
    if avg_kappa < min_kappa:
        print(f"⚠️ 标注一致性不足: {avg_kappa:.3f} (要求 > {min_kappa})")
        
        # 3. 找出分歧样本
        disagreements = []
        for idx, ann in enumerate(annotations):
            if len(set(ann)) > 1:
                disagreements.append({
                    "sample_id": idx,
                    "annotations": ann,
                    "entropy": self._compute_entropy(ann)
                })
        
        # 4. 触发指南优化
        return {
            "status": "failed",
            "kappa": avg_kappa,
            "disagreements": disagreements[:20],  # Top 20 分歧样本
            "action": "review_guidelines"
        }
    
    return {"status": "passed", "kappa": avg_kappa}

# 只有一致性达标后才合并
quality = check_annotation_quality(annotations)
if quality["status"] == "passed":
    final_labels = merge_annotations(annotations)
else:
    # 先优化指南，再重新标注
    optimize_guidelines(quality["disagreements"])
```

**原因**：标注者间一致性是标注数据质量的黄金标准。Cohen's Kappa > 0.7 才被认为可靠。未通过一致性检验的标注数据会污染训练集，导致模型学习错误的模式。

## Gotcha 3：标注任务设计不合理导致标注疲劳

**问题**：标注任务过于复杂或单调，标注者疲劳后质量急剧下降，但质检系统未考虑疲劳因素。

❌ **Before（错误做法）**
```python
# 让标注者连续标注 1000 条数据，无休息
annotation_task = {
    "data": all_1000_samples,
    "batch_size": 1000,  # 太大！
    "break_interval": None  # 无休息！
}
```

✅ **After（正确做法）**
```python
class AnnotationTaskDesigner:
    """设计合理的标注任务"""
    
    def design_batches(self, data, difficulty_scores):
        """根据难度分批次"""
        # 简单:困难 = 7:3，避免连续难题导致疲劳
        easy = [d for d, s in zip(data, difficulty_scores) if s < 0.5]
        hard = [d for d, s in zip(data, difficulty_scores) if s >= 0.5]
        
        batches = []
        for i in range(0, len(data), 50):  # 每批 50 条
            batch = easy[i:i+35] + hard[i:i+15]  # 7:3 混合
            batches.append(batch)
        
        return batches
    
    def insert_gold_samples(self, batch, gold_ratio=0.1):
        """插入已知答案的样本用于质检"""
        n_gold = int(len(batch) * gold_ratio)
        gold_samples = self.get_gold_samples(n_gold)
        
        # 随机插入
        for gold in gold_samples:
            pos = random.randint(0, len(batch))
            batch.insert(pos, gold)
        
        return batch
    
    def monitor_fatigue(self, annotator_id, recent_accuracy):
        """监控标注者疲劳度"""
        if recent_accuracy < 0.85:
            return {
                "alert": True,
                "message": "检测到质量下降，建议休息 10 分钟",
                "action": "pause"
            }
        return {"alert": False}
```

**原因**：标注是高度认知负荷的工作。连续标注会导致疲劳，错误率上升。必须通过合理的批次设计（混合难度）、黄金样本质检、疲劳监控来保障标注质量。

## Gotcha 4：数据分布变化未更新标注指南

**问题**：业务场景变化导致数据分布变化（如新类型的用户评论），但标注指南未同步更新，标注者按旧规则标注新类型数据，产生系统性偏差。

❌ **Before（错误做法）**
```python
# 一直使用旧版指南
annotation_guide = load_guide("guide_v1.0.md")  # 3年前编写

# 新类型的数据（如 AI 生成内容）没有标注规则
```

✅ **After（正确做法）**
```python
class GuideEvolutionManager:
    """标注指南进化管理"""
    
    def __init__(self):
        self.guide_version = "1.0"
        self.change_log = []
    
    def detect_distribution_shift(self, new_data, reference_data):
        """检测数据分布变化"""
        # 使用 PSI (Population Stability Index)
        psi_scores = compute_psi(reference_data, new_data)
        
        shifted_features = [
            feat for feat, score in psi_scores.items()
            if score > 0.25  # PSI > 0.25 表示显著变化
        ]
        
        return shifted_features
    
    def suggest_guide_updates(self, shifted_features, recent_disagreements):
        """建议指南更新"""
        suggestions = []
        
        for feature in shifted_features:
            if feature == "text_length":
                suggestions.append({
                    "type": "new_rule",
                    "content": "新增：长文本（>500字）需分段标注",
                    "reason": "近期长文本比例增加 30%"
                })
            
            if feature == "content_type":
                suggestions.append({
                    "type": "new_category",
                    "content": "新增类别：AI生成内容",
                    "reason": "检测到新型内容，旧指南无法覆盖"
                })
        
        # 基于分歧样本建议
        for disagreement in recent_disagreements[:10]:
            suggestions.append({
                "type": "clarification",
                "content": f"澄清：'{disagreement['text']}' 应标注为 {disagreement['consensus']}",
                "reason": "近期分歧率高"
            })
        
        return suggestions
    
    def update_guide(self, suggestions):
        """更新指南"""
        self.guide_version = bump_version(self.guide_version)
        
        for suggestion in suggestions:
            apply_change(suggestion)
            self.change_log.append({
                "version": self.guide_version,
                "date": datetime.now(),
                "change": suggestion
            })
        
        # 通知所有标注者
        notify_annotators(f"指南已更新至 v{self.guide_version}，请重新培训")
```

**原因**：数据分布会随时间变化（概念漂移），标注指南必须同步进化。必须建立分布监控、分歧分析、指南更新机制，确保标注规则始终覆盖当前数据类型。
