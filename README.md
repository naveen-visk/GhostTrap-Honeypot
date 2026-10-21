# 🛡️ GhostTrap – Active Cyber Deception & Smart Honeypot Sandbox

> **Hack The Circle (MAIT) Submission** | **Selected Track:** Track 3: Cybersecurity (Defensive Security Tools & Threat Detection)

---

## 📌 1. Problem Statement
Traditional Web Application Firewalls (WAFs) use passive blocking (`HTTP 403 Forbidden`) when they detect suspicious requests. This immediately alerts attackers, allowing them to rotate IPs, modify payloads, and probe again without leaving actionable forensic telemetry. Meanwhile, small teams, college portals, and open-source maintainers lack affordable Security Operations Center (SOC) tools to study incoming attack patterns on exposed `/admin` or `/login` endpoints.

## 💡 2. Proposed Solution
**GhostTrap** shifts defense from *passive blocking* to *active cyber deception*. Instead of rejecting an intruder attempting SQL Injection (SQLi), Cross-Site Scripting (XSS), or Brute-Force attacks, GhostTrap silently intercepts the payload and diverts the attacker into a realistic **Mirage Admin Environment (Honeypot)** populated with 100% synthetic data. 

While the intruder interacts with the decoy vault, GhostTrap captures their browser telemetry, classifies the attack vector, calculates a real-time Threat Score, and monitors **Canary File Traps** to alert defenders the moment data exfiltration is attempted.

---

## ✨ 3. Key Features
* **🎭 Mirage Admin Vault (Deception Layer):** Dynamically diverts malicious login attempts into a believable decoy database interface without alerting the attacker.
* **🔍 Heuristic Payload Classifier:** Real-time Regular Expression (Regex) inspection engine that detects and categorizes SQL Injection (`SQLi`), Cross-Site Scripting (`XSS`), Directory Traversal (`../`), and Dictionary Brute-Force attempts.
* **🧬 Zero-Friction Intruder Fingerprinting:** Captures client telemetry including User-Agent, Screen Resolution, Timezone, System Language, and session timestamps.
* **🚨 Canary Token Exfiltration Trap:** Embeds tracking identifiers inside decoy backup files (`prod_credentials_backup_2026.csv`) to immediately flag unauthorized file downloads.
* **📊 Live Defender SOC Dashboard:** Visualizes trapped intrusions, severity KPIs, and exports structured **Forensic JSON Incident Reports**.

---

## 🏗️ 4. System Architecture & Tech Stack

```text
[ Incoming Request / Login Attempt ]
                 │
                 ▼
[ GhostTrap Heuristic Inspection Engine (Regex + Rules) ]
                 │
       ┌─────────┴─────────┐
       ▼                   ▼
[ Malicious Payload ]   [ Silent Telemetry & Fingerprinting ]
       │                   │
       ▼                   ▼
[ Mirage Admin Vault ]  [ Live Defender SOC Dashboard + JSON Export ]
  (Synthetic Data + 
   Canary CSV Trap)
