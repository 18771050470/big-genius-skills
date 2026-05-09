# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：音频预处理不一致导致训练推理不匹配

**问题**：训练时对音频做了特定的预处理（如重采样、预加重、归一化），但推理时预处理参数不同，导致模型性能严重下降。

❌ **Before（错误做法）**
```python
# 训练时
train_audio = librosa.load(train_file, sr=16000)[0]
train_audio = librosa.effects.preemphasis(train_audio)  # 预加重

# 推理时（不同脚本，参数不一致）
test_audio = librosa.load(test_file, sr=22050)[0]  # 采样率不同！
# 忘记做预加重！
```

✅ **After（正确做法）**
```python
# 统一定义在配置中
AUDIO_CONFIG = {
    "sample_rate": 16000,
    "preemphasis": 0.97,
    "normalize": True,
    "max_duration": 30.0,
    "frame_length": 512,
    "hop_length": 256
}

class AudioPreprocessor:
    """统一的音频预处理"""
    
    def __init__(self, config=AUDIO_CONFIG):
        self.config = config
    
    def process(self, audio_path):
        """训练和推理使用完全相同的预处理流程"""
        # 1. 加载
        audio, sr = librosa.load(
            audio_path, 
            sr=self.config["sample_rate"]
        )
        
        # 2. 预加重
        if self.config["preemphasis"]:
            audio = librosa.effects.preemphasis(
                audio, 
                coef=self.config["preemphasis"]
            )
        
        # 3. 归一化
        if self.config["normalize"]:
            audio = audio / (np.max(np.abs(audio)) + 1e-8)
        
        # 4. 截断/填充
        max_len = int(self.config["max_duration"] * self.config["sample_rate"])
        if len(audio) > max_len:
            audio = audio[:max_len]
        else:
            audio = np.pad(audio, (0, max_len - len(audio)))
        
        return audio

# 训练和推理使用同一个实例
preprocessor = AudioPreprocessor(AUDIO_CONFIG)

train_data = [preprocessor.process(f) for f in train_files]
test_data = [preprocessor.process(f) for f in test_files]
```

**原因**：音频模型对预处理极其敏感。采样率、预加重、归一化等参数的微小差异都会导致特征分布变化，使训练好的模型无法正常工作。必须通过统一的预处理类确保训练和推理完全一致。

## Gotcha 2：长音频直接输入导致内存溢出和上下文丢失

**问题**：将长音频（如 1 小时会议录音）直接输入模型，导致 GPU 内存溢出，且模型无法捕捉长距离依赖。

❌ **Before（错误做法）**
```python
# 直接加载长音频
audio = librosa.load("meeting_1hour.wav", sr=16000)[0]  # 5760万样本！
# 内存溢出，或模型无法处理这么长的序列
```

✅ **After（正确做法）**
```python
class LongAudioProcessor:
    """长音频分块处理"""
    
    def __init__(self, chunk_duration=30, overlap=5):
        self.chunk_samples = chunk_duration * 16000
        self.overlap_samples = overlap * 16000
    
    def split_chunks(self, audio):
        """将长音频切分为重叠的块"""
        chunks = []
        start = 0
        
        while start < len(audio):
            end = min(start + self.chunk_samples, len(audio))
            chunk = audio[start:end]
            
            # 填充最后一个块
            if len(chunk) < self.chunk_samples:
                chunk = np.pad(chunk, (0, self.chunk_samples - len(chunk)))
            
            chunks.append({
                "audio": chunk,
                "start_time": start / 16000,
                "end_time": end / 16000,
                "is_last": end == len(audio)
            })
            
            start += self.chunk_samples - self.overlap_samples
        
        return chunks
    
    def merge_results(self, chunk_results):
        """合并各块的结果，处理重叠区域"""
        merged = []
        for i, result in enumerate(chunk_results):
            # 去除重叠区域的重复识别
            if i > 0:
                result = self._deduplicate_with_previous(
                    result, 
                    chunk_results[i-1]
                )
            merged.extend(result)
        return merged
```

**原因**：语音模型（尤其是基于 Transformer 的）有最大输入长度限制。长音频必须切分为重叠的块分别处理，然后合并结果。重叠区域用于消除边界效应和重复识别。

## Gotcha 3：未处理音频质量差异导致模型鲁棒性差

**问题**：训练数据都是高质量录音（清晰、无噪声），但生产环境有背景噪声、回声、压缩失真，导致模型性能急剧下降。

❌ **Before（错误做法）**
```python
# 只在干净数据上训练
train_data = load_clean_recordings()  # 录音棚质量
model.fit(train_data)

# 生产环境：电话录音、有背景噪声
# 识别准确率从 95% 降到 60%
```

✅ **After（正确做法）**
```python
class AudioAugmenter:
    """音频数据增强"""
    
    def __init__(self):
        self.noise_types = [
            "white_noise",
            "babble_noise",  # 人声嘈杂
            "traffic_noise",
            "music_noise"
        ]
    
    def augment(self, audio, sr=16000):
        """应用多种增强"""
        augmented = []
        
        # 1. 加噪
        for noise_type in self.noise_types:
            noise = self.load_noise(noise_type, len(audio))
            snr = random.choice([5, 10, 15, 20])  # 不同信噪比
            noisy = self.add_noise(audio, noise, snr)
            augmented.append(noisy)
        
        # 2. 混响（模拟不同房间）
        room = random.choice(["small", "medium", "large"])
        reverbed = self.add_reverb(audio, room)
        augmented.append(reverbed)
        
        # 3. 速度变化
        speed = random.uniform(0.9, 1.1)
        speed_changed = librosa.effects.time_stretch(audio, rate=speed)
        augmented.append(speed_changed)
        
        # 4. 音量变化
        gain = random.uniform(-6, 6)  # dB
        volume_changed = audio * (10 ** (gain / 20))
        augmented.append(volume_changed)
        
        return augmented

# 训练时增强
train_data = []
for audio in clean_recordings:
    train_data.append(audio)  # 原始
    train_data.extend(augmenter.augment(audio))  # 增强
```

**原因**：生产环境的音频质量千差万别。必须在训练时通过数据增强（加噪、混响、速度变化、音量变化）模拟各种场景，提升模型鲁棒性。

## Gotcha 4：Speaker Diarization 未处理重叠语音

**问题**：说话人分割系统假设语音不重叠，但真实场景中多人同时说话很常见，导致说话人识别错误和语音丢失。

❌ **Before（错误做法）**
```python
# 简单的时间分割
def diarize(audio):
    segments = detect_voice_activity(audio)  # 检测语音段
    for segment in segments:
        speaker = identify_speaker(segment)  # 假设每段只有一个说话人
        print(f"{speaker}: {segment.text}")
    # 重叠语音被分配给一个人，或丢失
```

✅ **After（正确做法）**
```python
class OverlapAwareDiarizer:
    """处理重叠语音的说话人分割"""
    
    def __init__(self, max_speakers=4):
        self.max_speakers = max_speakers
    
    def diarize(self, audio):
        """重叠感知的说话人分割"""
        # 1. 检测语音活动（允许重叠）
        vad_results = self.detect_overlapping_speech(audio)
        
        # 2. 提取嵌入（对每一帧提取说话人嵌入）
        embeddings = self.extract_frame_embeddings(audio)
        
        # 3. 聚类（考虑时间连续性）
        clusters = self.cluster_with_temporal_constraint(
            embeddings, 
            max_speakers=self.max_speakers
        )
        
        # 4. 生成时间线（允许同一时刻多个说话人）
        timeline = []
        for t in range(len(embeddings)):
            active_speakers = [
                spk for spk, label in enumerate(clusters[t])
                if label == 1
            ]
            timeline.append({
                "time": t * 0.02,  # 20ms 一帧
                "speakers": active_speakers
            })
        
        # 5. 合并连续段
        segments = self.merge_continuous_segments(timeline)
        
        return segments
    
    def format_output(self, segments):
        """格式化输出，标注重叠"""
        for seg in segments:
            if len(seg["speakers"]) == 1:
                print(f"[{seg['start']:.1f}s - {seg['end']:.1f}s] "
                      f"Speaker {seg['speakers'][0]}: {seg['text']}")
            else:
                print(f"[{seg['start']:.1f}s - {seg['end']:.1f}s] "
                      f"OVERLAP: Speakers {seg['speakers']}")
                for spk in seg["speakers"]:
                    print(f"  Speaker {spk}: {seg['text_per_speaker'][spk]}")
```

**原因**：真实场景中的多人对话有大量重叠。传统的顺序分割方法会丢失重叠部分的信息。必须使用支持重叠检测的算法（如帧级嵌入+聚类），并在输出中明确标注重叠区域。
