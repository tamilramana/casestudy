# Credit Card Fraud Detection — Detailed Explanation

## 1. What is the problem?

Every day, millions of card transactions happen — buying coffee, groceries, paying bills online. Out of these, a tiny fraction are **fraudulent** — someone using a stolen card number, or making an unusual purchase that doesn't match the cardholder's normal behavior.

The challenge: **fraud is rare**. In a typical dataset, maybe 0.1–0.2% of transactions are fraud. This makes it a hard problem because a lazy model could just say "everything is genuine" and still be 99.8% "correct" — while missing every actual fraud case.

**Question it answers:** *Is this transaction genuine, or is it fraud?*

## 2. What data does it use?

For each transaction, the system looks at details such as:

- Transaction **amount**
- **Location** of the purchase
- **Time** of day / day of week
- **Merchant type** (grocery store, online store, ATM withdrawal, etc.)
- How this compares to the cardholder's **usual spending pattern**

```text
New Transaction
     ↓
Extract Features (amount, location, time, merchant)
     ↓
Compare Against Cardholder's Normal Pattern
     ↓
Machine Learning Model
     ↓
Genuine ✅   or   Fraudulent ❌
```

## 3. Why is this technically different?

This is called an **imbalanced classification problem**. Because fraud cases are so rare, special techniques are needed:

- **Resampling** — creating more copies of the rare fraud examples (oversampling, e.g. SMOTE) or reducing the number of normal examples (undersampling) so the model doesn't ignore fraud.
- **Choosing the right metric** — instead of just "accuracy," the project should look at **Precision, Recall, and F1-score**, because accuracy alone is misleading when one class is so rare.
- **Threshold tuning** — deciding how "suspicious" a transaction needs to look before it gets flagged, balancing between catching fraud and not annoying genuine customers with false alarms.

## 4. Machine learning models used

- **Random Forest** — an ensemble of decision trees voting together.
- **XGBoost** — a more powerful, boosted tree-based model often used in fraud detection competitions.
- **Neural Networks** — can capture more complex, non-obvious spending patterns.

## 5. Full flow

```text
Historical Transactions (labeled genuine/fraud)
              ↓
      Train Machine Learning Model
              ↓
   New Transaction Comes In (real time)
              ↓
      Model Scores the Transaction
              ↓
   Score High (suspicious) → Flag for Review ❌
   Score Low (normal)      → Approve ✅
```

## 6. Why this matters

This is exactly the kind of system banks and payment apps (Visa, PayPal, etc.) run in real time, in the background, every time you swipe or tap your card — silently protecting both the bank and the customer from loss.

## 7. One-line summary

> This project builds a model that studies a person's normal spending pattern and flags transactions that don't fit that pattern, using special techniques to handle the fact that fraud is very rare compared to genuine purchases.
