# IoT Botnet Detection — Extended Project Content

## 1. Project Overview

**Title:** IoT Botnet Detection Using Anomaly Detection

**Objective:** Build a system that monitors network traffic from IoT devices and detects when a device has likely been hijacked and turned into part of a botnet — including detecting attack patterns the system has never explicitly seen before.

**Problem type:** Primarily anomaly detection (unsupervised or semi-supervised), sometimes combined with supervised classification if labeled attack data is available.

---

## 2. Dataset

**Recommended dataset:** N-BaIoT dataset (UCI Machine Learning Repository).

- Real network traffic captured from 9 commercial IoT devices (e.g. doorbells, cameras, baby monitors)
- Contains both **benign (normal)** traffic and traffic from **real botnet attacks** — specifically Mirai and BASHLITE/Gafgyt malware
- Each device has its own set of traffic statistics, since "normal" behavior differs by device type
- Provided as pre-extracted statistical features (no need to process raw packet captures from scratch)

**Why this dataset is a good fit:**
- Based on real malware (Mirai), not simulated data — high real-world credibility
- Naturally separates data per device, letting you demonstrate the "learn normal per device" concept clearly
- Well-cited in academic literature, so there are strong benchmarks to compare against

---

## 3. System Architecture

```text
┌───────────────────────┐
│  IoT Devices (Cameras,   │
│  Plugs, Doorbells, etc.)  │
└───────────┬───────────┘
            ↓
┌───────────────────────┐
│  Network Traffic Capture  │  (per-device statistics:
│                            │   packet size, rate, direction)
└───────────┬───────────┘
            ↓
┌───────────────────────┐
│  Feature Extraction       │  (rolling statistical windows
│                            │   per device)
└───────────┬───────────┘
            ↓
┌───────────────────────┐
│  Anomaly Detection Model  │  (Autoencoder / Isolation Forest)
└───────────┬───────────┘
            ↓
     Reconstruction Error /
        Anomaly Score
            ↓
      Above Threshold?
       ↙            ↘
     Yes              No
      ↓                ↓
  Flag as           Mark as
  Compromised       Normal
```

---

## 4. Step-by-Step Pipeline

### Step 1 — Data Preprocessing
- Normalize/scale the traffic statistics (packet counts, sizes, timing intervals), since features can have very different ranges
- Keep data **separated by device**, since "normal" behavior for a smart plug is very different from "normal" behavior for a security camera

### Step 2 — Model Choice: Anomaly Detection

**Option A: Autoencoder (Neural Network)**
- Train the autoencoder **only on benign/normal traffic**
- It learns to compress and then reconstruct normal traffic patterns accurately
- When fed abnormal (attack) traffic, it struggles to reconstruct it well → high **reconstruction error** → flagged as anomalous

```text
Normal Traffic → Encode → Compress → Decode → Reconstructed Traffic
                                                  (low error = normal)

Attack Traffic → Encode → Compress → Decode → Reconstructed Traffic
                                                  (high error = anomaly)
```

**Option B: Isolation Forest**
- Randomly partitions the data; anomalies (which are "different" from the bulk of the data) get isolated in fewer partitioning steps than normal points
- Simpler and faster to train than a neural network, good for a baseline comparison

**Option C: Statistical Thresholding**
- Simplest baseline: compute mean/standard deviation of key features per device, flag anything beyond a set number of standard deviations

### Step 3 — Evaluation
Since this is anomaly detection, evaluation still needs labeled test data (the N-BaIoT dataset does include attack labels for testing purposes, even though training used only normal data):
- **Precision / Recall / F1-score** on the held-out attack traffic
- **ROC-AUC** for how well the anomaly score separates normal vs attack traffic
- Per-device breakdown — some devices may be easier or harder to protect than others

### Step 4 — Threshold Selection
Like fraud detection, the anomaly score is continuous, not binary. The cutoff for "this is now considered infected" needs tuning — based on how aggressive you want detection to be.

---

## 5. Suggested Tech Stack

- **Language:** Python
- **Libraries:** pandas, scikit-learn (Isolation Forest), TensorFlow/Keras or PyTorch (for the autoencoder), matplotlib/seaborn for visualizing traffic patterns
- **Optional deployment:** a simple dashboard showing live per-device anomaly scores

---

## 6. Common Challenges & How to Handle Them

| Challenge | Solution |
|---|---|
| "Normal" varies a lot between devices | Train a separate model (or profile) per device type |
| No attack examples during training | Use unsupervised anomaly detection (autoencoder / Isolation Forest) rather than a standard classifier |
| Too many false alarms from natural traffic variation | Use rolling time windows and smooth anomaly scores rather than reacting to single spikes |
| New, unseen attack types | This is actually a strength of anomaly detection — it doesn't need to have seen the exact attack before |

---

## 7. Possible Extensions (for a stronger project)

- Compare **Autoencoder vs Isolation Forest vs simple statistical thresholding** and show which performs best
- Visualize a device's "normal traffic envelope" vs a flagged anomalous spike, as a time-series chart
- Simulate a small **testbed** with mock device traffic to demonstrate real-time flagging
- Discuss mitigation steps once a device is flagged (e.g. isolate device from network, alert the owner)

---

## 8. Presentation Talking Points

1. Why IoT security matters (weak default security, huge and growing number of connected devices)
2. Real-world case: the Mirai botnet and its large-scale impact
3. Why this needs anomaly detection instead of standard classification (attacks constantly evolve)
4. How "normal" is learned per device
5. Model comparison and results (Precision/Recall/F1, ROC-AUC)
6. Why this approach can catch **future, unseen** attacks — not just known ones
