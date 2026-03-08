# 🔐 Cybersecurity Portfolio — Paulson K Babu

![SOC](https://img.shields.io/badge/Role%20Target-SOC%20Analyst-blue?style=for-the-badge&logo=shield&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![GitHub](https://img.shields.io/badge/GitHub-joseph920744-181717?style=for-the-badge&logo=github)

> **Cybersecurity Enthusiast | SOC Analyst Aspirant**
> Hands-on lab projects focused on SIEM, threat detection, log analysis, and SOC operations.

---

## 📂 Projects

| # | Project | Tools | Key Skill |
|---|---------|-------|-----------|
| 1 | [🔵 SIEM Lab — Splunk Brute-Force Detection](#-project-1--siem-implementation-using-splunk) | Splunk, Kali Linux, Ubuntu, Hydra | SPL Queries, SOC Dashboards, Alerts |
| 2 | [🟢 SOC Lab — Wazuh Brute-Force Detection](#-project-2--soc-detection-engineering-using-wazuh) | Wazuh SIEM/XDR, Windows, Linux | Custom Rules, Event Correlation, MITRE ATT&CK |

---

---

## 🔵 Project 1 — SIEM Implementation Using Splunk

![Splunk](https://img.shields.io/badge/Splunk-Enterprise-black?style=flat&logo=splunk&logoColor=green)
![Kali](https://img.shields.io/badge/Kali_Linux-Attacker-557C94?style=flat&logo=kalilinux&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-Target-E95420?style=flat&logo=ubuntu&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat)

### 📌 Overview

Designed and implemented a **Security Information and Event Management (SIEM)** lab using **Splunk Enterprise**. Real-world SSH brute-force attacks were simulated using Hydra and detected using custom **SPL (Search Processing Language)** queries, real-time alerts, and SOC dashboards.

> **Role Target:** SOC Analyst (Tier 1/2) | Security Analyst | Threat Detection Engineer

---

### 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Splunk Enterprise** | SIEM platform — log indexing, SPL queries, alerts, dashboards |
| **Kali Linux** | Attacker machine — SSH brute-force simulation |
| **Ubuntu Linux** | Target machine — OpenSSH server, auth log source |
| **Hydra** | Brute-force tool using rockyou.txt wordlist |
| **Splunk Universal Forwarder** | Forwards `/var/log/auth.log` to Splunk indexer |
| **VirtualBox** | Virtualization platform for the lab environment |

---

### 🎯 Objectives

- ✅ Build a SIEM lab using Splunk, Kali Linux, and Ubuntu
- ✅ Collect and ingest Linux authentication logs (`/var/log/auth.log`) into Splunk
- ✅ Simulate SSH brute-force attacks using Hydra + rockyou.txt wordlist
- ✅ Develop SPL detection queries for brute-force and invalid user attempts
- ✅ Configure real-time alerts triggered on attack thresholds
- ✅ Design a SOC Dashboard to visualize attacker behavior

---

### 🏗️ Lab Architecture

```
┌─────────────────┐     SSH Brute-Force      ┌─────────────────┐
│   Kali Linux    │ ───────────────────────► │  Ubuntu Linux   │
│  192.168.50.1   │                          │  192.168.50.4   │
│  (Attacker)     │                          │  (Target/SIEM)  │
└─────────────────┘                          └────────┬────────┘
                                                      │
                                            /var/log/auth.log
                                                      │
                                             Universal Forwarder
                                                      │
                                                      ▼
                                          ┌─────────────────────┐
                                          │  Splunk Enterprise  │
                                          │  localhost:8000     │
                                          │                     │
                                          │  • SPL Queries      │
                                          │  • Real-time Alerts │
                                          │  • SOC Dashboards   │
                                          └─────────────────────┘
```

---

### 🔍 Key SPL Queries

**Detect Failed SSH Login Attempts**
```spl
search source=/var/log/auth.log "failed password"
```

**Brute-Force Detection (Threshold-Based)**
```spl
index=main sourcetype="linux_secure" "failed password"
| bucket _time span=1m
| stats count by src_ip
| where count>=5
```

**Detect Invalid User Login Attempts**
```spl
index=main sourcetype="linux_secure" "invalid user"
| rex "(?i)invalid user (?<extracted_user>\w+) from (?<extracted_ip>\d+\.\d+\.\d+\.\d+)"
| where isnotnull(extracted_user) AND isnotnull(extracted_ip)
| stats count by extracted_user, extracted_ip
| sort - count
```

**Detect Privilege Escalation via sudo**
```spl
index=main sourcetype="linux_secure" "sudo"
| rex "sudo:\s+(?<extracted_user>\w+)\s+:"
| where isnotnull(extracted_user)
| stats count by extracted_user
| sort - count
```

**Top Attacking IP Addresses**
```spl
index=main sourcetype="linux_secure" "invalid user"
| rex "(?i)invalid user (?<extracted_user>\w+) from (?<extracted_ip>\d+\.\d+\.\d+\.\d+)"
| where isnotnull(extracted_ip)
| stats count by extracted_ip
| sort - count
| head 10
```

---

### 🚨 Alert Configuration

| Setting | Value |
|---------|-------|
| **Alert Name** | Bruteforce Detection |
| **Type** | Real-time |
| **Trigger Condition** | Number of results > 0 in 1 minute |
| **Severity** | High |
| **Throttle** | Suppress for 10 minutes |
| **Action** | Add to Triggered Alerts |

---

### 📊 Results & Key Findings

| Metric | Result |
|--------|--------|
| Total failed login events | **525+ events** in 24-hour window |
| Top attacker IP | **192.168.50.1** (Kali Linux) — ~400 attempts |
| Invalid usernames targeted | **hacker, admin, fakeuser** |
| Brute-force alert | **Fired correctly** — High severity |
| Privilege escalation captured | **22 sudo commands** by user jude |
| Attack peak window | **5:00 PM Mar 6 – 1:00 AM Mar 7, 2026** |

---

### 🧠 Skills Demonstrated

- SIEM configuration and log ingestion
- SPL (Search Processing Language) query development
- Real-time alert engineering in Splunk
- SOC Dashboard design and visualization
- SSH brute-force simulation with Hydra
- Linux log analysis (`/var/log/auth.log`)

---

---

## 🟢 Project 2 — SOC Detection Engineering Using Wazuh

![Wazuh](https://img.shields.io/badge/Wazuh-SIEM%20%2F%20XDR-blue?style=flat&logo=wazuh&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-Target-0078D6?style=flat&logo=windows&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-Wazuh%20Manager-FCC624?style=flat&logo=linux&logoColor=black)
![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-T1110-red?style=flat)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat)

### 📌 Overview

Built and validated a **custom frequency-based correlation rule** in Wazuh SIEM to detect Windows brute-force login attacks. Multiple failed authentication events were aggregated within a defined timeframe and escalated as a **Level 12 Critical alert** mapped to **MITRE ATT&CK T1110**.

> **Role Target:** SOC Analyst (Tier 1/2) | Detection Engineer | Security Analyst

---

### 🛠️ Lab Environment

| Component | Details |
|-----------|---------|
| **Wazuh Manager** | Linux server — processes rules and generates alerts |
| **Wazuh Agent** | Windows endpoint — forwards Security Event Logs |
| **Log Source** | Windows Security Event ID 4625 (Failed Logon) |
| **Dashboard** | Wazuh Web Interface — Discover + Threat Hunting |
| **Custom Rule File** | `/var/ossec/etc/rules/local_rules.xml` |
| **Custom Rule ID** | 100200 |

---

### 🎯 Objectives

- ✅ Build a custom frequency-based correlation rule in `local_rules.xml`
- ✅ Detect brute-force behavior — 3 failed logins within 120 seconds
- ✅ Validate real-time alert generation in Wazuh Dashboard
- ✅ Map the detection to MITRE ATT&CK T1110 (Brute Force)
- ✅ Troubleshoot and resolve Wazuh configuration errors

---

### 🏗️ Lab Architecture

```
┌──────────────────────┐    Failed Logins    ┌───────────────────┐
│  Windows Endpoint    │ ──────────────────► │   Wazuh Agent     │
│  (Target Machine)    │                     │  (on Windows)     │
└──────────────────────┘                     └────────┬──────────┘
                                                      │
                                          Event ID 4625 logs
                                                      │
                                                      ▼
                                          ┌─────────────────────┐
                                          │   Wazuh Manager     │
                                          │   (Linux Server)    │
                                          │                     │
                                          │  Rule 100200        │
                                          │  freq=3 / 120s      │
                                          │  Level 12 Critical  │
                                          └──────────┬──────────┘
                                                     │
                                                     ▼
                                          ┌─────────────────────┐
                                          │  Wazuh Dashboard    │
                                          │  Discover + Threat  │
                                          │  Hunting views      │
                                          └─────────────────────┘
```

---

### 📝 Custom Detection Rule

```xml
<rule id="100200" level="12" frequency="3" timeframe="120">
  <if_matched_sid>60122</if_matched_sid>
  <description>Multiple Windows login failures detected. Possible brute-force attack.</description>
  <mitre><id>T1110</id></mitre>
</rule>
```

| Parameter | Value | Meaning |
|-----------|-------|---------|
| `frequency` | 3 | Events needed to trigger |
| `timeframe` | 120s | Time window for counting |
| `level` | 12 | Critical severity |
| `if_matched_sid` | 60122 | Parent rule — Windows failed auth |
| MITRE | T1110 | Brute Force technique |

---

### ⚠️ Key Concept — `if_sid` vs `if_matched_sid`

| Directive | Behavior |
|-----------|----------|
| `if_sid` | Triggers on a **single event** — cannot be used with frequency |
| `if_matched_sid` | **Counts multiple events** over time — required for brute-force detection |

> ⚠️ Using `if_sid` with `frequency` causes: `ERROR: Invalid use of frequency`

---

### 📊 Alert Results

| Field | Value |
|-------|-------|
| **Rule ID** | 100200 |
| **Severity** | Level 12 — Critical |
| **Trigger** | 3 failed logins within 120 seconds |
| **MITRE** | T1110 — Brute Force |
| **Alert status** | ✅ Fired correctly in Discover + Threat Hunting |

---

### 🧠 Skills Demonstrated

- Custom Wazuh rule development (`local_rules.xml`)
- Frequency-based event correlation in SIEM
- Windows Security Event Log analysis (Event ID 4625)
- Real-time alert configuration and validation
- MITRE ATT&CK framework mapping
- Troubleshooting Wazuh Manager configuration errors
- Full SOC workflow: **Configure → Restart → Simulate → Validate → Document**

---

---

## 📁 Repository Files

| File | Description |
|------|-------------|
| `Splunk_SIEM_Project_Report_Final.docx` | Full Splunk project report with screenshots |
| `SOC_Wazuh_Brute_Force_Detection_Documentation.docx` | Full Wazuh project report with screenshots |
| `Wazuh_README.md` | Standalone Wazuh project documentation |
| Other `.docx` files | Additional cybersecurity lab reports |

---

## 👤 About Me

**Paulson K Babu**
Cybersecurity Enthusiast | SOC Analyst Aspirant

- 🎓 Master of Computer Applications (MCA)
- 🔍 Focused on: SIEM, Threat Detection, Log Analysis, SOC Operations
- 🛠️ Tools: Splunk, Wazuh, Kali Linux, Wireshark, Nmap, OWASP ZAP

[![GitHub](https://img.shields.io/badge/GitHub-joseph920744-181717?style=flat&logo=github)](https://github.com/joseph920744)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/)

---

## 📄 License

All projects are for educational purposes only. All simulations were conducted in isolated, controlled lab environments.

---

> *"The best way to learn cybersecurity is to build, break, detect, and document."*
