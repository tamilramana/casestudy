# IoT Botnet Detection — Detailed Explanation

## 1. What is the problem?

"IoT" means Internet of Things — everyday smart devices connected to the internet: smart cameras, smart plugs, smart TVs, routers, doorbells. These devices are often weakly secured, making them easy targets. A hacker can secretly break into many of them at once and link them into a **botnet** — a network of hijacked devices controlled remotely, typically used to launch large-scale attacks such as flooding a website with traffic until it crashes (a DDoS attack).

**Question it answers:** *Are my smart devices behaving normally, or have they been secretly hijacked?*

## 2. Why this is hard to notice

A hijacked device usually keeps working normally from the owner's point of view — the smart camera still streams video, the smart plug still turns the lamp on. In the background, though, it may also be quietly sending attack traffic. There's no visible warning sign for the owner.

## 3. How the system detects it

Rather than scanning each individual device for viruses (many IoT devices don't support that at all), the system watches the **network traffic pattern** each device produces — how much data it sends, how often, and to which destinations.

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

## 4. Anomaly detection — the key technique

Unlike a standard classifier trained on labeled "attack" and "normal" examples, botnet detection typically leans on **anomaly detection**:

- The model is trained mostly on **normal behavior**.
- It builds a profile of what "normal" looks like for each device (e.g. a smart plug should only send small, infrequent signals — never thousands of requests per second).
- Any traffic that deviates significantly from that learned normal profile gets flagged — even if it's a brand-new attack type the model has never seen before.

## 5. Models/techniques used

- **Statistical thresholds** — flagging traffic that falls outside a device's normal statistical range
- **Autoencoders** (a type of neural network) — trained to reconstruct normal traffic; struggling to reconstruct new traffic signals it's abnormal
- **Clustering / Isolation Forest** — groups similar traffic together and isolates outliers that don't belong to any cluster

## 6. Full flow

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

## 7. Why this matters

This mirrors real-world incidents like the **Mirai botnet**, which infected huge numbers of IoT devices and was used to launch attacks that took down major websites. Detecting hijacked devices early — before they're weaponized — is critical as more homes and cities fill up with connected devices.

## 8. One-line summary

> This project monitors how each smart device normally communicates and raises an alert the moment a device starts behaving differently, catching hijacked devices even when the attack method is completely new.
