# Case Study 5: Credit Card Fraud Detection

**Problem:** Millions of card transactions happen every day. A small number are fraudulent (stolen card, unusual purchase), and catching them quickly prevents financial loss.

**Question it answers:** *Is this transaction genuine or fraudulent?*

```text
Transaction Data
 (amount, location, time, merchant type)
     ↓
Feature Analysis
     ↓
Machine Learning Model
 (Random Forest / XGBoost / Neural Network)
     ↓
Genuine ✅   or   Fraudulent ❌
```

**Technique:** Classification models are trained on historical transactions labeled genuine or fraudulent. A key challenge is that fraud cases are rare compared to genuine ones, so the model must be carefully trained to still catch them.

**Summary:** Scores each transaction in real time and flags the ones that look statistically unusual compared to a customer's normal spending pattern.
