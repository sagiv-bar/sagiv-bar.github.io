# Sagiv Bar

Algorithm and machine learning engineer with an M.Sc in Intelligent Systems and AI. I work on
LLMs and controllable text generation, deep learning, and statistical estimation on noisy
real-world measurements.

Site: https://sagiv-bar.github.io
LinkedIn: https://www.linkedin.com/in/sagiv-bar

---

## Research

### [LLM-guided headline rewriting for clickability enhancement without clickbait](https://arxiv.org/abs/2603.22459)

arXiv:2603.22459 | cs.CL / cs.AI | March 2026
Yehudit Aperstein, Linoy Halifa, **Sagiv Bar**, Alexander Apartsin

Optimizing a news headline for engagement tends to slide into clickbait. We treat clickbait as
the extreme end of amplifying legitimate engagement cues, which lets us frame headline
rewriting as a controllable generation problem: strengthen specific engagement attributes under
explicit constraints on semantic faithfulness and proportional emphasis.

The framework steers an LLM at inference time using the FUDGE paradigm (Future Discriminators
for Generation). Two auxiliary guide models do the steering. A clickbait scorer pushes back
against stylistic over-amplification, and an engagement-attribute model pulls toward the
target. Both guides train on neutral headlines from a curated news corpus, with clickbait
counterparts generated synthetically under controlled activation of predefined tactics.
Adjusting the guidance weights moves the output along a continuum from faithful paraphrase to
more engaging phrasing that still holds up editorially.

[Read the paper](https://arxiv.org/abs/2603.22459) | [PDF](https://arxiv.org/pdf/2603.22459)

---

## 1. Tactic-Level Clickbait Attribution

LLMs, NLP, explainability. Joint work with Linoy Halifa.

Most clickbait systems return a yes or a no, which does not tell an editor what to change.
This two-stage framework also names the rhetorical tactic in play: curiosity gap, unfinished
narrative, ambiguous reference, provocative question, and six others.

Stage one is a fine-tuned BERT binary classifier. Stage two is a multi-label head that
attributes up to three tactics per headline. Training data combines a real news corpus with
clickbait generated through controlled GPT-4o prompting, and the train/test split is taken
**before** generation, so no synthetic sibling of a test headline can leak into training. The
fine-tuned models are then benchmarked against GPT-4o and Gemini 2.5 in zero-shot and few-shot
settings on the same held-out set, scored with macro and micro F1, exact-match ratio, and
per-class F1.

Stack: PyTorch, HuggingFace Transformers, BERT, GPT-4o, Gemini 2.5

[Code](https://github.com/LinoyHalifa/NLP_Project)

---

## 2. Blind Noise Estimation and BM3D Denoising

Image processing, statistical estimation.

BM3D is one of the strongest denoisers available, but it has to be told the noise standard
deviation, which you do not know on a real image. This project estimates sigma from the noisy
image itself and feeds the result to BM3D.

The image is split into 6x6 patches and each patch is scored by a gradient texture index
(Sobel). Textured patches are dropped, and sigma is estimated from the flat ones through a
chi-square confidence bound on the pooled variance. The threshold separating flat from textured
is re-derived from the current estimate, and the process repeats until the relative change in
variance falls below 1e-3. Output quality is measured against the clean reference with MSE,
SNR, PSNR, SSIM and Pearson correlation.

Stack: Python, OpenCV, SciPy, BM3D, scikit-image

[Notebook](Gaussian_Noise_Estimation_and_Denoising_Using_BM3D_Algorithm.ipynb)

---

## 3. BLE Distance Estimation with Neural Networks

RF, indoor positioning, deep learning.

Beacon-based indoor positioning needs a mapping from BLE signal strength (RSSI) to distance.
Analytic path-loss models assume free-space propagation and degrade badly indoors, where
multipath and absorption dominate. Here the mapping is learned from measurements.

Three beacons sit at known positions in a 2.74 x 4.38 m area. Ground-truth distances come from
the recorded receiver positions, normalized by the room diagonal, and are regressed from the
RSSI vector with fully connected networks. Four depths, from 128-64 up to 128-64-32-16-8, were
swept against three activations (sigmoid, ReLU, tanh), with held-out R2 recorded every 10
epochs up to 250. Plotting R2 across training shows how fast each architecture converges and
whether it stays stable there.

Stack: TensorFlow, Keras, scikit-learn, NumPy

[Notebook](Estimation_of_BLE_Signal_Distance_Using_Artificial_Neural_Networks.ipynb)

---

## 4. Classical ML vs. Deep Learning on Imbalanced Health Data

Applied ML, model selection.

About 15,000 records with a strong class imbalance, used to compare a tuned Random Forest
against a tuned deep network end to end: EDA, correlation and outlier analysis, feature
engineering, scaling, then grid search over both model families and over class-balancing
strategies.

The best model reaches **97.1% accuracy**, with **F1 of 0.80** and **ROC AUC of 0.967**. A
second configuration lands at 95.3% accuracy but only 0.61 F1. On data this imbalanced accuracy
hides most of what matters, so model selection in the notebook runs on F1 and AUC.

Stack: scikit-learn, TensorFlow, Keras, pandas, SciKeras

[Notebook](<Diabetes_Prediction_(Classification)_Using_Machine_Learning_and_Deep_Learning_Models.ipynb>)

---

## 5. PowderDraw: Autonomous Painting Robot

Robotics, sensor fusion, navigation.

A modular ground robot that reproduces large-scale designs on open terrain by dispensing
colored powder along a planned path. GPS on its own is not precise enough for the drawing to
come out clean, so most of the work sits in the navigation stack.

Built on ArduPilot with a Pixhawk flight controller and a Raspberry Pi companion. GPS, LIDAR,
IMU and optical flow are fused through an external Kalman filter to hold position, with path
planning and dispensing control layered on top.

Stack: ArduPilot, Pixhawk, Raspberry Pi, Kalman filtering, optical flow, LIDAR/IMU/GPS

[![Watch the demo](https://img.youtube.com/vi/O9t15PjKslc/0.jpg)](https://www.youtube.com/watch?v=O9t15PjKslc)

---

## Contact

[GitHub](https://github.com/sagiv-bar) | [LinkedIn](https://www.linkedin.com/in/sagiv-bar) | [arXiv](https://arxiv.org/abs/2603.22459)
