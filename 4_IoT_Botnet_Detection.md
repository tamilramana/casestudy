# Case Study 4: IoT Botnet Detection

**Problem:** Smart home devices (cameras, routers, smart plugs) can be secretly hijacked by hackers and combined into a "botnet" — an army of infected devices used to launch large-scale attacks.

**Question it answers:** *Are my smart devices behaving normally, or have they been hijacked?*

```text
IoT Device Network Traffic
     ↓
Monitor Traffic Patterns
 (packet size, request frequency,
  which devices talk to which)
     ↓
Machine Learning / Anomaly Detection
     ↓
Normal Behavior ✅   or   Infected Device ❌
```

**Technique:** Anomaly detection — the model first learns what "normal" device behavior looks like, then flags anything that deviates from that pattern.

**Summary:** Watches how smart devices communicate with each other and the internet, and raises an alarm if a device starts behaving like it's been taken over by an attacker.
