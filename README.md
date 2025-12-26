# Wavelet-Based Anomaly Detection for Sensor Signals (MATLAB)

This repository presents a **wavelet-based anomaly detection system** implemented in **MATLAB App Designer** for real-time monitoring of sensor signals.  
The project combines **Discrete Wavelet Transform (DWT)** and **statistical process control** to detect abnormal behavior such as bias, drift, and excessive noise.

The system follows a **two-stage architecture (offline training and online monitoring)** and is designed with real-time execution and interpretability in mind.

---

## 📌 Project Motivation

Many physical systems generate **non-stationary signals** where anomalies appear as transient or localized events. Classical frequency-domain techniques struggle to detect such behavior.

Wavelet-based analysis enables:
- Time–frequency localization
- Sensitivity to abrupt changes
- Efficient real-time implementation

This project demonstrates how wavelets can be used as a practical and theoretically grounded solution for **anomaly detection in sensor data**.

---

## 🧠 Methodology Overview

The proposed system consists of two main phases:

### 1. Offline Phase (Training)
- Acquisition of normal operating data
- Signal segmentation into fixed-size windows
- Multilevel DWT decomposition (Haar wavelet)
- Construction of a reference model using averaged wavelet coefficients
- Estimation of statistical control limits

### 2. Online Phase (Monitoring)
- Real-time signal acquisition
- Sliding window DWT analysis
- Distance computation to reference model
- Anomaly detection using control charts

An anomaly is detected when the distance exceeds predefined control limits.

---

## 🧩 Algorithm Description

The anomaly detection algorithm is fully documented in:

📄 **Algorithm specification**  
➡️ [`docs/anomaly_detection_algorithm.md`](docs/anomaly_detection_algorithm.md)

📘 **Wavelet theory background**  
➡️ [`docs/wavelet_theory.md`](docs/wavelet_theory.md)

These documents describe the theoretical foundation and algorithmic structure independently of the MATLAB code.

---

## 🖥️ Implementation Details

- **Language:** MATLAB
- **Interface:** App Designer
- **Wavelet:** Haar (db1)
- **Decomposition levels:** 3
- **Distance metric:** Euclidean norm
- **Detection method:** Statistical Process Control (μ ± kσ)

The system includes:
- Real-time signal visualization
- Control chart visualization
- DWT detail coefficient inspection
- Visual anomaly indicators

---

## 📁 Repository Structure

```text
.
├── app/
│   └── app1.m                     # MATLAB App Designer code
├── docs/
│   ├── wavelet_theory.md          # Wavelet theory background
│   ├── anomaly_detection_algorithm.md
│   ├── experimental_results.md    # Experimental setup and results
│   ├── figures/
│   │   ├── system_architecture.png
│   │   ├── offline_training.png
│   │   └── online_detection.png
│   └── original_report.pdf        # Original academic report 
├── README.md
└── LICENSE
