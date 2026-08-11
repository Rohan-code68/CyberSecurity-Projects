# SOC Incident Investigation – End-to-End Attack Simulation

## Overview

Hands-on SOC investigation of a simulated end-to-end cyberattack conducted in an isolated VirtualBox lab.

The investigation covered the complete attack chain from reconnaissance and exploitation to privilege escalation and data exfiltration, followed by defensive analysis and incident reconstruction.

## Objectives

- Investigate and reconstruct a complete cyberattack.
- Analyze network and system evidence from multiple sources.
- Build an accurate attack timeline.
- Identify Indicators of Compromise (IOCs).
- Map attacker activity to the MITRE ATT&CK framework.
- Identify detection gaps and recommend security controls.

## Environment

- Attacker: Kali Linux
- Target: DVWA / Metasploitable VM
- Network: Isolated VirtualBox network
- Packet Capture: `lab_capture.pcap`

## Tools

- Wireshark
- Nmap
- Burp Suite
- SQLMap
- Hashcat
- Netcat
- Linux logs

## Attack Chain

**Reconnaissance → SQL Injection → Credential Compromise → Command Injection → Reverse Shell → Privilege Escalation → Data Exfiltration**

## Investigation

The attack was reconstructed by correlating three independent evidence sources:

- **Wireshark** – Network traffic and packet capture analysis
- **Web server access logs** – Reconnaissance and SQL Injection activity
- **System authentication logs** – Post-exploitation authentication activity

The packet capture contained evidence of the attack from reconnaissance through data exfiltration. :contentReference[oaicite:1]{index=1}

## Key Findings

| Stage | Finding | Result |
|---|---|---|
| Reconnaissance | Nmap scanning | Open services identified |
| Initial Access | SQL Injection | Usernames and password hashes extracted |
| Credential Access | Hash cracking | Plaintext credentials recovered |
| Execution | OS Command Injection | Reverse shell as `www-data` |
| Privilege Escalation | SUID `nmap` | Escalated to root |
| Exfiltration | Netcat over TCP 5555 | Sensitive simulated data transferred |

The report classified all four major technical findings as **Critical**. :contentReference[oaicite:2]{index=2}

## Indicators of Compromise

Key IOCs identified during the investigation included:

- SQL Injection payloads containing `UNION SELECT`
- Outbound TCP connection on port `4444`
- Outbound TCP connection on port `5555`
- Nmap scanning patterns
- Shell processes spawned by `www-data`
- `nmap --interactive` execution
- Netcat connections from the target
- Files written to `/tmp`

## Detection Gaps

The investigation identified several missing or ineffective controls:

- No IDS/IPS detection for scanning activity
- No WAF protection against injection attacks
- No alerting for non-standard outbound ports
- No SUID auditing
- No process monitoring
- No DLP controls
- No egress firewall restrictions

## MITRE ATT&CK

The attack activity was mapped to techniques including:

- T1595 – Active Scanning
- T1190 – Exploit Public-Facing Application
- T1552 – Unsecured Credentials
- T1110.002 – Password Cracking
- T1059.004 – Unix Shell
- T1548.001 – Setuid
- T1005 – Data from Local System
- T1041 – Exfiltration Over C2 Channel
- T1571 – Non-Standard Port

## Recommendations

- Implement SIEM-based log correlation and real-time alerting.
- Deploy WAF protection for web applications.
- Monitor non-standard outbound connections.
- Implement SUID auditing and least-privilege controls.
- Deploy DLP and egress firewall controls.
- Use parameterized SQL queries.
- Monitor suspicious processes spawned by web server accounts.
- Conduct regular penetration testing and security audits.

## Evidence

The investigation included:

- Network packet capture
- Wireshark analysis
- Web server access logs
- System authentication logs
- Attack timeline
- IOC analysis
- MITRE ATT&CK mapping
- Detection-gap analysis

> All activity was performed in an isolated and authorized laboratory environment for educational purposes.
