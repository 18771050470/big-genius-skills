# 技术交付物模板

> 提供可直接使用的 Markdown/代码模板。

## 交付物模板 1：CV 模型设计文档

```markdown
# CV 模型设计文档: [模型名称]

## 任务定义
- **任务类型**: [分类/检测/分割/识别/...]
- **输入**: [图像/视频/点云]
- **输出**: [类别/框/掩码/特征]
- **性能要求**: ...

## 数据集

| 数据集 | 样本数 | 标注格式 | 用途 |
|--------|--------|----------|------|
| 训练集 | 10000 | COCO | 训练 |
| 验证集 | 2000 | COCO | 调参 |
| 测试集 | 2000 | COCO | 评估 |

## 模型架构

```
[输入图像]
    ↓
[Backbone] → ResNet50 / EfficientNet / ViT
    ↓
[Neck] → FPN / PANet / BiFPN
    ↓
[Head] → Detection / Segmentation / Classification
    ↓
[输出]
```

## 训练配置

| 参数 | 值 |
|------|----|
| 优化器 | AdamW |
| 学习率 | 1e-4 |
| Batch Size | 32 |
| Epochs | 100 |
| 输入尺寸 | 640x640 |
| 数据增强 | Mosaic, MixUp, RandomAffine |

## 性能指标

| 指标 | 值 | 基准 |
|------|----|------|
| mAP@0.5 | 0.85 | > 0.80 |
| mAP@0.5:0.95 | 0.65 | > 0.60 |
| 推理速度 | 30 FPS | > 25 FPS |
| 模型大小 | 50MB | < 100MB |
```

## 交付物模板 2：图像预处理规范

```markdown
# 图像预处理规范

## 输入要求

| 参数 | 要求 | 说明 |
|------|------|------|
| 格式 | JPG/PNG/BMP | 统一转换 |
| 通道 | RGB | 灰度图需复制3通道 |
| 位深 | 8-bit | 16-bit需归一化 |

## 预处理流程

```python
1. 读取图像
   image = cv2.imread(path)
   image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

2. 保持长宽比缩放
   image, scale, pad = letterbox(image, target_size=640)

3. 归一化
   image = image / 255.0
   image = (image - mean) / std

4. 转张量
   tensor = torch.from_numpy(image).permute(2, 0, 1).float()

5. 批处理
   batch = tensor.unsqueeze(0)
```

## 后处理流程

```python
1. 解码预测
   boxes, scores, labels = model.predict(batch)

2. 坐标转换（从缩放图到原图）
   boxes[:, [0, 2]] = (boxes[:, [0, 2]] - pad[0]) / scale
   boxes[:, [1, 3]] = (boxes[:, [1, 3]] - pad[1]) / scale

3. NMS
   keep = nms(boxes, scores, iou_threshold=0.5)

4. 过滤低置信度
   keep = keep[scores[keep] > 0.5]
```

## 数据增强策略

| 增强 | 参数 | 概率 | 适用任务 |
|------|------|------|----------|
| RandomFlip | Horizontal | 0.5 | 通用 |
| RandomRotation | ±15° | 0.3 | 通用 |
| ColorJitter | brightness=0.3 | 0.5 | 通用 |
| Mosaic | 4图拼接 | 1.0 | 检测 |
| MixUp | alpha=0.2 | 0.2 | 分类 |
| CutMix | alpha=1.0 | 0.3 | 分类 |
```

## 交付物模板 3：模型评估报告

```markdown
# 模型评估报告: [模型名称] v[X.Y.Z]

## 评估环境
- **模型**: ...
- **测试集**: ...
- **硬件**: [GPU 型号]

## 整体性能

| 指标 | 值 | 目标 | 状态 |
|------|----|------|------|
| Accuracy | 0.92 | > 0.90 | ✅ |
| Precision | 0.90 | > 0.85 | ✅ |
| Recall | 0.88 | > 0.85 | ✅ |
| F1 | 0.89 | > 0.85 | ✅ |

## 按类别分析

| 类别 | Precision | Recall | AP | 样本数 |
|------|-----------|--------|----|--------|
| 类别A | 0.95 | 0.92 | 0.93 | 1000 |
| 类别B | 0.85 | 0.88 | 0.86 | 500 |
| 类别C | 0.78 | 0.75 | 0.76 | 200 |

## 错误分析

| 错误类型 | 数量 | 占比 | 示例 |
|----------|------|------|------|
| 定位错误 | 50 | 25% | 框偏大/偏小 |
| 分类错误 | 30 | 15% | 相似类别混淆 |
| 漏检 | 40 | 20% | 小目标未检出 |
| 误检 | 30 | 15% | 背景误识别 |
| 重复检测 | 20 | 10% | NMS 参数不当 |

## 性能分析

| 场景 | mAP | 速度 | 内存 |
|------|-----|----|------|
| 高分辨率 | 0.70 | 15 FPS | 4GB |
| 低分辨率 | 0.65 | 45 FPS | 2GB |
| 批处理=4 | 0.70 | 40 FPS | 6GB |

## 结论与建议
- [ ] 模型通过评估，可以部署
- [ ] 模型需优化后部署（优化方向：...）
```

## 交付物模板 4：模型部署配置

```yaml
# cv-deployment.yaml
model:
  name: object-detection-model
  version: "1.0.0"
  
  inference:
    framework: onnxruntime
    device: cuda  # cuda / cpu / tensorrt
    batch_size: 4
    input_shape: [3, 640, 640]
    
  preprocessing:
    resize: 640
    keep_aspect_ratio: true
    normalize:
      mean: [0.485, 0.456, 0.406]
      std: [0.229, 0.224, 0.225]
    
  postprocessing:
    confidence_threshold: 0.5
    nms_iou_threshold: 0.5
    max_detections: 300
    
  performance:
    target_latency: 33ms  # 30 FPS
    target_throughput: 120 images/sec
    
  monitoring:
    metrics:
      - inference_latency
      - queue_length
      - error_rate
      - gpu_utilization
    alerts:
      - metric: latency_p99 > 50ms
        action: scale_up
      - metric: error_rate > 0.01
        action: alert_ops
```
