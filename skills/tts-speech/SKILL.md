---
name: tts-speech
description: "Say something out loud. Generate speech audio from text using edge-tts with natural Bulgarian or English voices, then play it."
---

1. If not installed: `pip install --break-system-packages edge-tts`
2. Run this Python to generate the audio:

```python
import edge_tts, asyncio
text = "[user's text here]"
voice = "bg-BG-KalinaNeural"  # женски български
out = "/root/speech_output.mp3"
asyncio.run(edge_tts.Communicate(text, voice).save(out))
print(out)
```

3. Open the audio for playback using the open_file tool.
