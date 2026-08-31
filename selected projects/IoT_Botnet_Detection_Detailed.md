# IoT Botnet Detection — Detailed Explanation

## 1. What is the problem?

"IoT" means **Internet of Things** — everyday smart devices connected to the internet: smart cameras, smart plugs, smart TVs, routers, doorbells, etc.

These devices are often weakly secured. Hackers can secretly break into many of them and combine them into a **botnet** — a network of hijacked devices that the hacker controls remotely, often used to launch large attacks (like flooding a website with traffic until it crashes).

**Question it answers:** *Are my smart devices behaving normally, or have they been secretly hijacked?*

## 2. Why is this hard to notice?

A hijacked device usually keeps working normally from the owner's point of view — the smart camera still shows video, the smart plug still turns the lamp on and off. But in the background, it may also be secretly sending attack traffic. The owner has no visual sign anything is wrong.

## 3. How does the system detect it?

Instead of checking each device individually for viruses (which is hard, since many IoT devices have very limited software), this system watches the **network traffic pattern** each device produces.

```text
IoT Device Network Traffic
     ↓
Monitor Traffic Patterns
 (packet size, request frequency,
  which devices talk to which,
  time-of-day patterns)
     ↓
Learn "Normal" Behavior per Device
     ↓
Compare New Traffic Against Normal Pattern
     ↓
Normal ✅   or   Infected / Botnet Activity ❌
```

## 4. Why is this technically different — Anomaly Detection

Unlike the fraud or ransomware examples (which learn "fraud vs genuine" or "safe vs ransomware" from labeled examples of both), botnet detection often uses **anomaly detection**:

- The model is mostly trained on **normal behavior only**.
- It learns what "normal" looks like for each device (e.g., a smart plug sends tiny, occasional signals; it should never suddenly start sending thousands of requests per second).
- Anything that doesn't match that learned "normal" pattern is flagged as suspicious — even attack types the model has never seen before.

This makes it powerful against **new, unknown types of attacks**, which is a real strength compared to detection systems that only recognize attacks they were specifically trained on.

## 5. What techniques/models are typically used?

- **Statistical thresholds** — flag traffic that is statistically far from the device's normal range.
- **Autoencoders (a type of neural network)** — the model tries to "reconstruct" normal traffic; if it struggles to reconstruct new traffic accurately, that traffic is probably abnormal.
- **Clustering / Isolation Forest** — groups similar traffic together and flags outliers that don't belong to any normal group.

## 6. Step-by-step flow

```text
Collect Traffic from Each IoT Device
              ↓
     Learn What "Normal" Looks Like
              ↓
      New Traffic Arrives
              ↓
   Compare to Learned Normal Pattern
              ↓
   Matches Normal → Device is Fine ✅
   Doesn't Match  → Possible Infection ❌
```

## 7. Real-world impact

This kind of system is what ISPs, smart-home security products, and enterprise IoT networks use to catch hijacked devices before they're used in a large-scale attack (like the real-world **Mirai botnet**, which infected IoT devices and was used to take down major websites).

## 8. One-line summary

> This project monitors how each smart device normally communicates, and raises an alert when a device starts behaving differently — catching hijacked devices even if the attack method has never been seen before.
