# Sagiv Bar — Portfolio

Signal processing, estimation and machine learning. Currently an algorithm engineer at
**Starbird**, working on satellite-based positioning — signal acquisition and tracking,
Doppler-based navigation solutions, and the estimation and calibration layers between raw
RF and a position fix.

**Live site:** https://sagiv-bar.github.io &nbsp;·&nbsp;
**LinkedIn:** https://www.linkedin.com/in/sagiv-bar

---

## 1. Blind Noise Estimation & BM3D Denoising

*Image processing · Statistical estimation*

BM3D is one of the strongest denoisers available — but it has to be told the noise standard
deviation, which in practice you don't know. This project estimates σ directly from the noisy
image and then feeds it to BM3D.

**Approach.** The image is split into 6×6 patches and each patch is scored by a gradient
texture index (Sobel). Textured patches are rejected, and σ is estimated from the remaining
flat patches using a chi-square confidence bound on the pooled variance. The flat/textured
threshold is re-derived from the current estimate and the process iterates until the relative
change in variance falls below 10⁻³. The converged σ drives BM3D hard-thresholding.

**Evaluation.** MSE, SNR, PSNR, SSIM and Pearson correlation against the clean reference.

**Stack.** Python · OpenCV · SciPy (χ² distribution) · BM3D · scikit-image

[→ Notebook](Gaussian_Noise_Estimation_and_Denoising_Using_BM3D_Algorithm.ipynb)

---

## 2. BLE Distance Estimation with Neural Networks

*RF · Indoor positioning · Deep learning*

Mapping BLE signal strength (RSSI) to distance is the core problem in beacon-based indoor
positioning, and analytic path-loss models degrade badly indoors because of multipath and
absorption. Here the mapping is learned from measurements instead.

**Approach.** A three-beacon setup with known geometry; ground-truth distances are derived
from recorded positions, normalised, and regressed from the RSSI vector using fully connected
networks. Four depths (128–64 through 128–64–32–16–8) were swept against three activations
(sigmoid, ReLU, tanh), with held-out R² tracked across 250 epochs so architectures are compared
on convergence behaviour rather than a single final number.

**Stack.** TensorFlow · Keras · scikit-learn · NumPy

[→ Notebook](Estimation_of_BLE_Signal_Distance_Using_Artificial_Neural_Networks.ipynb)

---

## 3. Diabetes Classification — Classical ML vs. Deep Learning

*Applied ML · Imbalanced data*

A ~15,000-record health dataset with a strong class imbalance, used to compare a tuned Random
Forest against a tuned deep network end to end: EDA, correlation and outlier analysis, feature
engineering, scaling, then grid search over both model families and over class-balancing
strategies.

**Results.** The best model reaches **97.1% accuracy**, but the numbers that actually describe
it are **F1 = 0.80** and **ROC AUC = 0.967**. A second configuration with almost the same
accuracy (95.3%) collapses to **F1 = 0.61** — a clean demonstration of why accuracy is the wrong
metric on imbalanced data. Model selection in the notebook is driven by F1 and AUC accordingly.

**Stack.** scikit-learn · TensorFlow/Keras · pandas · SciKeras

[→ Notebook](<Diabetes_Prediction_(Classification)_Using_Machine_Learning_and_Deep_Learning_Models.ipynb>)

---

## 4. PowderDraw — Autonomous Painting Robot

*Robotics · Sensor fusion · Navigation*

A modular ground robot that reproduces large-scale designs on open terrain by dispensing
coloured powder along a planned path. GPS alone is nowhere near precise enough for the job, so
the interesting part is the navigation stack.

**Approach.** Built on ArduPilot with a Pixhawk flight controller and a Raspberry Pi companion,
fusing GPS, LIDAR, IMU and optical flow through an external Kalman filter to hold position
accurately enough for the drawing to come out clean, with path planning and dispensing control
layered on top.

**Stack.** ArduPilot · Pixhawk · Raspberry Pi · Kalman filtering · Optical flow · LIDAR/IMU/GPS

[![Watch the demo](https://img.youtube.com/vi/O9t15PjKslc/0.jpg)](https://www.youtube.com/watch?v=O9t15PjKslc)

---

## Contact

[GitHub](https://github.com/sagiv-bar) · [LinkedIn](https://www.linkedin.com/in/sagiv-bar)
