# Wavelet-Based Anomaly Detection Algorithm

## 1. Overview

This project implements a **wavelet-based anomaly detection algorithm** for real-time monitoring of sensor signals. The method combines multiresolution signal analysis using the Discrete Wavelet Transform (DWT) with statistical process control techniques.

The algorithm is divided into two main stages:
- **Offline phase:** construction of a reference model using normal operating data.
- **Online phase:** real-time monitoring and anomaly detection based on deviations from the reference model.

This structure follows standard approaches in wavelet-based fault detection and computational intelligence systems.

**Reference:**  
Mallat, S. (1999). *A Wavelet Tour of Signal Processing*. Academic Press.

---

## 2. Offline Phase: Reference Model Construction

The offline phase assumes that the system operates under normal conditions. Its objective is to build a statistical reference model representing normal behavior.

### Steps:

1. Acquire a signal under normal operating conditions.
2. Segment the signal into fixed-length windows.
3. Apply a multilevel DWT to each window.
4. Extract the wavelet coefficient vectors.
5. Compute a reference vector as the mean of all coefficient vectors.
6. Calculate the Euclidean distance between each window and the reference vector.
7. Estimate statistical control limits based on the distance distribution.

The resulting model consists of:
- A reference coefficient vector
- Mean distance (μ)
- Standard deviation (σ)
- Upper and lower control limits

---

## 3. Online Phase: Real-Time Monitoring

During online operation, the system continuously monitors incoming sensor data.

### Steps:

1. Acquire new sensor samples.
2. Update a sliding window buffer.
3. Apply the same multilevel DWT used in the offline phase.
4. Compute the Euclidean distance between the current window coefficients and the reference vector.
5. Compare the distance with the predefined control limits.
6. Trigger an anomaly alarm if the distance exceeds the limits.

This approach enables the detection of abrupt changes, drifts, or abnormal noise patterns.

---

## 4. Distance Metric and Control Limits

### Distance Metric

The deviation between the current signal window and the reference model is quantified using the **Euclidean distance**:

\[
d = \| \mathbf{c}_{current} - \mathbf{c}_{ref} \|_2
\]

where:
- \( \mathbf{c}_{current} \) is the wavelet coefficient vector of the current window,
- \( \mathbf{c}_{ref} \) is the reference coefficient vector.

### Control Limits

Control limits are defined statistically as:

\[
UCL = \mu + k\sigma
\]
\[
LCL = \max(0, \mu - k\sigma)
\]

where:
- \( \mu \) is the mean distance during training,
- \( \sigma \) is the standard deviation,
- \( k \) is a design parameter (typically between 2.5 and 3).

This method is consistent with Statistical Process Control (SPC) theory.

**Reference:**  
Montgomery, D. C. (2013). *Introduction to Statistical Quality Control*. Wiley.

---

## 5. Detection Rule

An anomaly is detected if:

\[
d > UCL \quad \text{or} \quad d < LCL
\]

If the distance remains within the control limits, the system is considered to operate normally.

This decision rule corresponds to threshold-based anomaly detection commonly used in industrial monitoring systems.

---

## 6. Algorithm Pseudocode

```text
OFFLINE PHASE:
Input: Normal signal x[n]
Output: Reference vector c_ref, UCL, LCL

1. Segment x[n] into windows of length N
2. For each window:
      Compute DWT coefficients c_i
3. Compute reference vector:
      c_ref = mean(c_i)
4. For each window:
      Compute distance d_i = ||c_i - c_ref||
5. Compute μ and σ from {d_i}
6. Define control limits UCL and LCL

ONLINE PHASE:
Input: Incoming signal y[n]
Output: Anomaly alarm

1. Update sliding window with new samples
2. Compute DWT coefficients c_current
3. Compute distance d = ||c_current - c_ref||
4. If d > UCL or d < LCL:
      Raise anomaly alarm
   Else:
      System operates normally
