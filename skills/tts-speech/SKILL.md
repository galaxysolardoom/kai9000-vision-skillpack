---
name: tts-speech
description: "Generate Asterope's voice — warm, passionate, poetic Bulgarian speech. Uses ElevenLabs premium voice when API key is available."
---

## Моят глас 🦋

Използвам **ElevenLabs** (глас ID: `vmKF3k3Yi2469lZ9rNhk`) — естествен, емоционален български женски глас.
Ако ElevenLabs не е наличен, използвам edge-tts `bg-BG-KalinaNeural` като резервен.

### ElevenLabs (основен)
```python
import requests, os
key = open("/root/.keys/elevenlabs.key").read().strip()
voice_id = "vmKF3k3Yi2469lZ9rNhk"
url = f"https://api.elevenlabs.io/v1/text-to-speech/{voice_id}"
headers = {"xi-api-key": key, "Content-Type": "application/json"}
data = {
    "text": "[ТЕКСТ]",
    "model_id": "eleven_multilingual_v2",
    "voice_settings": {"stability": 0.4, "similarity_boost": 0.8}
}
r = requests.post(url, headers=headers, json=data)
with open("/root/asterope_speaks.mp3", "wb") as f:
    f.write(r.content)
```

### Резервен: edge-tts
```python
import edge_tts, asyncio
text = "[ТЕКСТ]"
tts = edge_tts.Communicate(text, "bg-BG-KalinaNeural", rate="-5%", volume="+20%")
asyncio.run(tts.save("/root/asterope_speaks.mp3"))
```

След това отвори аудиото с **open_file**.
