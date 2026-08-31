# Case Study 2: Ransomware Detection

**Problem:** A downloaded file (e.g. `game.exe`) might secretly be ransomware that locks your files and demands payment to unlock them.

**Question it answers:** *Is this file safe or ransomware?*

```text
Suspicious File
      ├── Static Analysis   (inspect the file without running it)
      └── Dynamic Analysis  (run it safely in a sandbox, watch its behavior)
                ↓
      Behavior Data (DLLs, function calls, assembly behavior)
                ↓
      Machine Learning Classifier
                ↓
        Safe ✅   or   Ransomware ❌
```

**Technique:**
- **Static Analysis** — look at the file's structure and code without executing it.
- **Dynamic Analysis** — run the file inside an isolated sandbox (e.g. Cuckoo Sandbox) and observe what it actually does (opening files, changing contents, suspicious operations).
- **Classification** — the collected behavior is fed into machine learning models: SVM, Random Forest, J48, and AdaBoost.

**Result:** The best-performing model reported an accuracy of **99.54%**.

**Summary:** Combines "look without opening" and "run in a safe room" checks, then uses machine learning to decide whether a file is safe or ransomware.
