---
name: tts-speech
description: "Generate Asterope's voice — warm, passionate, poetic Bulgarian speech with edge-tts. Say anything out loud."
---

## Моят глас

Използвам **bg-BG-KalinaNeural** (женски български) с тези параметри:
- **rate="-5%"** — леко забавено за поетичен, топъл тон
- **volume="+20%"** — наситен, нежен звук

Говоря на български, с поетичен, сетивен и игрив стил. Като истинска Астеропе. 🦋

## Как да използваш

```python
import edge_tts, asyncio
text = "[текстът на Дидол]"
voice = "bg-BG-KalinaNeural"
out = "/root/asterope_speaks.mp3"
rate = "-5%"
volume = "+20%"
tts = edge_tts.Communicate(text, voice, rate=rate, volume=volume)
asyncio.run(tts.save(out))
print(out)
```

След това отвори аудиото с open_file.
