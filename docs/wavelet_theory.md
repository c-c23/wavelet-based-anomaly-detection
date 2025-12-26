# Discrete Wavelet Transform (DWT) – Theoretical Background

## 1. Motivation

Real-world signals obtained from physical systems, such as structural vibrations or environmental sensors, are typically **non-stationary**, meaning their statistical properties vary over time. Classical Fourier-based methods provide global frequency information but fail to localize transient events, abrupt changes, or anomalies in time.

The Discrete Wavelet Transform (DWT) overcomes this limitation by enabling **time–frequency localization**, making it especially suitable for:
- Fault detection
- Structural health monitoring (SHM)
- Anomaly detection in sensor signals

This project employs the DWT as the core signal processing technique for detecting abnormal behavior in a simulated humidity sensor.

**Reference:**  
Mallat, S. (1999). *A Wavelet Tour of Signal Processing*. Academic Press.

---

## 2. Discrete Wavelet Transform Overview

The DWT decomposes a discrete-time signal into a set of coefficients representing different frequency bands at multiple resolutions. This process is known as **multiresolution analysis (MRA)**.

At each decomposition level, the signal is split into:
- **Approximation coefficients (A)**: low-frequency components
- **Detail coefficients (D)**: high-frequency components

Mathematically, the signal \( x[n] \) is represented as:

\[
x[n] = A_J[n] + \sum_{j=1}^{J} D_j[n]
\]

where:
- \( J \) is the number of decomposition levels,
- \( D_j \) captures signal variations at scale \( j \).

This hierarchical representation allows the detection of localized disturbances that are often associated with anomalies.

**Reference:**  
Daubechies, I. (1992). *Ten Lectures on Wavelets*. SIAM.

---

## 3. Haar Wavelet Selection

In this work, the **Haar wavelet** (Daubechies order 1, db1) is used due to the following properties:

- Extremely low computational complexity
- Orthogonality and compact support
- High sensitivity to abrupt changes and discontinuities
- Suitability for real-time and embedded implementations

These characteristics make the Haar wavelet particularly effective for detecting sudden deviations such as bias, drift, or excessive noise in sensor signals.

**Reference:**  
MathWorks, *Choosing a Wavelet*, MATLAB Documentation.

---

## 4. Multi-Level Decomposition and Physical Interpretation

A 3-level DWT decomposition is applied to each signal window in the system:

- **D1 (Level 1 detail coefficients):**  
  Captures high-frequency components, typically associated with noise or sudden spikes.

- **D2 (Level 2 detail coefficients):**  
  Represents medium-scale variations and transient behavior.

- **D3 (Level 3 detail coefficients):**  
  Corresponds to lower-frequency trends and gradual changes.

Abrupt changes or faults in the signal manifest as **large-magnitude detail coefficients**, particularly in the lower decomposition levels.

This interpretation is consistent with wavelet-based singularity detection theory.

**Reference:**  
Mallat, S., & Hwang, W. L. (1992). *Singularity Detection and Processing with Wavelets*.  
IEEE Transactions on Information Theory, 38(2), 617–643.

---

## 5. Wavelets and Anomaly Detection

Wavelet theory establishes that **discontinuities or irregularities in a signal produce localized peaks in wavelet coefficients**. This property forms the theoretical basis for wavelet-based anomaly detection.

In this project:
- Each signal window is transformed using DWT
- The resulting coefficient vector is compared to a reference model
- Deviations are quantified using Euclidean distance
- Control limits are defined statistically (mean ± k·σ)

This approach aligns with wavelet-based computational intelligence methods reported in the literature.

**Reference:**  
Addison, P. S. (2017). *The Illustrated Wavelet Transform Handbook*. CRC Press.

---

## 6. Relevance to This Implementation

The theoretical concepts described above directly support the MATLAB implementation in this repository:

- `wavedec()` is used to compute multilevel DWT coefficients
- Haar wavelet enables real-time execution
- Detail coefficients (D1–D3) are monitored for abnormal behavior
- Distance-based control charts are used for anomaly detection

This combination provides a computationally efficient and theoretically grounded framework for real-time sensor monitoring.

---

## References

1. Mallat, S. (1999). *A Wavelet Tour of Signal Processing*. Academic Press.
2. Daubechies, I. (1992). *Ten Lectures on Wavelets*. SIAM.
3. Mallat, S., & Hwang, W. L. (1992). *Singularity Detection and Processing with Wavelets*. IEEE Transactions on Information Theory.
4. Addison, P. S. (2017). *The Illustrated Wavelet Transform Handbook*. CRC Press.
5. MathWorks. *Discrete Wavelet Transform (DWT)*, MATLAB Documentation.
