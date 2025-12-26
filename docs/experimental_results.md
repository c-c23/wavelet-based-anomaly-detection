# Experimental Setup and Results

## 1. Experimental Objective

The objective of the experimental evaluation is to validate the effectiveness of the proposed **wavelet-based anomaly detection system** under controlled conditions. The system is tested using synthetic sensor data that emulate realistic operating behavior and common fault patterns.

The experiments focus on:
- Verifying the sensitivity of the DWT-based approach to anomalies
- Evaluating real-time detection capability
- Assessing robustness under different anomaly types

---

## 2. Signal Generation and Simulation

A synthetic humidity sensor signal is generated to represent normal operating conditions with natural variability.

### Normal Operation
- Base value: 50%
- Low-frequency sinusoidal variation
- Additive Gaussian noise
- Signal bounded to the physical sensor range [0, 100] %

This signal models realistic environmental sensor behavior while allowing controlled anomaly injection.

---

## 3. System Parameters

The experimental parameters are summarized below:

| Parameter | Value |
|---------|------|
| Sampling frequency (Fs) | 8 samples/min |
| Window size | 8 samples |
| Number of training windows | 10 |
| Wavelet type | Haar (db1) |
| Decomposition levels | 3 |
| Distance metric | Euclidean norm |
| Control limit factor (k) | 2.5 |

These parameters are consistent with real-time wavelet-based monitoring literature and allow efficient online processing.

---

## 4. Offline Training Phase

During the offline phase:
1. The signal is segmented into fixed-length windows.
2. A 3-level DWT is applied to each window.
3. Wavelet coefficient vectors are extracted.
4. A reference vector is computed as the mean of all training windows.
5. Euclidean distances between each window and the reference vector are calculated.
6. Statistical control limits are defined using the mean and standard deviation of the distances.

The resulting model represents normal system behavior and serves as the baseline for anomaly detection.

---

## 5. Anomaly Injection Scenarios

To evaluate detection performance, three common anomaly types are injected during online monitoring:

### 5.1 Bias
- Sudden offset added to the signal
- Represents sensor miscalibration or offset errors
- Produces large deviations in wavelet coefficients

### 5.2 Drift
- Gradual scaling of signal amplitude
- Represents sensor aging or gradual degradation
- Detected primarily at lower-frequency wavelet levels

### 5.3 Excessive Noise
- High-variance additive noise
- Represents electromagnetic interference or sensor malfunction
- Reflected in high-frequency detail coefficients (D1)

Each anomaly type is injected randomly with a low probability to simulate realistic fault occurrence.

---

## 6. Detection Results

The proposed system successfully detected all injected anomaly types during online monitoring.

### Observations:
- Abrupt anomalies (bias, noise) triggered immediate threshold violations.
- Gradual anomalies (drift) were detected after sustained deviation.
- Normal operation remained within control limits.

The wavelet-based distance metric demonstrated strong sensitivity to abnormal behavior while maintaining stability under normal conditions.

---

## 7. Visualization and Interpretation

The system provides real-time visualization of:
- Sensor signal evolution
- Euclidean distance control chart
- Upper and lower control limits
- Wavelet detail coefficients (D1–D3)

Anomalies are clearly indicated by:
- Distance values exceeding control limits
- Visual alarm indicators in the interface
- Increased magnitude of wavelet detail coefficients

These visual tools improve interpretability and facilitate system diagnostics.

---

## 8. Discussion and Limitations

While the experimental results demonstrate effective anomaly detection, several limitations are acknowledged:

- Synthetic data may not capture all real-world complexities
- Control limits are fixed and not adaptive
- Detection performance depends on window size and wavelet selection

Future work may include:
- Testing with real sensor datasets
- Adaptive thresholding techniques
- Comparison with machine learning-based approaches

---

## 9. Reproducibility

All experiments are fully reproducible using the provided MATLAB App Designer application. The experimental setup and parameters are explicitly defined, and no external datasets are required.

---

## References

1. Mallat, S. (1999). *A Wavelet Tour of Signal Processing*. Academic Press.
2. Addison, P. S. (2017). *The Illustrated Wavelet Transform Handbook*. CRC Press.
3. Montgomery, D. C. (2013). *Introduction to Statistical Quality Control*. Wiley.
4. MathWorks. *Discrete Wavelet Transform (DWT)*, MATLAB Documentation.
