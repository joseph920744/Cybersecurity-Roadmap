# Lab 1 — Splunk SIEM Analysis

## Overview
Hands-on Splunk SIEM lab simulating SSH brute-force attacks
and privilege escalation detection on Ubuntu Linux.

## Tools Used
- Splunk Enterprise (Free Trial)
- Kali Linux (Attack machine)
- Ubuntu Linux (Target machine)
- Hydra (Brute-force tool)

## Key Skills Demonstrated
- SPL query writing with rex field extraction
- linux_secure log ingestion and parsing
- SSH brute-force detection
- Privilege escalation alerting
- MITRE ATT&CK T1110 mapping

## Files
| File | Description |
|---|---|
| `Splunk_SIEM_Project_Report_Final.docx` | Full investigation report |
| `splunk_ftp_log_analysis.docx` | FTP log analysis report |
| `splunkhttplog.docx` | HTTP log analysis report |
| `DNSLOGanalysis.docx` | DNS log analysis report |
## Attack Scenario
| Item | Detail |
|---|---|
| Attack Type | SSH Brute-Force + Privilege Escalation |
| Attacker | Kali Linux VM |
| Target | Ubuntu Linux VM |
| Tool Used | Hydra |
| Detection | Splunk SPL queries on linux_secure logs |
| MITRE Tactic | T1110 — Brute Force |
```

