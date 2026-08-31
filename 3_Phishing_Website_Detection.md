# Case Study 3: Phishing Website Detection

**Problem:** Fake websites trick people into entering passwords or bank details by imitating real sites (e.g. a fake bank login page).

**Question it answers:** *Is this website real or a phishing trap?*

```text
Website URL / Page
     ↓
Extract Features
 (URL length, use of "https", domain age,
  presence of login forms, suspicious symbols)
     ↓
Machine Learning Classifier
     ↓
Legitimate ✅   or   Phishing ❌
```

**Technique:** Features are extracted from the URL and page content (length of the address, whether it uses HTTPS, how old the domain is, presence of login forms, unusual characters) and fed into classifiers such as Random Forest, Logistic Regression, or Neural Networks.

**Summary:** Looks at small warning signs in a website's address and structure to catch fake sites before a user is tricked into entering personal information.
