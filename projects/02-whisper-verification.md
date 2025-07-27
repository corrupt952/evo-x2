# [Verification 2] Whisper Speech Recognition Verification

## Overview
Run OpenAI Whisper utilizing EVO-X2's GPU and verify speech recognition performance.

## Objectives
- Confirm Whisper operation in ROCm environment
- Evaluate speech recognition accuracy and real-time capability
- Verify feasibility of practical voice input system

## Verification Items

### 1. Whisper Installation
```bash
# Python environment setup
python -m venv whisper-env
source whisper-env/bin/activate

# Whisper installation (CPU version)
pip install openai-whisper

# GPU version (ROCm compatibility check)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.0
```

### 2. Basic Operation Test
```python
import whisper

# Model loading
model = whisper.load_model("large-v3")

# Speech file recognition
result = model.transcribe("audio.mp3")
print(result["text"])
```

### 3. Benchmark Test
- **Recognition Speed Measurement**
  - Processing time for small/medium/large models
  - Real-time factor (RTF) measurement
  
- **Accuracy Evaluation**
  - Evaluation with Japanese speech dataset (JSUT, etc.)
  - Evaluation with English speech dataset (LibriSpeech, etc.)

### 4. Real-time Speech Recognition
```python
# Real-time recognition from microphone input
import pyaudio
import numpy as np

# Streaming recognition implementation
def realtime_transcribe():
    # Implementation details
    pass
```

### 5. Practical Scenarios
- **Automatic Meeting Minutes**
  - Real-time transcription of meeting audio
  - Speaker diarization verification

- **Voice Command System**
  - Voice assistant integrated with LLM
  - Response time measurement

## Expected Results
- Whisper operability in ROCm environment
- Performance data for each model size
- Guidelines for practical speech recognition system

## Test Environment
- Microphone: High-quality USB microphone recommended
- Audio: PulseAudio/ALSA configuration
- Test data: Public benchmark datasets

## Troubleshooting
- PyTorch ROCm version recognition issues
- Audio device configuration
- Solutions for memory shortage