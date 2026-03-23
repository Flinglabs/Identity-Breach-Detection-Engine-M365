# 🔐 Identity Detection Engine (Demo)

## Overview

This project showcases a lightweight **identity-focused detection engine** designed to complement platforms like Microsoft Identity Protection.

Rather than relying purely on static rules, this engine focuses on **behavioural baselining and signal correlation** to identify suspicious authentication activity.

---

## 🚨 Key Detection Capabilities

The engine is designed to identify high-risk identity behaviours, including:

* 🌍 **New Country Login**
* 🌐 **New ASN (Network) Activity**
* 💻 **New Device Fingerprint**
* 🔁 **Session Reuse (Same session, new device)**
* ⏱️ **Unusual Login Time (Behavioural deviation)**
* 🔑 **MFA Changes / Resets**
* 📬 **Suspicious Mailbox Rule Creation**
* ⚠️ **Correlated Signals (Multiple anomalies in short timeframe)**

---

## 🧠 Detection Approach

This engine uses a **rolling baseline model** per user:

* Tracks historical behaviour over time (e.g. country, ASN, device, login hour)
* Flags deviations once sufficient baseline data is established
* Avoids alerting too early ("learn first, alert later")

### Key Principles:

* Behaviour over signatures
* Correlation over single events
* Context-aware alerting

---

## 🔍 Why This Matters

## 🧪 Example Attack Scenario

This dataset represents a potential account compromise:

1. User signs in from a known location (baseline behaviour)
2. A new login occurs from a different country, ASN, and device
3. The same session is reused across a device change
4. MFA settings are modified
5. A mailbox rule is created (possible data exfiltration)

Individually, these signals may not indicate compromise.  
When correlated, they form a high-confidence attack chain.

Traditional identity detections often trigger on single signals (e.g. new country or impossible travel), which can lead to high false positive rates.

This engine focuses on:
- Correlating multiple weak signals into high-confidence alerts
- Tracking behavioural baselines per user
- Prioritising context over isolated anomalies

This allows for more meaningful alerts and reduced noise.

## 📊 Example Output

### Alerts (JSON)

```json
{
  "user": "alice@example.com",
  "risk_level": "high",
  "signals": [
    "new country",
    "new ASN",
    "new device fingerprint",
    "session reuse"
  ],
  "timestamp": "2026-03-11T19:42:15Z"
}
```

### Timeline (Human-readable)

```
2026-03-11T19:20:10Z - Normal login (baseline learning)
2026-03-11T19:42:15Z - Suspicious login: new country + new ASN + new device
2026-03-11T19:42:15Z - Possible session reuse detected
```

---

## 🎯 Purpose of This Repository

This is a **demo repository** intended to:

* Showcase detection logic and output format
* Demonstrate how behavioural analytics can enhance identity security
* Provide sample data for feedback and testing

> ⚠️ The core detection engine logic is not included in this repository.

---

## 🤝 Collaboration & Feedback

I’m actively looking for:

* 📁 Sanitised authentication logs for testing
* 🧪 Feedback on detection logic and alert quality
* 💡 Ideas for additional identity-based detections

If you're interested in testing or collaborating, feel free to reach out.

---

## 🛠️ Future Improvements

Planned enhancements include:

- Independent impossible travel detection (distance + time correlation, with VPN / proxy suppression)
- Detection of successful password spraying across multiple users
- Enhanced session analysis for token theft / replay scenarios
- Risk scoring model based on correlated signals and behavioural context
- API integration and SaaS portal for multi-tenant alerting and visualisation

---

## 📌 Positioning

This engine is designed to **complement**, not replace, existing security tools.

It aims to:

* Fill gaps in behavioural detection
* Provide clearer correlation of signals
* Reduce noise through smarter baselining

---

## 📬 Contact

For access to the full engine or collaboration opportunities, please open an issue or get in touch.

---

## ⭐ If You Find This Useful

Please consider starring the repo — it helps visibility and supports development.
