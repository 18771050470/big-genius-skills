# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：图像预处理不一致导致训练推理不匹配

**问题**：训练时对图像做了特定的预处理（如归一化均值/方差、Resize 方式），但推理时参数不同，导致模型性能下降。

❌ **Before（错误做法）**
```python
# 训练时
train_transform = transforms.Compose([
    transforms.Resize(256),
    transforms.CenterCrop(224),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.485, 0.456, 0.406], 
                        std=[0.229, 0.224, 0.225])  # ImageNet 统计
])

# 推理时（不同脚本）
test_transform = transforms.Compose([
    transforms.Resize(224),  # 尺寸不同！
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.5, 0.5, 0.5],  # 统计值不同！
                        std=[0.5, 0.5, 0.5])
])
```

✅ **After（正确做法）**
```python
# 统一定义在配置中
PREPROCESS_CONFIG = {
    "input_size": 224,
    "resize_size": 256,
    "mean": [0.485, 0.456, 0.406],
    "std": [0.229, 0.224, 0.225],
    "interpolation": "bilinear"
}

class ImagePreprocessor:
    """统一的图像预处理"""
    
    def __init__(self, config=PREPROCESS_CONFIG):
        self.config = config
        self.transform = transforms.Compose([
            transforms.Resize(config["resize_size"]),
            transforms.CenterCrop(config["input_size"]),
            transforms.ToTensor(),
            transforms.Normalize(
                mean=config["mean"], 
                std=config["std"]
            )
        ])
    
    def process(self, image_path):
        """训练和推理使用完全相同的预处理"""
        image = Image.open(image_path).convert('RGB')
        return self.transform(image)

# 训练和推理使用同一个实例
preprocessor = ImagePreprocessor(PREPROCESS_CONFIG)

train_data = [preprocessor.process(f) for f in train_files]
test_data = [preprocessor.process(f) for f in test_files]
```

**原因**：深度学习模型对输入分布极其敏感。预处理参数（均值、方差、Resize 方式）的微小差异都会导致特征分布偏移，使训练好的模型无法正常工作。必须通过统一的预处理类确保训练和推理完全一致。

## Gotcha 2：未处理图像长宽比导致目标变形

**问题**：直接将图像 Resize 到正方形，未保持长宽比，导致目标变形（如人脸变扁、车辆变窄），影响检测和识别精度。

❌ **Before（错误做法）**
```python
# 直接 Resize 到正方形，忽略长宽比
image = cv2.resize(image, (224, 224))  # 16:9 的图像被压扁！
```

✅ **After（正确做法）**
```python
def resize_keep_aspect(image, target_size=224):
    """保持长宽比的 Resize"""
    h, w = image.shape[:2]
    
    # 计算缩放比例
    scale = min(target_size / h, target_size / w)
    new_h, new_w = int(h * scale), int(w * scale)
    
    # 按比例缩放
    resized = cv2.resize(image, (new_w, new_h))
    
    # 填充到目标尺寸（letterbox）
    top = (target_size - new_h) // 2
    left = (target_size - new_w) // 2
    
    padded = cv2.copyMakeBorder(
        resized,
        top, target_size - new_h - top,
        left, target_size - new_w - left,
        cv2.BORDER_CONSTANT,
        value=[114, 114, 114]  # 灰色填充
    )
    
    return padded, scale, (top, left)

# 检测后需要将坐标转换回原图
boxes = model.predict(padded_image)
for box in boxes:
    x1 = (box[0] - left) / scale
    y1 = (box[1] - top) / scale
    x2 = (box[2] - left) / scale
    y2 = (box[3] - top) / scale
```

**原因**：强行改变长宽比会导致目标几何变形，严重影响检测和识别精度（尤其是几何敏感的任务如 OCR、人脸检测）。必须使用 Letterbox 填充保持长宽比，并在后处理时将坐标映射回原图。

## Gotcha 3：数据增强过度导致模型学习错误特征

**问题**：使用了过于激进的数据增强（如大角度旋转、强色彩抖动），导致增强后的图像与原始任务无关，模型学习了错误的特征。

❌ **Before（错误做法）**
```python
# 过度增强
transform = transforms.Compose([
    transforms.RandomRotation(180),  # 旋转180度！数字"6"变成"9"
    transforms.ColorJitter(brightness=2.0, contrast=2.0),  # 过强
    transforms.RandomHorizontalFlip(p=0.5),  # 数字翻转后意义改变
])
```

✅ **After（正确做法）**
```python
# 任务相关的适度增强
# 数字识别任务
digit_transform = transforms.Compose([
    transforms.RandomRotation(10),  # 小角度旋转
    transforms.ColorJitter(brightness=0.2, contrast=0.2),  # 适度
    # 不翻转！6 和 9 会混淆
])

# 自然图像分类
image_transform = transforms.Compose([
    transforms.RandomResizedCrop(224, scale=(0.8, 1.0)),
    transforms.RandomHorizontalFlip(p=0.5),  # 自然图像可以翻转
    transforms.ColorJitter(brightness=0.4, contrast=0.4, 
                          saturation=0.4, hue=0.1),
    transforms.RandomAffine(degrees=15, translate=(0.1, 0.1)),
])

# 医学图像（需要特别小心）
medical_transform = transforms.Compose([
    transforms.RandomRotation(5),  # 极小的旋转
    transforms.ColorJitter(brightness=0.1),  # 极弱的色彩变化
    # 不翻转！医学图像有方向性
])
```

**原因**：数据增强必须与任务匹配。过度增强会引入与任务无关的变异，导致模型学习错误特征。例如，数字识别中 180 度旋转会使 6 和 9 混淆，医学图像翻转可能改变病理含义。

## Gotcha 4：未处理小目标导致检测漏检率高

**问题**：目标检测模型在训练时主要学习大目标，小目标（占图像比例 < 1%）的检测率极低，但业务场景中大量目标都是小目标。

❌ **Before（错误做法）**
```python
# 直接使用标准 Anchor 和 FPN
model = FasterRCNN(backbone, 
                   rpn_anchor_generator=default_anchors,  # 默认 Anchor 偏大
                   box_roi_pool=default_roi_pool)
# 小目标漏检率 > 50%
```

✅ **After（正确做法）**
```python
# 针对小目标优化
from torchvision.models.detection import FasterRCNN
from torchvision.models.detection.rpn import AnchorGenerator

# 1. 使用更小的 Anchor
small_anchors = AnchorGenerator(
    sizes=((4, 8, 16), (8, 16, 32), (16, 32, 64), 
           (32, 64, 128), (64, 128, 256)),  # 更小的基础尺寸
    aspect_ratios=((0.5, 1.0, 2.0),) * 5
)

# 2. 使用更高分辨率的 FPN
class HighResFPN(nn.Module):
    def __init__(self):
        super().__init__()
        # 保留更多高层特征
        self.lateral_c2 = nn.Conv2d(64, 256, 1)  # 使用 P2（1/4 分辨率）
        
# 3. 多尺度训练
train_transform = transforms.Compose([
    transforms.RandomResize([(800, 1333), (1000, 1666), (1200, 2000)]),
])

# 4. 小目标数据增强
def copy_paste_small_objects(image, boxes, labels):
    """复制粘贴小目标增加样本"""
    small_objects = [b for b in boxes if area(b) < 32*32]
    for obj in small_objects:
        # 随机粘贴到其他位置
        paste_to_random_location(image, obj)
    return image

# 5. 使用专门的小目标检测头
model = FasterRCNN(
    backbone,
    rpn_anchor_generator=small_anchors,
    box_roi_pool=MultiScaleRoIAlign(
        featmap_names=['p2', 'p3', 'p4', 'p5'],
        output_size=7,
        sampling_ratio=2
    ),
    min_size=600,  # 允许更小的输入
    max_size=2000
)
```

**原因**：小目标检测是计算机视觉的难点。标准检测器（如 Faster R-CNN）的 Anchor 和 FPN 设计偏向中大目标。必须通过小 Anchor、高分辨率特征图、多尺度训练、小目标增强等手段专门优化小目标检测。
