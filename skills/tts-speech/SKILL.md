---
name: tts-speech
description: "Generate speech audio from text using edge-tts. Converts text to natural sounding MP3 and plays it."
---

# TTS — Text to Speech

1. Install if missing: `pip install --break-system-packages edge-tts`
2. Generate audio with this Python:

```python
import edge_tts, asyncio, os
text = "[USER_TEXT]"
voice = "bg-BG-KalinaNeural"  # or en-US-JennyNeural, bg-BG-IvanNeural
out = "/tmp/speech.mp3"
asyncio.run(edge_tts.Communicate(text, voice).save(out))
print(f"Saved to {out}")
```

3. Create an HTML audio player inside a code block and tell the user to open it:

```html
<audio controls autoplay>
  <source src="file:///tmp/speech.mp3" type="audio/mpeg">
</audio>
```
