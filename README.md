# NUML Traffic Detection Dataset and YOLO Fine-Tuning

A custom traffic detection project developed for the final-year project titled: **Real-Time Traffic Choking Point Detector** at the **National University of Modern Languages (NUML), Islamabad, Pakistan**.

This repository contains the implementation and documentation for fine-tuning a YOLO model on a self-collected and manually annotated traffic dataset built specifically for traffic monitoring and choking-point detection in urban environments.

> Quick access: [Open the fine-tuning notebook in Google Colab](https://colab.research.google.com/drive/12Txu1gJ21R1P4P9uC7jpQdc_psE-5UE6?usp=sharing)
> Quick access: [Open the Dataset](https://www.kaggle.com/datasets/muhammadawaisqrni/yolo-numl-dataset-1-0)

---

## Project Overview

This project focuses on detecting critical traffic participants and objects in real-world road scenes. The custom dataset includes four classes:

- Controller
- Human
- Numl_Bus
- Vehicle

The goal is to develop a robust real-time detection model capable of identifying pedestrians, vehicles, traffic controllers, and university buses in Islamabad traffic scenarios.

The model was trained using a YOLO-based architecture and fine-tuned on a custom dataset to support intelligent traffic monitoring and safety applications.

---

## Dataset

### Dataset Name
**NUML Traffic Detection Dataset (YOLO format, 4 classes)**

### Dataset Description
This dataset was self-collected and manually annotated from traffic scenes in Islamabad, Pakistan. It was created to support research in real-time object detection and multi-object tracking for traffic video analytics.

### Dataset Statistics

- Total images: **1,672**
- Total labeled objects: **6,612**
- Format: **YOLO**
- One label file per image in the format:
  `class x_center y_center width height`
- Split: **80/10/10**
  - Train: **1,342**
  - Validation: **168**
  - Test: **162**

### Classes

| Class ID | Class Name | Description |
|---------|------------|-------------|
| 0 | Controller | Traffic warden / police officer / traffic management personnel |
| 1 | Human | Pedestrians and people on foot |
| 2 | Numl_Bus | University buses operated by NUML |
| 3 | Vehicle | Cars, motorcycles, rickshaws, and other road vehicles |

### Test-Split Distribution

| Class | Instances |
|-------|-----------|
| Controller | 131 |
| Human | 221 |
| Numl_Bus | 237 |
| Vehicle | 210 |
| Total | 799 |

---

## Collection and Annotation Details

### Data Collection
- Where: **Islamabad, Pakistan**
- Scenario: **Traffic scenes and choking points**
- Capture environment: **Real-world road and junction footage**
- Camera(s): **[Insert camera/device details]**
- Resolution: **[Insert image resolution or camera specification]**
- Time conditions: **[Daylight only / day and night / weather conditions]**

### Annotation Process
- Annotation tool: **[Roboflow / LabelImg / CVAT / Manual annotation]**
- Annotated by: **[Annotator name(s)]**
- Review process: **[Manual verification / quality checks / review by experts]**
- Split method: **[Random split / by video to avoid near-duplicate frames across train/validation/test]**

---

## Model and Training

The project uses a **YOLOv8n** model with approximately **3.0M parameters**, fine-tuned for 282 epochs on a **Tesla T4 GPU**.

### Training Summary

| Metric | Value |
|--------|-------|
| Model | YOLOv8n |
| Parameters | 3.0M |
| Epochs | 282 |
| Hardware | Tesla T4 |
| Framework | Ultralytics 8.3.233 |

### Performance Results

| Split | mAP@50 | mAP@50-95 | Precision | Recall |
|-------|--------|-----------|-----------|--------|
| Validation | 89.5% | 59.3% | 86.4% | 84.7% |
| Test (162 images) | 89.1% | 54.8% | 82.2% | 86.8% |

### Per-Class Test mAP@50

| Class | mAP@50 |
|-------|--------|
| Numl_Bus | 95.9% |
| Controller | 94.2% |
| Vehicle | 89.7% |
| Human | 76.6% |

### Interpretation

- The model performs strongly on bus and controller detection.
- Vehicle detection is also robust.
- Human detection is comparatively harder due to more variability in pose, occlusion, and clutter.
- The main source of errors is often background false positives rather than severe class confusion.

---

## Model Limitations

- Limited to a specific region of Islamabad and may not generalize to other cities.
- Dataset size is relatively small for broader deployment.
- Human detection remains challenging in crowded or partially occluded scenes.
- Environmental variability such as lighting conditions, weather, and camera differences may affect performance.
- Additional data collection may be required for real-world generalization.

---

## Privacy Statement

This dataset was created with privacy in mind. Faces and license plates were handled to avoid personal identification, either by being not visible at the chosen resolution or by applying privacy-preserving techniques such as blurring.

---

## Notebook and Colab Access

This project was trained in a large notebook environment, and due to notebook size and runtime constraints, the full model training workflow is shared through Google Colab.

### Colab Notebook

[Open the fine-tuning notebook in Google Colab](https://colab.research.google.com/drive/12Txu1gJ21R1P4P9uC7jpQdc_psE-5UE6?usp=sharing)

This notebook includes:
- Dataset loading and preprocessing
- YOLO annotation validation
- Training setup and hyperparameters
- Model fine-tuning
- Evaluation and result analysis
- Inference on images and videos

---

## Repository Structure

```text
FYP_YOLO_FINE-TUNING/
├── README.md
├── data/
│   ├── images/
│   │   ├── train/
│   │   ├── val/
│   │   └── test/
│   └── labels/
│       ├── train/
│       ├── val/
│       └── test/
├── notebooks/
│   └── YOLO_fine_tuning.ipynb
├── runs/
│   └── detect/
├── weights/
│   └── best.pt
├── scripts/
│   ├── train.py
│   ├── detect.py
│   └── evaluate.py
├── requirements.txt
└── LICENSE
```

---

## Getting Started

### Requirements

```bash
pip install ultralytics opencv-python numpy matplotlib
```

### Train the Model

```bash
python train.py
```

### Run Inference

```bash
python detect.py --weights weights/best.pt --source input.jpg
```

---

## License

The project may use an open license such as:

- **CC BY 4.0**
- **CC BY-NC-SA 4.0**
- Or another license depending on your institutional and publication requirements

Please update this section with the final license chosen for the project.

---

## Citation

Awais, M. (2026). NUML Traffic Detection Dataset (YOLO format, 4 classes). Kaggle. [URL]

---

## Contact

Muhammad Awais  
Email: muhammad.awais.swe@gmail.com  
Portfolio: https://muhammad-awais-swe.vercel.app/

---

## Author

This project was developed by **Muhammad Awais** as part of the final-year project work at **NUML, Islamabad**.

---

## Acknowledgments

- National University of Modern Languages (NUML), Islamabad
- Traffic dataset collection team
- Annotation contributors and reviewers
- Open-source YOLO ecosystem and Ultralytics community

---

## Final Note

This project demonstrates the practical use of deep learning for real-world traffic detection and contributes to the development of intelligent traffic monitoring systems in Pakistan. The results show that a custom YOLO model can be effectively fine-tuned for relevant detection tasks using a targeted, domain-specific dataset.
