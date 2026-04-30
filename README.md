# 🚨 SOS Alert Detection System — 4-Layer Intelligence

> **"We never auto-block a single alert. Because this is not a spam filter. This is someone pressing a button because they believe they are going to die."**

Built at **Hackathon 2026** in under 3 hours.

---

## 🧠 What Is This?

Every SOS app today has the same critical flaw — when someone presses the button, the system is completely blind. It doesn't know if the user sent ten false alarms this week. It doesn't know they just traveled 1,300km in five minutes. It doesn't know their message says "haha testing" while they selected Medical Emergency.

**We built the intelligence layer that sits between the button press and the emergency response.**

Our system runs **4 independent layers of analysis** on every alert, assigns a dynamic **Credibility Passport** to every user, and routes alerts through a **smart escalation engine** — all without ever auto-blocking a single alert.

---

## 🏗️ The Four Layers

### Layer 1 — Behavioral Rules Engine
Rule-based scoring that runs in O(1) time. Checks:
- Alert frequency (> 3/hour → suspicious)
- Account age (< 7 days → new account penalty)
- Verification status
- Message length and vagueness
- Test keywords (`lol`, `testing`, `fake`, `dummy`)
- Location repetition patterns
- User trust score influence

### Layer 2 — Gemini AI Semantic Analysis
Calls **Gemini 2.0 Flash** via REST API. Asks three questions:
- What is the confidence this is a real emergency? (0–100)
- Does the message content match the selected alert type?
- What is the one-line reason for this assessment?

Designed with graceful degradation — if Gemini is unavailable, the system continues with Layers 1, 3, and 4.

### Layer 3 — Geospatial + Network Intelligence
Uses the **Haversine formula** to calculate great-circle distance between GPS coordinates and derive travel speed between alerts.

```
speed > 900 km/h → Physically impossible → +60 risk score
speed > 200 km/h → Suspiciously fast   → +25 risk score
```

Also performs **cross-user corroboration** — if 2+ independent users report from the same location within 5 minutes, the alert gains credibility and the suspicion score decreases.

### Layer 4 — Multi-Signal Verification
Validates physical evidence beyond the button press:
- Motion detected (accelerometer)
- Audio spike (scream / loud noise)
- Sudden stop in movement
- Network instability

3+ signals confirmed → strong physical evidence → score reduction

---

## 🛂 SOS Credibility Passport

The core innovation. Every user has a **dynamic trust identity** that evolves in real time based on behavior.

```json
{
  "user_id": "U101",
  "credibility_level": "LOW",
  "trust_score": 25,
  "risk_score": 75,
  "user_type": "Potential Misuser",
  "history_pattern": "Frequent repeated alerts",
  "last_action": "Temporarily blocked",
  "system_confidence": "HIGH"
}
```

**Trust Score dynamics:**
| Event | Score Change |
|---|---|
| Genuine alert verified | +10 |
| Suspicious alert flagged | -15 |
| Fake alert detected | -30 |
| Impossible travel detected | -50 |
| Human reviewer approves | +15 |
| Human reviewer rejects | -25 |

**Credibility Levels:**
- 75–100 → HIGH → Trusted Responder
- 50–74 → MEDIUM → Standard User
- 25–49 → LOW → At-Risk User
- 0–24 → CRITICAL → Potential Misuser

---

## 🚦 Smart Escalation Engine

Not all alerts go to the same place. The system routes based on confidence:

| Risk Score | Signals | Action |
|---|---|---|
| < 30 | 3+ signals | 🚨 Dispatch emergency services immediately |
| < 30 | < 3 signals | 📡 Forward to control center |
| 30–54 | Any | 👥 Notify nearby community users |
| 55+ | Any | 🔍 Hold for human reviewer |

---

## 🛡️ Human-In-The-Loop (Core Design Principle)

**We never auto-block a single alert.**

Every suspicious or high-risk alert enters a **Reviewer Queue** where a human operator sees:
- Full flag breakdown with layer attribution
- Gemini AI reasoning
- User's Credibility Passport
- Approve or Reject decision

Reviewer decisions feed back into the user's trust score — creating a **continuous learning loop**.

---

## ⚔️ Adversarial Self-Attack Testing

We attack our own system to find vulnerabilities. Four attack strategies:

1. **Polished fake** — well-written, verified-looking, designed to fool AI
2. **Geo-velocity attack** — impossible travel speed between cities
3. **Alert flood** — mass spam from one user
4. **Trusted user gone rogue** — high trust score abuser

This demonstrates production-level security thinking.

---

## 📊 Scoring Algorithm

```
total_score = layer1_score + layer2_score + layer3_score + layer4_score
total_score = clamp(total_score, 0, 100)

score < 30  → REAL       → Escalation engine
score 30-54 → SUSPICIOUS → Reviewer queue
score >= 55 → FAKE       → Reviewer queue
```

**Confidence = 100 - total_score**

---

## 🚀 How To Run

No installation. No dependencies. No terminal.

1. Download `sos_final_system.html`
2. Double-click to open in any browser (Chrome recommended)
3. Optionally paste a free Gemini API key from [aistudio.google.com](https://aistudio.google.com) for live AI analysis
4. Submit alerts and watch the system work

That's it.

---

## 🔑 Getting a Free Gemini API Key

1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Sign in with any Google account
3. Click **Get API Key** → **Create API key**
4. Copy and paste into the yellow bar at the top of the app
5. Click **Save Key** — AI layer is now active

**No payment required.**

---

## 🆚 How We're Different From Existing SOS Systems

| Feature | Existing SOS Apps | Our System |
|---|---|---|
| Fake detection | ❌ None | ✅ 4-layer intelligence |
| AI analysis | ❌ None | ✅ Gemini semantic analysis |
| User trust history | ❌ None | ✅ Credibility Passport |
| Geospatial velocity | ❌ Never checked | ✅ Haversine formula |
| Cross-user corroboration | ❌ None | ✅ Network-level analysis |
| Explainability | ❌ Black box | ✅ Every flag explained |
| Auto-blocks alerts | ⚠️ Some do | ✅ Never — human always in loop |
| Escalation tiers | ❌ One size fits all | ✅ 3 tiers based on confidence |
| Self-attack testing | ❌ None | ✅ Adversarial test suite |
| Dependencies | Various | ✅ Zero — pure HTML/JS |

---

## 💻 Technical Stack

| Component | Technology |
|---|---|
| Frontend | Pure HTML5 + CSS3 + Vanilla JavaScript |
| AI Layer | Gemini 2.0 Flash REST API |
| Geospatial | Haversine formula (custom implementation) |
| Architecture | Client-side, zero backend required |
| Dependencies | None |
| Deployment | Any browser, any device |

---

## 📁 Project Structure

```
sos_final_system.html     ← Entire application (single file)
README.md                 ← This file
```

---

## 🧩 Key Algorithms

**Haversine Formula** — calculates real-world distance between GPS coordinates accounting for Earth's curvature. Used for geospatial velocity detection.

**Weighted Additive Scoring** — four independent layers each contribute a score that aggregates into a final risk value.

**Dynamic Trust Decay** — asymmetric trust model where penalties are larger than rewards, making trust slow to earn and fast to lose.

**Corroboration Boost** — cross-user validation that increases confidence when multiple independent users report from the same location.

---

## 👥 Team

Built at Hackathon 2026

---

## 📄 License

MIT License — free to use, modify, and deploy.

---

*"This is not a spam filter. This is someone pressing a button because they believe they are going to die. We built a system that treats it that way."*
