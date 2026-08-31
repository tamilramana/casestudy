# Cloud Intrusion Detection — Detailed Explanation

## 1. What is the problem?

A company or organization stores its data and runs its applications on a cloud server (like AWS, Azure, or Google Cloud). That server constantly receives incoming requests — some from legitimate users (students, customers, employees), and some potentially from hackers trying to break in, steal data, or disrupt the service.

The scale makes this hard: a busy cloud server can receive thousands to millions of requests per day. Checking each one manually is simply not possible.

**Question it answers:** *Is this network activity normal, or is it an attack?*

```text
Students / Users ──────► Cloud Server
                            ▲
                            │
                         Hacker

Normal traffic  → ✅ Safe
Hacker traffic  → ❌ Attack
```

## 2. What data does it use?

The system captures details of network traffic hitting the server — things like:
- Volume of data sent and received
- Connection duration
- Number of requests in a time window
- Protocol/port information

## 3. High-level flow

```text
Network Data
     ↓
Data Cleaning
     ↓
Feature Selection (important attributes only)
     ↓
Machine Learning Model (Random Forest)
     ↓
Classification: Normal or Attack
```

## 4. Core technique: Random Forest

Random Forest is an ensemble method — instead of relying on a single decision-making model, it combines the opinions of many individual decision trees and goes with the majority vote. This makes it more robust than a single tree, since one tree's mistake gets outvoted by the others.

```text
Tree 1 → Attack
Tree 2 → Attack
Tree 3 → Normal
Tree 4 → Attack
Tree 5 → Attack
        ↓
Majority Vote → ATTACK ❌
```

## 5. Feature engineering

A key design choice in this project is reducing the number of features the model needs to look at. Research on this topic has shown that traffic can be classified accurately using just a couple of well-chosen features (such as bytes sent and bytes received), which keeps the system fast enough to run in real time on high-volume traffic.

## 6. Why this matters

Cloud servers are attractive targets because a successful breach can expose large amounts of centralized data. An automated, always-on detection layer catches attacks that would be impossible to spot by manually reviewing logs.

## 7. One-line summary

> This project uses machine learning (Random Forest) to automatically classify incoming cloud network traffic as normal or malicious, using a small, efficient set of traffic features.
