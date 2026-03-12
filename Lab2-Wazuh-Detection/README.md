# Lab 2 — Wazuh SOC Brute-Force Detection

## Overview
Hands-on Wazuh SIEM/EDR lab simulating SSH brute-force attacks
and building custom detection rules mapped to MITRE ATT&CK framework.

## Tools Used
- Wazuh Manager (SIEM/EDR)
- Kali Linux (Attack machine)
- Ubuntu Linux (Target machine)
- Hydra (Brute-force tool)

## Key Skills Demonstrated
- Wazuh custom rule development
- if_sid and if_matched_sid rule logic
- SSH brute-force detection and alerting
- MITRE ATT&CK T1110 mapping
- Wazuh dashboard alert analysis
- Agent deployment and configuration

## Attack Scenario
| Item | Detail |
|---|---|
| Attack Type | SSH Brute-Force |
| Attacker | Kali Linux VM |
| Target | Ubuntu Linux VM |
| Tool Used | Hydra |
| Detection | Wazuh custom rules |
| MITRE Tactic | T1110 — Brute Force |

## Files
| File | Description |
|---|---|
| `Wazuh_SOC_Project_Report.docx` | Full Wazuh investigation report |
```
