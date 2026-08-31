# Phishing Website Detection — Detailed Explanation

## 1. What is the problem?

Phishing websites are fake pages designed to look like real ones (a bank login, a shopping site, an email provider) in order to trick people into entering sensitive information like passwords, card numbers, or personal details. Once entered, that data goes straight to the attacker.

The challenge: phishing pages are built to look nearly identical to the real thing, so most users can't tell the difference just by looking.

**Question it answers:** *Is this website legitimate, or is it a phishing trap?*

## 2. What data does it use?

Instead of relying on a human to "notice something's off," the system extracts measurable features from the URL and the page itself, such as:

- **URL structure** — unusually long URLs, extra subdomains, presence of suspicious symbols (`@`, multiple hyphens, IP addresses instead of domain names)
- **Security indicators** — whether the site uses HTTPS and has a valid certificate
- **Domain information** — how old the domain is (phishing domains are often newly registered)
- **Page content** — presence of login/password forms, hidden form fields, mismatched branding

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

## 3. Machine learning approach

These extracted features are turned into a numeric profile for each website, which is then fed into a classifier such as:

- **Random Forest** — combining multiple decision trees
- **Logistic Regression** — a simpler, interpretable baseline model
- **Neural Networks** — for capturing more complex, non-linear patterns among the features

## 4. Why it works

Phishing sites are copies, not originals — copying the *look* of a real site is easy, but the underlying technical fingerprint (a suspicious URL, a brand-new domain, missing security certificates) is much harder to fake convincingly. That fingerprint is exactly what this project targets.

## 5. Full flow

```text
User Visits / Submits a URL
      ↓
Extract URL & Page Features
      ↓
Machine Learning Classifier
      ↓
 ┌──────────────┐
 ↓              ↓
LEGITIMATE    PHISHING
 ✅              ❌
```

## 6. Why this matters

Phishing remains one of the most common ways attackers steal credentials, since it targets human trust rather than a technical vulnerability. A browser extension or email filter built on this kind of model can warn users before they ever enter sensitive information.

## 7. One-line summary

> This project analyzes small technical warning signs in a website's URL and content to automatically flag phishing pages before a user gets tricked into entering personal information.
