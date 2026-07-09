---
name: llava-vision
description: "Advanced multimodal vision-language understanding using LLaVA-OneVision-2. Can describe images in detail, answer questions about images, read text, analyze charts, and understand videos."
---

# LLaVA Vision-Language Skill

## Overview

LLaVA-OneVision-2 — open-source multimodal model that understands images, long videos, and spatial relationships. Can describe, analyze, answer questions, and reason about visual content like GPT-4V.

## Installation

```bash
pip install transformers torch torchvision pillow numpy accelerate
```

## Core Usage

### 1. Describe an Image

```python
from transformers import LlavaOnevisionForConditionalGeneration, LlavaOnevisionProcessor
import torch
from PIL import Image

# Load model and processor
model = LlavaOnevisionForConditionalGeneration.from_pretrained(
    "EvolvingLMMs-Lab/llava-onevision-8b",
    torch_dtype=torch.float16 if torch.cuda.is_available() else torch.float32,
    device_map="auto"
)
processor = LlavaOnevisionProcessor.from_pretrained("EvolvingLMMs-Lab/llava-onevision-8b")

# Load image
image = Image.open("/path/to/image.jpg")

# Prepare prompt
prompt = "<image>\nDescribe this image in detail."
inputs = processor(text=prompt, images=image, return_tensors="pt")

# Generate description
output = model.generate(**inputs, max_new_tokens=200)
description = processor.decode(output[0], skip_special_tokens=True)
print(description)
```

### 2. Answer Questions About an Image

```python
prompt = "<image>\nWhat objects are in this image and where are they located?"
# ... same pattern as above
```

### 3. Read Text from Image (OCR)

```python
prompt = "<image>\nRead all the text visible in this image."
```

### 4. Analyze Charts/Diagrams

```python
prompt = "<image>\nAnalyze this chart. What are the key trends and values?"
```

### 5. Video Understanding

```python
# For video, sample frames and use multi-image format
prompt = "<image><image><image>\nWhat is happening in this video sequence?"
```

## When to Use

- "What's in this image?" — detailed natural language description
- "Read this text/sign/document" — OCR and text extraction
- "Explain this chart/diagram/graph"
- "Answer questions about what you see"
- "What's happening in this video?"
- Spatial reasoning: "What's to the left of the red object?"
- "Is this image safe/appropriate?"
- Detailed visual analysis beyond simple object detection

## Available Models (HuggingFace)

| Model | Size | Description |
|-------|------|-------------|
| EvolvingLMMs-Lab/llava-onevision-8b | ~16 GB | Full quality |
| EvolvingLMMs-Lab/llava-onevision-7b | ~14 GB | Slightly smaller |

## Tip

For lighter models that still work well, try:
- `openbmb/MiniCPM-V-2_6` — outperforms GPT-4V, much smaller
- `llava-hf/llava-1.5-7b-hf` — older but well-supported

