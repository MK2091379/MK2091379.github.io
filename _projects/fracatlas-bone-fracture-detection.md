---
layout: page
title: FracAtlas Bone Fracture Classification & Segmentation
description: End-to-End CAD Radiographic Framework Combining DenseNet-121, ResNet-34 U-Net, and Meta's SAM for Zero-Shot Boundary Delineation.
importance: 2
category: ai-ml
github: https://github.com/MK2091379/fracatlas-bone-fracture-detection
---

## Overview

Accurate radiological interpretation of bone fractures requires both rapid patient-level screening and fine-grained spatial localization. Subtle hairline fissures, complex peri-articular dislocations, and anatomical overlaps across diverse projections (frontal, lateral, oblique) frequently challenge conventional computer-aided diagnosis (CAD) pipelines.

This project delivers an end-to-end multi-task deep learning framework (**FracAtlas**) designed for automated bone fracture detection and pixel-level lesion segmentation from digital radiographs. The pipeline integrates a decoupled architecture: global binary classification via **DenseNet-121**, dense semantic segmentation via a **ResNet-34 U-Net**, and zero-shot foundation boundary delineation using Meta's **Segment Anything Model (SAM)** guided by geometric bounding-box prompts.

---

## Architectural Pipeline

* **Data Engineering & Stream Sanitization:** Ingests raw radiography streams, handling truncated or corrupt JPEG encodings via low-level PIL/C-library handlers (`ImageFile.LOAD_TRUNCATED_IMAGES`), paired with dynamic Albumentations transforms.
* **Global Classification Head (DenseNet-121):** Predicts patient-level fracture probability with dense feature reuse and direct gradient backpropagation paths to mitigate vanishing gradients.
* **Semantic Localization Head (ResNet34-UNet):** Decodes fine-grained pixel masks trained via a composite `BCEWithLogitsLoss` and `DiceLoss` objective to counter extreme background-to-lesion class imbalance.
* **Zero-Shot Boundary Prompting (Meta SAM ViT-B):** Integrates vision foundation models conditioned on COCO bounding-box coordinates to isolate complex boundary geometries and non-displaced diaphyseal shaft fractures.
* **Decoupled Inference Engine:** Executes conditional segmentation gating and visualizes global classification confidence alongside side-by-side ground truth and predicted spatial masks.

---

## Technical Highlights & Methodological Insights

### 1. Multi-Task Decoupling & Sensitivity Calibration
* **Calibrated Decision Boundaries:** To maximize clinical recall in emergency room triage, the segmentation inference head utilizes a lowered probability threshold ($0.20 \le \tau \le 0.30$), prioritizing lesion sensitivity over conservative precision.
* **Diagnostic Discordance Handling:** Empirical evaluations reveal cases where global classifiers report low fracture confidence ($P < 0.05$) while the spatial segmentation head resolves exact morphological boundaries, demonstrating the necessity of decoupled, multi-tier CAD architectures.

### 2. Anatomical Generalization
* High-density joint and peri-articular structures (such as the distal radius, wrist, and ankle) achieve superior segmentation precision ($\text{IoU} > 0.90$, maximum probability $\ge 0.98$).
* For hairline fractures lacking obvious cortical disruption, explicit geometric prompt engineering via SAM ViT-B recovers crisp topological contours where standard convolutional backbones experience boundary blurring.

---

## Dataset & Annotation Schema

Evaluated on the benchmark **FracAtlas Dataset** (Nature Scientific Data):
* **Payload:** 4,083 clinical radiographs across hand, leg, hip, and shoulder anatomies.
* **Labels & Targets:** 717 confirmed fractured cases and 3,366 healthy scans paired with dense COCO polygon masks and bounding boxes.
* **Projections:** Multi-view evaluations spanning frontal (AP/PA), lateral, and oblique views.

---

## Technical Stack

* **Deep Learning Runtime:** Python 3.8+, PyTorch, Torchvision
* **Segmentation Architectures:** `segmentation-models-pytorch`, Meta Segment Anything Model (`segment-anything`)
* **Computer Vision & Augmentations:** OpenCV, Albumentations, PIL, PyCOCOTools
* **Evaluation & Analytics:** Scikit-Learn (IoU, Dice, Precision, Recall, ROC-AUC), NumPy, Pandas