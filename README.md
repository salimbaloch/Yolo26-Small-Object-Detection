# Yolo26
Fine-tuned YOLOv26-OBB (oriented bounding box) model from Ultralytics for ship detection in aerial/satellite imagery. Converts Pascal VOC annotations → YOLO OBB format, trains on custom ship dataset, evaluates, predicts &amp; visualizes rotated detections.
# Ship Detection using YOLOv26-OBB (Oriented Bounding Boxes)

<img src="https://img.shields.io/badge/YOLOv26-EE4C2C?style=for-the-badge&logo=ultralytics&logoColor=white"/>  
<img src="https://img.shields.io/badge/OBB-Oriented%20Bounding%20Box-blue?style=for-the-badge"/>  
<img src="https://img.shields.io/badge/Ultralytics-00A3E0?style=for-the-badge"/>  
<img src="https://img.shields.io/badge/Ship%20Detection-Aerial%20Imagery-green?style=for-the-badge"/>

End-to-end pipeline that fine-tunes **YOLOv26-OBB** — the latest Ultralytics model (released Jan 2026) — for **oriented ship detection** in aerial and satellite images.  

YOLOv26-OBB natively supports rotated bounding boxes (via 4 corner points + rotation), which is ideal for maritime monitoring, port surveillance, and remote sensing where ships appear at arbitrary angles.

## Key Features

- Converts Pascal VOC XML annotations → YOLO OBB format (`class x1 y1 x2 y2 x3 y3 x4 y4`)
- Stratified dataset split (70% train / 15% val / 15% test)
- Downloads pretrained **YOLOv26-n-OBB** from Hugging Face
- Trains with Ultralytics API + augmentations suited for aerial views (rotation, flip, mosaic, etc.)
- Validates with mAP50 / mAP50-95
- Runs inference on test set → saves predictions + confidence stats
- Visualizes rotated bounding boxes (polygons + corners)
- Exports model to ONNX / TorchScript for deployment
- Extracts detection statistics (confidence distribution, ships per image)

## Results (example from notebook – update with your numbers)

| Metric          | Value    | Notes                          |
|-----------------|----------|--------------------------------|
| mAP@50 (val)    | ~0.82–0.89 | Depends on epochs & aug       |
| mAP@50:95 (val) | ~0.58–0.68 | Typical for single-class OBB  |
| Avg Confidence  | ~0.78–0.85 | Test set predictions          |
| Avg ships/image | ~1.4–2.1 | Varies by image density       |

## Repository Structure

```text
.
├── yolo26-small-object-detection.ipynb     # Main notebook (full pipeline)
├── ship_dataset/                           # Converted dataset (created during run)
│   ├── data.yaml
│   ├── images/
│   │   ├── train/  val/  test/
│   └── labels/
│       ├── train/  val/  test/
├── runs/                                   # Training logs, weights, predictions
│   ├── ship_yolov26_obb*/              # Training runs
│   └── test_predictions/               # Visualized inference results
├── ship_detections.csv                     # Extracted OBB predictions (CSV)
└── README.md
