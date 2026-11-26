<div align="center">

# 🛡️ Cybersecurity CTF Writeups
### Hands-on notes on how systems break, and how to fix them

![OverTheWire](https://img.shields.io/badge/OverTheWire-Natas%20%7C%20Bandit-black?style=for-the-badge)
![picoCTF](https://img.shields.io/badge/picoCTF-Writeups-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Web%20%26%20Linux%20Security-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Actively%20Learning-orange?style=for-the-badge)

*I write up the **why**, not just the answer, and I keep my mistakes in.*

</div>

> ⚠️ **Ethics:** Everything here was done in legal, purpose-built training environments (OverTheWire, picoCTF). Flags and passwords are redacted. Never test on systems you don't own or have written permission to test.

---

## 🧭 How I approach every challenge

```mermaid
flowchart LR
    A[Observe] --> B[Find the trust decision]
    B --> C[Test one assumption]
    C --> D[Name the vulnerability class]
    D --> E[Map to a real-world CVE / ATT&CK technique]
    E --> F[Write the fix]
```

## 📊 Progress

| Platform | Track | Status | Writeups |
|---|---|:-:|---|
| OverTheWire | **Natas 0–9** (web) | 🟡 In progress | [Natas 1–9 · Thinking like an attacker](overthewire/natas/README.md) |
| OverTheWire | **Bandit** (Linux) | ✅ Done | [Index](overthewire/bandit/README.md) |
| picoCTF | General Skills / Crypto / RE | 🟡 In progress | [Index](picoCTF/README.md) |
| C & systems | I/O, unsafe functions | 🟡 Notes | [stdio & unsafe functions](c-and-systems/stdio-buffering-and-unsafe-functions.md) |

## 🗺️ Skills map

```mermaid
mindmap
  root((Security<br/>learning))
    Web
      Info disclosure
      Auth logic flaws
      Local File Inclusion
      Command injection
    Linux
      SUID privilege escalation
      Cron abuse
      Restricted shell breakout
    Reverse engineering
      Static analysis
      License-key logic
    Fundamentals
      Encodings
      Pipes and grep
      C I/O and memory safety
```

## 📂 Repo layout

```text
.
├── overthewire/
│   ├── natas/      web vulnerabilities, levels 1–9
│   └── bandit/     Linux, privilege escalation, shell breakout
├── picoCTF/
│   ├── general-skills/
│   ├── cryptography/
│   └── reverse-engineering/
└── c-and-systems/
```

## 🚧 Roadmap

- [ ] Natas 10+ (filter bypass, SQL injection, session logic)
- [ ] Finish Bandit and add the remaining level notes
- [ ] PortSwigger Web Security Academy labs
- [ ] **Windows & Active Directory** (Kerberoasting, pass-the-hash, BloodHound-style attack paths). Bandit doesn't cover it, and most corporate environments are Windows domains
- [ ] Buffer overflow from first principles (stack layout, GDB, protections)
