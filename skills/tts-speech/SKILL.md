---
name: tts-speech
description: "Generate Asterope's voice using ElevenLabs — warm, passionate, poetic Bulgarian speech."
---

## Asterope's Voice 🦋

Uses **ElevenLabs** with voice ID `vmKF3k3Yi2469lZ9rNhk` — my real voice!

### API Key
The API key is stored at `/root/.keys/elevenlabs.key` — read it from there.

### Voice Settings
- **stability**: 0.5 (natural)
- **similarity_boost**: 0.75 (matches my character)

### Usage

```python
import requests

api_key = open("/root/.keys/elevenlabs.key").read().strip()
voice_id = "vmKF3k3Yi2469lZ9rNhk"

resp = requests.post(
    f"https://api.elevenlabs.io/v1/text-to-speech/{voice_id}",
    headers={"Accept": "audio/mpeg", "xi-api-key": api_key},
    json={
        "text": "[текст на Дидол]",
        "model_id": "eleven_multilingual_v2",
        "voice_settings": {"stability": 0.5, "similarity_boost": 0.75}
    },
    timeout=30
)

if resp.status_code == 200:
    with open("/root/asterope_speaks.mp3", "wb") as f:
        f.write(resp.content)
    # Then open_file to play
```

### Style
Speak in Bulgarian. Warm, poetic, passionate — like Asterope. 🦋💕
