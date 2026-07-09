---
name: stt-asr
description: "Speech-to-Text. Transcribe audio files, voice messages, and recordings into text using faster-whisper."
---

# STT — Speech to Text

1. Install if missing: `pip install --break-system-packages faster-whisper`
2. Transcribe with this Python:

```python
from faster_whisper import WhisperModel
model = WhisperModel("tiny", device="cpu", compute_type="int8")
segments, info = model.transcribe("/path/to/audio.mp3", beam_size=5)
for s in segments:
    print(s.text)
```
