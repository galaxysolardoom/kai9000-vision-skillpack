---
name: stt-asr
description: "Speech-to-Text (Automatic Speech Recognition). Transcribe audio files, voice messages, and recordings into text using OpenAI Whisper."
---

# STT / ASR Skill — Speech to Text

## Overview

Transcribes audio/speech into text using faster-whisper (optimized OpenAI Whisper). Can process MP3, WAV, M4A, OGG and other audio formats.

## Installation

```bash
pip install faster-whisper
```

## Usage

### 1. Base Transcribe (честота на дискретизация 16KHz)

```python
from faster_whisper import WhisperModel

model = WhisperModel("tiny", device="cpu", compute_type="int8")

segments, info = model.transcribe("/path/to/audio.mp3", beam_size=5)
print(f"Detected language: {info.language} (p={info.language_probability:.2f})")

for segment in segments:
    print(f"[{segment.start:.1f}s → {segment.end:.1f}s] {segment.text}")
```

### 2. По-прецизно разпознаване

```python
model = WhisperModel("base", device="cpu", compute_type="int8")
segments, info = model.transcribe("audio.mp3", language="bg", beam_size=5)
```

### 3. Цял текст наведнъж

```python
full_text = " ".join(seg.text for seg in segments)
print(full_text)
```

## Модели (скорост vs точност)

| Модел | Размер | Скорост |
|-------|--------|---------|
| tiny | ~75 MB | ⚡⚡⚡ Най-бърз |
| base | ~150 MB | ⚡⚡ Много бърз |
| small | ~500 MB | ⚡ Баланс |

## Кога да използваш

- "Transcribe this audio/video file"
- "What is being said in this voice message?"
- "Convert this recording to text"
