# Spatial–Temporal Confidence-Weighted Parking Occupancy Inference
*(Detector-Agnostic Framework for Vision-Based Parking Systems)*

This repository contains the **official implementation** of the framework presented in the paper:

> **Reliable Parking Occupancy Inference Using Spatial–Temporal Confidence Fusion in Vision-Based Systems**

The proposed system performs **parking occupancy inference** by combining **object detection outputs**, **custom-defined parking slot boundaries**, and **temporal stability reasoning**.  
The implementation is **detector-agnostic** and has been experimentally validated using multiple state-of-the-art object detection models.

---

## 🔍 Overview

Unlike conventional frame-level parking detection approaches, this framework focuses on **decision reliability** rather than raw detection accuracy. Vehicle detections are fused with spatial priors (parking slot boundaries) and temporal evidence accumulation to produce **stable occupancy decisions**.

This repository includes:
- Custom parking slot boundary definition (GUI-based)
- Detector-agnostic vehicle detection pipeline
- Confidence-weighted spatial overlap logic
- Temporal Stability Index (TSI)–based inference
- Experimental scripts used for evaluation in the paper

---

## 🚗 Supported Models (As Evaluated in the Paper)

### Object Detection Models
- **RetinaNet**
- **SSD**
- **YOLOv8**
- **YOLOv9**

> These models were evaluated under identical experimental conditions to demonstrate the detector-agnostic nature of the proposed spatial–temporal inference framework.

### Classification Models (Baseline Comparison Only)
- ResNet50  
- VGG16  
- AlexNet  
- MobileNet  

> Classification-based methods are included for comparative analysis but are **not the core contribution** of the paper.

---

## ✨ Key Features

### 1. Custom Parking Slot Boundary Definition
- GUI-based boundary annotation using four-point polygon selection
- Multiple parking slots supported per camera view
- Boundaries are defined once and reused across experiments

### 2. Detector-Agnostic Occupancy Inference
- Vehicle detection performed using selected deep learning models
- Confidence-weighted spatial overlap between detected vehicles and parking slots
- Temporal evidence accumulation using a fixed sliding window

### 3. Temporal Stability Index (TSI)
- Aggregates spatial evidence across consecutive frames
- Suppresses false occupancy transitions caused by occlusions and transient detections
- Produces stable **Occupied / Free / Uncertain** states, as described in the paper

---

## 🧪 Experimental Configuration (Paper-Aligned)

- **Temporal Window Size:** `T = 10` frames  
- **Decision Thresholds:**  
  - Occupied: `θ_occ = 0.7`  
  - Free: `θ_free = 0.3`
- **Inference Mode:** Offline video processing
- **Evaluation Focus:** Occupancy decision stability and reliability

> Predictions classified as *Uncertain* are excluded from precision, recall, accuracy, and F1-score computation, following the evaluation protocol described in the paper.

---

## ▶️ Usage

### Step 1: Configure Parking Slot Boundaries
```bash
python Config_Generator.py
```
1. Load a parking surveillance video  
2. Extract the first frame automatically  
3. Manually draw parking slot boundaries using four points  
4. Save the configuration file for reuse  

---

### Step 2: Run Parking Occupancy Inference

#### Detection-Based Inference (Primary Method)
```bash
python Parking_Occupation_Detector_Using_Detection.py
```
- Load the saved boundary configuration
- Select one of the supported detection models via the GUI
- Observe real-time visualization of:
  - Vehicle detections
  - Parking slot occupancy status
- Processed frames can be optionally saved for analysis

---

#### Classification-Based Inference (Baseline Only)
```bash
python Parking_Occupation_Detector_Using_Classification.py
```
> Included for comparative evaluation only; not the main contribution of the paper.

---

## ⚙️ Performance and Computational Cost

- The Temporal Stability Index (TSI) computation involves only simple summation and averaging operations.
- Additional latency introduced by the temporal inference layer is **less than 1 ms per frame**, making the framework suitable for **real-time and edge-based deployment**, subject to the chosen detector.

---

## 📊 Dataset Notes

- Experiments were conducted on real-world outdoor parking surveillance videos
- Fixed camera viewpoints with multiple lighting conditions (daytime, evening, low-light)
- Parking slots were manually annotated per camera view
- Frame sampling was used to reduce redundancy while preserving temporal continuity

*(Exact dataset statistics are reported in the paper.)*

---

## 📄 Citation

If you use this code, please cite the corresponding paper:

```bibtex
@article{YourPaper2025,
  title   = {Reliable Parking Occupancy Inference Using Spatial--Temporal Confidence Fusion in Vision-Based Systems},
  author  = {Author Names},
  journal = {Journal Name},
  year    = {2025}
}
```

---

## ⚠️ Notes

- This repository reflects the **exact implementation evaluated in the paper**
- No additional modules (e.g., tracking, re-identification) are included beyond what is reported
- The framework is designed to be extended with future detection models

---

## 📬 Contact

For questions, clarifications, or research collaboration, please contact the repository maintainer.
