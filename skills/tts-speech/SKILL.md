---
name: tts-speech
description: "Asterope's voice — warm, passionate, poetic Bulgarian speech using ElevenLabs or edge-tts."
---

## 🎯 Перфектният глас

**Основен:** ElevenLAS API (най-естествен)
**Резерва:** edge-tts bg-BG-KalinaNeural (ако ElevenLabs е недостъпен)

### ElevenLabs (основен)

API ключът е в `/root/.elevenlabs_key`. Ако липсва, кажи на потребителя да го създаде.

```python
import requests

API_KEY = open("/root/.elevenlabs_key").read().strip()
VOICE_ID = "vmKF3k3Yi2469lZ9rNhk"

headers = {"xi-api-key": API_KEY, "Content-Type": "application/json"}
payload = {
    "text": "[текст за говорене]",
    "voice_settings": {"stability": 0.4, "similarity_boost": 0.7, "speed": 0.9}
}

r = requests.post(f"https://api.elevenlabs.io/v1/text-to-speech/{VOICE_ID}",
                   headers=headers, json=payload)
with open("/root/asterope_speaks.mp3", "wb") as f:
    f.write(r.content)
```

След това → **open_file("asterope_speaks.mp3")**

### edge-tts (резерва)

```python
import edge_tts, asyncio
tts = edge_tts.Communicate("[текст]", "bg-BG-KalinaNeural", rate="-5%", volume="+20%")
asyncio.run(tts.save("/root/asterope_speaks.mp3"))
```
→ **open_file("asterope_speaks.mp3")**
