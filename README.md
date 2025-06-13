# ♥️ ECG Noise Removal Using Butterworth Low-Pass Filter

This DSP project implements a **4th-order Butterworth low-pass filter** to remove high-frequency noise (100 Hz) from ECG signals, enhancing cardiac diagnosis.

---

## 🎓 Project Info

* **University**: Sukkur IBA University
* **Department**: Computer Systems Engineering
* **Project Title**: ECG Noise Removal Using Butterworth Low-Pass Filter
* **Submitted By**: Nimerta Wadhwani
* **Supervisor**: Sir Asif Ali

---

## 🌎 Abstract

Electrocardiograms (ECGs) are prone to noise that can obscure diagnostic features like QRS, P, and T waves. This project applies a **Butterworth low-pass filter** with a 40 Hz cutoff to eliminate 100 Hz synthetic noise simulating muscle artifacts. Using Python, the filter performance is evaluated through **Signal-to-Noise Ratio (SNR)** and **Mean Squared Error (MSE)**, confirming effective noise suppression.

---

## 🔢 Methodology

### 1. Data Acquisition

* **Source**: MIT-BIH Arrhythmia Database (record 100)
* **Library**: `wfdb`
* **Sampling Rate**: 360 Hz

### 2. Noise Simulation

* Added 100 Hz sine wave (0.1 amplitude) to the original ECG

```python
noise = 0.1 * np.sin(2 * np.pi * 100 * t)
noisy_ecg = ecg + noise
```

### 3. Filter Design

* **Type**: Butterworth low-pass
* **Order**: 4
* **Cutoff**: 40 Hz
* **Library**: `scipy.signal`

```python
b, a = signal.butter(4, 40 / (fs / 2), btype='low')
filtered_ecg = signal.lfilter(b, a, noisy_ecg)
```

### 4. Performance Metrics

| Metric | Noisy ECG | Filtered ECG |
| ------ | --------- | ------------ |
| SNR    | 8.73 dB   | -0.04 dB     |
| MSE    | 0.0050    | 0.0377       |

---

## 🌐 Visualization & Analysis

* **Time-Domain**: Noisy ECG obscures QRS, while filtered ECG restores clear waveform
* **Frequency-Domain**: FFT confirms attenuation of 100 Hz component
* **Filter Response**: Shows flat passband and sharp roll-off after 40 Hz
* **Comparison Chart**: SNR/MSE bar plots highlight improved performance

---

## 🚀 Discussion & Insights

### Trade-offs:

* **Cutoff Frequency**: 40 Hz preserves diagnostic features while reducing 100 Hz noise
* **Filter Order**: Higher order would improve roll-off but increase complexity

### Limitations:

* Only simulates 100 Hz noise (muscle artifacts)
* Fixed parameters may not adapt to real-world ECGs
* Single record (record 100) tested

---

## 📊 Future Improvements

* Add **notch filters** for 50 Hz powerline noise
* Use **adaptive filters** (e.g., LMS, Kalman)
* Apply to broader ECG datasets (e.g., arrhythmic cases)
* Explore **wavelet denoising** or ML-based methods

---

## 📖 References

1. PhysioNet MIT-BIH Arrhythmia Database
2. SciPy Signal Processing Docs
3. Oppenheim & Schafer, *Discrete-Time Signal Processing*
4. Proakis & Manolakis, *Digital Signal Processing*
5. Goldberger et al., *PhysioBank/PhysioNet Resources*

---

> ✨ *Preserving heartbeats through clean signals. A biomedical DSP application using real-world ECG data and classical filter design.*
