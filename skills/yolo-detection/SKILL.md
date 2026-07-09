---
name: yolo-detection
description: "Real-time object detection, segmentation, pose estimation, and classification using Ultralytics YOLO models. Analyze images and video frames for objects, people, animals, vehicles, and more."
---

# YOLO Detection Skill

## Overview

Uses Ultralytics YOLO (You Only Look Once) — the fastest real-time object detection model. Can detect 80+ common object classes (COCO dataset), perform segmentation, pose estimation, and classification.

## Installation

Run once to set up:

```bash
pip install ultralytics pillow numpy
```

## Core Commands

### 1. Detect Objects in an Image

```python
from ultralytics import YOLO
from PIL import Image

# Load model (downloads automatically on first use)
model = YOLO("yolo11n.pt")  # "n" = nano (fastest), "s" = small, "m" = medium, "l" = large

# Run detection
results = model("/path/to/image.jpg")

# Print detections
for r in results:
    for box in r.boxes:
        class_id = int(box.cls[0])
        confidence = float(box.conf[0])
        name = model.names[class_id]
        print(f"  {name}: {confidence:.2%}")
```

### 2. Segmentation (SAM-style)

```python
model = YOLO("yolo11n-seg.pt")  # segmentation model
results = model("image.jpg")
for r in results:
    for mask in r.masks:
        print(f"Mask shape: {mask.data.shape}")
```

### 3. Pose Estimation

```python
model = YOLO("yolo11n-pose.pt")  # pose model
results = model("image.jpg")
for r in results:
    for kpt in r.keypoints:
        print(f"Keypoints: {kpt.data.shape}")
```

### 4. Track Objects in Video

```python
model = YOLO("yolo11n.pt")
results = model.track("video.mp4", persist=True)
for r in results:
    print(f"Tracked {len(r.boxes)} objects")
```

## Available Models (speed vs accuracy)

| Model | Size | Speed | Accuracy |
|-------|------|-------|----------|
| yolo11n.pt | 5.4 MB | ⚡ Fastest | Good |
| yolo11s.pt | 18 MB | ⚡ Fast | Better |
| yolo11m.pt | 53 MB | 🏃 Medium | Great |
| yolo11l.pt | 115 MB | 🚶 Slower | Best |

## Example Output

```
Detected objects in image.jpg:
  person: 95.2%
  car: 87.3%
  dog: 76.8%
  bicycle: 62.1%
```

## When to Use

- User asks "what's in this image/picture/photo"
- User needs objects identified in an image
- User asks "how many people/cars/animals are in this image"
- Real-time video analysis needs
- Counting objects in a scene

