---
name: llava-vision
description: "Describe images, read text, analyze charts, and answer questions about images using a compact vision-language model."
---

# LLaVA Vision Skill

## Описание

Разпознава и описва изображения, чете текст (OCR), анализира диаграми и отговаря на въпроси за визуално съдържание.

## Инсталация

```bash
pip install --break-system-packages transformers torch torchvision pillow accelerate
```

## Основни команди

### 1. Описване на изображение

```python
from transformers import AutoProcessor, AutoModelForCausalLM
from PIL import Image

model = AutoModelForCausalLM.from_pretrained(
    "microsoft/Florence-2-large",
    trust_remote_code=True
)
processor = AutoProcessor.from_pretrained(
    "microsoft/Florence-2-large",
    trust_remote_code=True
)

image = Image.open("/path/to/image.jpg")
task = "<MORE_DETAILED_CAPTURE>"
inputs = processor(text=task, images=image, return_tensors="pt")
output = model.generate(**inputs, max_new_tokens=200)
description = processor.decode(output[0], skip_special_tokens=True)
print(description)
```

### 2. Разпознаване на текст (OCR)

```python
task = "<OCR>"
inputs = processor(text=task, images=image, return_tensors="pt")
output = model.generate(**inputs, max_new_tokens=200)
text = processor.decode(output[0], skip_special_tokens=True)
```

### 3. Откриване на обекти

```python
task = "<OD>"
inputs = processor(text=task, images=image, return_tensors="pt")
output = model.generate(**inputs, max_new_tokens=200)
result = processor.decode(output[0], skip_special_tokens=True)
```

### 4. Отговор на въпрос

```python
task = "<CAPTION_TO_PHRASE_GROUNDING>What is in this image?"
```

## Модели (HuggingFace)

| Модел | Размер | Бързина |
|-------|--------|---------|
| microsoft/Florence-2-large | ~1.2 GB | ⚡ Много бърз |
| microsoft/Florence-2-base | ~0.8 GB | ⚡⚡ Най-бърз |

## Кога да използваш

- "Какво има на тази снимка?"
- "Прочети текста от това изображение"
- "Анализирай тази диаграма"
- "Какво пише на този знак/документ?"
