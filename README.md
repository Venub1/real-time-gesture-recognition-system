# 🖐️ Real-Time Gesture Recognition using Edge AI (Jetson)

## 🚧 Project Status: In Progress (Iterative Development)

This project presents the **ongoing development of a real-time gesture recognition system** designed for **silent communication in critical environments** using **Edge AI (NVIDIA Jetson)**.

The system detects predefined gestures such as **HELP** and **DANGER** from video input and classifies them using a **deep learning LSTM model** trained on **MediaPipe keypoint sequences**.

⚠️ **Current Stage:**
The system is implemented using **hand keypoints only**, and while it demonstrates a working pipeline, the results are **not yet optimal**.
The project is actively being extended to include **full-body keypoints (hands + shoulders + elbows + posture)** for improved performance.

---

## 🎯 Objective

* Build a real-time gesture recognition system
* Enable **silent communication** using gestures
* Deploy a **lightweight model suitable for edge devices**
* Demonstrate an **end-to-end ML pipeline**
* Iteratively improve the system using richer feature representations

---

## 🧠 Methodology

### 🔹 1. Data Collection

* Custom dataset of gesture videos (`.mov`)
* Classes used in this phase:

  * `HELP`
  * `DANGER`
* Dataset includes variations:

  * Lighting (dark, bright)
  * Noise
  * Blur
  * Flips and rotations

---

### 🔹 2. Feature Extraction (Current Approach)

* Used **MediaPipe Hand Landmarks**
* Extracted **21 keypoints per frame**
* Each frame represented as:

```text
21 keypoints × (x, y, z) → 63 features
```

* Each video converted into a sequence:

```text
(30 frames × 63 features)
```

---

### 🔹 3. Model Architecture

* Model: **LSTM (Long Short-Term Memory)**
* Input: Keypoint sequences
* Output: Gesture class (`HELP`, `DANGER`)

```text
Input → LSTM → Fully Connected Layer → Prediction
```

---

### 🔹 4. Training Setup

* Total samples: **160**
* Train/Test split: **80/20**
* Loss Function: CrossEntropyLoss
* Optimizer: Adam

---

## 📊 Results (Hand Keypoints Model)

### 🔹 Model Performance

* **Test Accuracy:** 68.75%

| Class  | Precision | Recall | F1-score |
| ------ | --------- | ------ | -------- |
| DANGER | 0.62      | 0.94   | 0.75     |
| HELP   | 0.88      | 0.44   | 0.58     |

---

### 🔹 Confusion Matrix

```text
[[15  1]
 [ 9  7]]
```

---

### 🔹 Sample Prediction

```text
Actual: HELP  
Predicted: DANGER  
Confidence: 62.24%
```

---

## ⚡ Performance (Speed)

* **Inference Time:** 0.000505 seconds
* **Estimated FPS:** ~1979 FPS

> ⚠️ Note: This measures only LSTM inference on keypoints, not full video + MediaPipe processing.

---

## 🎥 Visual Outputs

The project includes:

* Raw sample videos
* Keypoint overlay videos

Example outputs:

* `danger_hand_keypoints.mp4`
* `help_hand_keypoints.mp4`

These confirm that **keypoint extraction aligns correctly with hand motion**.

---

## ⚠️ Current Limitation

The present model relies **only on hand keypoints**, which limits its ability to fully understand gestures.

It does not capture:

* Elbow movement
* Shoulder positioning
* Body posture
* Head or facial orientation

👉 Because of this, gestures like **HELP and DANGER can appear similar**, leading to misclassification.

---

## 🚀 Ongoing Improvement (Next Phase)

The project is currently being extended to include:

* **MediaPipe Holistic (Full Body Keypoints)**
* Integration of:

  * Hands
  * Shoulders
  * Elbows
  * Upper body posture
  * (Optional) Face landmarks

### 🎯 Goal of this upgrade:

* Improve gesture differentiation
* Capture richer spatial context
* Increase model accuracy
* Move closer to **real-world deployment**

---

## 📁 Project Structure

```text
Gesture_Project_GitHub/
 ├── notebooks/
 │    └── hand_keypoints_lstm_model.ipynb
 │
 ├── scripts/
 │    └── train_danger_help.py
 │
 ├── models/
 │    └── gesture_lstm_help_danger.pth
 │
 ├── results/
 │    └── hand_keypoints_results.txt
 │
 ├── outputs/
 │    └── keypoint_videos/
 │         ├── danger_hand_keypoints.mp4
 │         ├── help_hand_keypoints.mp4
 │
 ├── dataset/
 │    ├── raw_videos/              (sample subset)
 │    ├── processed_keypoints/     (sample subset)
```

---

## 💡 Key Takeaways

* Demonstrates a complete **end-to-end ML pipeline**
* Uses **keypoint-based representation for efficiency**
* Shows importance of **temporal modeling (LSTM)**
* Highlights limitations of **partial feature representation**
* Emphasizes **iterative improvement in ML systems**

---

## 👨‍💻 Author

**Venu Bandi**
MPS Data Science — UMBC

---

## 📌 Note

Due to GitHub size constraints, only a **subset of dataset samples** is included. The full dataset was used during training.
This repository reflects an **ongoing project**, and improvements are actively being implemented.

