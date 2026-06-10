# 📡 Week 10 — C2 Frameworks & Phishing Infrastructure

**Intern:** Ali Ahsan | **Roll No:** CSI-B1-427
**Program:** Cyberstar Cybersecurity Red Teaming Internship
**Instructor:** Umar Niaz
**Date:** 13 May 2026
**Environment:** Kali Linux + Windows VM (Host-Only Network)

---

## 📌 Overview

This week covered modern attacker infrastructure — deploying a Command & Control framework, weaponizing documents for payload delivery, building a phishing campaign platform, and analyzing email authentication protocols used to detect and prevent spoofing.

---

## 🧪 Tasks Covered

### Task 01 — Sliver C2 Framework Deployment

**Sliver** is an open-source C2 framework supporting HTTP, HTTPS, DNS, and mTLS communications.

**Installation & Setup:**
```bash
# Fix permissions and create symlink
chmod +x sliver-server
ln -s /path/to/sliver-server /usr/local/bin/sliver-server

# Reload daemon after fixing service file
sudo systemctl daemon-reload
sudo systemctl start sliver
```

**HTTP Listener Configuration:**
```bash
http -L 8080   # Listener on port 8080
jobs            # Verify listener running
```

**Capabilities demonstrated:**
- Beacon communication
- Session handling
- Remote command execution
- Multi-session management
- Encrypted HTTP communications

### Task 02 — Payload Weaponization Techniques

**VBA Macro (Word .docm):**
- Created macro-enabled Word document with `AutoOpen()` function
- Triggers automatically on document open — no user interaction beyond enabling macros

**LNK Shortcut Execution:**
- Windows `.LNK` shortcut files created to execute commands while appearing harmless
- Both GUI and command-line generation methods demonstrated

**HTML Smuggling:**
- Payload encoded directly inside HTML/JavaScript
- Reconstructed client-side in the browser — bypasses email security filters

### Task 03 — GoPhish Phishing Infrastructure

**GoPhish** is an open-source phishing simulation framework.

```bash
# Launch GoPhish
./gophish
# Access dashboard: https://127.0.0.1:3333
```

**Campaign Components Built:**
- Email template using urgency + authority social engineering principles
- Cloned authentication landing page (credential collection portal)
- Target group configuration
- SMTP sending profile

**Dashboard metrics:** Email delivery status, open rates, click tracking, user submissions.

> Note: SMTP delivery errors occurred due to no active MTA in the isolated lab — full phishing workflow was demonstrated conceptually.

### Task 04 — Email Security & SMTP Analysis

| Protocol | Purpose |
|----------|---------|
| **SPF** | Validates sending mail server is authorized for the domain |
| **DKIM** | Cryptographic signature ensures message integrity |
| **DMARC** | Combines SPF + DKIM → enforces reject/quarantine policies |

**Typosquatting Examples:**
- `goggle.com`, `googlle.com`, `go0gle.com`

**Homograph Attacks:** Replacing Latin letters with visually identical Cyrillic/Greek Unicode characters — malicious domains appear identical to legitimate ones.

---

## 🛡️ Security Recommendations

- Enforce SPF, DKIM, and DMARC on all organizational domains
- Disable Office macros via Group Policy
- Conduct regular phishing awareness training
- Monitor for typosquatted domain registrations
- Deploy secure email gateways and endpoint protection
- Implement Multi-Factor Authentication

---

## 🛠️ Tools Used

`Sliver C2` · `GoPhish` · `Swaks` · `msfvenom` · `Microsoft Word (VBA)`

---

## ⚠️ Disclaimer

> Performed in an **authorized, isolated lab environment**. Phishing techniques demonstrated for defensive awareness only. Never use against real targets without explicit written authorization.
