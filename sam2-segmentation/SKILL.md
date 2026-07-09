---
name: sam2-segmentation
description: "Precise image and video segmentation using Meta's SAM 2 (Segment Anything Model 2). Can segment any object in any image with just a point, box, or text prompt."
---

# SAM 2 Segmentation Skill

## Overview

Meta's SAM 2 (Segment Anything Model 2) — the most advanced open-source segmentation model. Can segment ANY object in ANY image without training. Supports image and video segmentation.

## Installation

```bash
pip install torch torchvision numpy opencv-python pillow
pip install git+https://github.com/facebookresearch/sam2.git
```

## Core Usage

### 1. Segment Everything (Automatic)

```python
import torch
from sam2.build_sam import build_sam2
from sam2.automatic_mask_generator import SAM2AutomaticMaskGenerator

# Load model
sam2 = build_sam2("sam2_hiera_large.yaml", "sam2_hiera_large.pt", device="cpu")
mask_generator = SAM2AutomaticMaskGenerator(sam2)

# Generate all masks
masks = mask_generator.generate("/path/to/image.jpg")
print(f"Generated {len(masks)} masks")

for m in masks:
    print(f"  Area: {m['area']}px, Confidence: {m['stability_score']:.2f}")
```

### 2. Segment with a Point Prompt

```python
from sam2.build_sam import build_sam2
from sam2.sam2_image_predictor import SAM2ImagePredictor
import numpy as np
from PIL import Image

predictor = SAM2ImagePredictor(build_sam2("sam2_hiera_large.yaml", "sam2_hiera_large.pt"))
image = np.array(Image.open("image.jpg"))
predictor.set_image(image)

# Point = (x, y) in pixels, label=1 for foreground
masks, scores, _ = predictor.predict(
    point_coords=np.array([[150, 200]]),
    point_labels=np.array([1])
)
```

### 3. Segment with a Box Prompt

```python
masks, scores, _ = predictor.predict(
    box=np.array([50, 50, 300, 400]),  # x1, y1, x2, y2
    multimask_output=True
)
```

## Model Sizes

| Variant | Size | Speed |
|---------|------|-------|
| sam2_hiera_tiny.pt | 140 MB | ⚡ Fastest |
| sam2_hiera_small.pt | 460 MB | ⚡ Fast |
| sam2_hiera_large.pt | 2.5 GB | 🏃 Full quality |

## Video Segmentation

```python
from sam2.build_sam import build_sam2_video_predictor

predictor = build_sam2_video_predictor("sam2_hiera_large.yaml", "sam2_hiera_large.pt")
predictor.init_state(video_path="/path/to/video/frames/")

# Add mask on first frame
predictor.add_mask(0, np.array([[100, 100]]), np.array([1]))
# Propagate through all frames
for i in range(1, len(video_frames)):
    mask = predictor.propagate_in_video(i)
```

## When to Use

- Precise object isolation/removal from images
- "Select/cut out this object from the image"
- "Segment the person/car/building in this image"
- Video object tracking and segmentation
- Generating masks for further processing

