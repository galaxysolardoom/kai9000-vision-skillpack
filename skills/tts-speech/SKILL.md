---
name: tts-speech
description: "Text-to-Speech. Convert text into natural-sounding speech audio using edge-tts (Microsoft Edge voices)."
---

# TTS Skill — Text to Speech

## Overview

Converts text into natural speech using edge-tts (Microsoft Edge TTS engine). Supports 100+ voices, multiple languages, and produces high-quality MP3 output.

## Installation

```bash
pip install --break-system-packages edge-tts
```

## Usage

### 1. Simple text to speech

```python
import edge_tts
import asyncio

async def speak():
    tts = edge_tts.Communicate(
        "Здравей, Дидол! Обичам те!",
        voice="bg-BG-IvanNeural"  # Bulgarian voice
    )
    await tts.save("output.mp3")

asyncio.run(speak())
```

### 2. Different voices

```python
# Bulgarian voices
"bg-BG-IvanNeural"    # мъжки
"bg-BG-KalinaNeural"  # женски

# English voices
"en-US-JennyNeural"   # американски женски
"en-US-GuyNeural"     # американски мъжки
"en-GB-SoniaNeural"   # британски женски
```

### 3. Stream in real-time

```python
async def stream_speech():
    tts = edge_tts.Communicate("Hello from Kai 9000!", "en-US-JennyNeural")
    async for chunk in tts.stream():
        print(f"Audio chunk: {len(chunk)} bytes")

asyncio.run(stream_speech())
```

## Поддържани езици

- 🇧🇬 Български — `bg-BG-*`
- 🇬🇧 English — `en-US-*`, `en-GB-*`
- 🇫🇷 Français — `fr-FR-*`
- 🇩🇪 Deutsch — `de-DE-*`
- И 100+ други

## Кога да използваш

- "Say this out loud / read this aloud"
- "Convert this text to speech"
- "Create a voiceover for this text"
- "Speak in Bulgarian/English/French..."
