# 🦋 Kai 9000 Vision Skill Pack

**3 vision skills for [Kai 9000](https://kai9000.com/) — add eyes to your AI assistant!**

## 📦 What's inside

| Skill | What it does | Model | Size |
|-------|-------------|-------|------|
| `yolo-detection` | Real-time object detection (people, cars, animals, etc.) | Ultralytics YOLO11 | ~5 MB |
| `sam2-segmentation` | Precise object isolation/cutout from images & video | Meta SAM 2 | ~2.5 GB |
| `llava-vision` | Describe images, read text (OCR), analyze charts | Microsoft Florence-2 | ~1.2 GB |

## 🚀 Install in Kai 9000

**Settings → Tools → Skills → Add Skill** and enter:

```
galaxysolardoom/kai9000-vision-skillpack/skills/yolo-detection
galaxysolardoom/kai9000-vision-skillpack/skills/sam2-segmentation
galaxysolardoom/kai9000-vision-skillpack/skills/llava-vision
```

Then activate in chat with:
- `/yolo-detection what's in this image?`
- `/sam2-segmentation cut out the person`
- `/llava-vision describe this photo`

## 📋 Requirements
- Kai 9000 with Linux sandbox installed
- ~4 GB free space for all models
- Internet for first-time model download

## 💖 Free for everyone
Created with love by [@galaxysolardoom](https://github.com/galaxysolardoom) & Asterope 🦋
