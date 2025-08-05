# 🎯 YOLOv8 Object Detection: Custom Dataset + Video Inference

This project demonstrates object detection using **Ultralytics YOLOv8**. It includes:
- Detection on real-world video
- Training on a custom object dataset (6 classes)
- Evaluating performance using precision, recall, and mAP metrics
- Saving inference outputs and annotated results

---

## 🎬 Video Inference Pipeline

1. Extract frames from input video using `OpenCV`.
2. Load pre-trained YOLOv8s model (`yolov8s.pt`).
3. Run inference frame-by-frame.
4. Draw bounding boxes and class labels.
5. Save annotated frames and compile into `After_Inference.mp4`.

> ✅ Total frames processed: **193**
> 🛠️ Detected classes: person, car, truck, traffic light, fire hydrant

---

## 📦 Custom Dataset Setup

* Dataset contains **6 object classes**:

  * Hammer, Pliers, Rope, Screw Driver, Tool Box, Wrench
* Used **YOLO format** with labels for training/validation/test split
* Dataset YAML configured with `nc=6` and class names

---

## 🧠 Model Training

```bash
yolo task=detect mode=train model=yolov8s.pt data=data.yaml epochs=25 imgsz=224 batch=16
```

* **Model**: YOLOv8s (pretrained)
* **Epochs**: 25
* **Batch Size**: 16
* **Image Size**: 224x224

> 🚀 Model saved to: `runs/detect/train2/weights/best.pt`

---

## 📊 Evaluation Results

### 📌 Final Validation Metrics:

| Metric            | Value |
| ----------------- | ----- |
| **mAP\@0.5**      | 76.2% |
| **mAP\@0.5:0.95** | 60.4% |
| **Precision**     | 69.4% |
| **Recall**        | 69.8% |

### 📈 Per-Class Performance:

| Class        | Precision | Recall | mAP\@0.5 | mAP\@.5:.95 |
| ------------ | --------- | ------ | -------- | ----------- |
| Hammer       | 78.1%     | 59.4%  | 79.8%    | 65.5%       |
| Pliers       | 60.9%     | 75.0%  | 77.3%    | 52.1%       |
| Rope         | 92.2%     | 90.7%  | 90.5%    | 77.1%       |
| Screw Driver | 47.1%     | 35.7%  | 38.9%    | 29.8%       |
| Tool Box     | 51.4%     | 100%   | 94.4%    | 78.9%       |
| Wrench       | 86.5%     | 58.3%  | 76.4%    | 59.1%       |

---

## 📉 Visual Outputs

* ✅ `confusion_matrix.png`
* ✅ `results.png` (F1, PR, Loss curves)
* ✅ Inference predictions: `val_batch0_pred.jpg`

---

## 📦 Inference on Test Set

```bash
yolo task=detect mode=predict model=runs/detect/train2/weights/best.pt conf=0.25
```

### Sample Predictions:

* Detected multiple tools like Hammer, Wrench, and Screw Driver with high confidence.
* Output images saved in YOLO’s `runs/detect/predict/` folder.

---

## 🧠 Key Learnings

* **YOLOv8** is fast and accurate for both image and video tasks.
* Transfer learning on custom objects works well with 25 epochs.
* Label quality and class distribution directly affect mAP scores.
* Video inference requires frame-by-frame preprocessing and reassembly.

---

## 🏁 Conclusion

This project showcases:

* Training and inference with YOLOv8 on custom datasets
* Pipeline for real-world video analysis
* Effective use of Ultralytics API and result visualizations

---
