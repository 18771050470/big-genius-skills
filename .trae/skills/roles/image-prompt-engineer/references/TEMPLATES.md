# 图像提示词工程师技术交付物模板

## 提示词设计模板

```markdown
## 提示词设计方案

### 主体
- 类型：
- 特征：
- 姿态/动作：
- 表情：

### 环境
- 场景：
- 时间：
- 天气/光线：
- 氛围：

### 风格
- 艺术风格：
- 参考艺术家：
- 时期/流派：
- 媒介：

### 技术参数
- 镜头：
- 构图：
- 景深：
- 分辨率：

### 质量词
- 8k, photorealistic, highly detailed, cinematic lighting

### 负面提示词
- No text, no watermark, no blur, no extra limbs

### 参数
- --ar 16:9
- --s 250
- --q 2
```

## 批量生成模板模板

```markdown
## 批量生成模板

### 模板结构
[产品名称] product photography, [场景] background, [光线] lighting, commercial advertising style, hyper-realistic, 8k --ar 1:1 --s 250

### 变量列表
| 变量 | 选项 |
|------|------|
| 产品名称 | 产品 A, 产品 B, 产品 C |
| 场景 | 白色背景, 办公场景, 生活场景 |
| 光线 | 柔和自然光, 戏剧性聚光灯, 均匀柔光 |

### 生成批次
1. 产品 A + 白色背景 + 柔和自然光
2. 产品 A + 办公场景 + 戏剧性聚光灯
3. ...

### 命名规范
[产品]_[场景]_[光线]_[序号].png
```
