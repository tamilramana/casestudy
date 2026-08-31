# Case Study 1: Cloud Intrusion Detection

**Problem:** A cloud server receives thousands of requests. Some are normal users, some are hackers. Manually checking each one is impossible.

**Question it answers:** *Is this network activity normal or an attack?*

```text
Network Data
     ↓
Clean & Select Important Data
     ↓
Random Forest (Machine Learning)
     ↓
Normal ✅   or   Attack ❌
```

**Technique:** Random Forest — many decision trees vote, majority wins.

```text
Tree 1 → Attack
Tree 2 → Attack
Tree 3 → Normal
Tree 4 → Attack
Tree 5 → Attack
        ↓
Majority Vote → ATTACK ❌
```

**Feature Engineering:** The model can distinguish normal from abnormal traffic using only a small number of selected features (e.g. amount of data sent and received), which keeps the system fast and efficient.

**Summary:** Uses machine learning to classify cloud network traffic as safe or malicious, using only a few key features instead of checking every request manually.
