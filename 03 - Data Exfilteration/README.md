# Data Exfiltration – Netcat

## Overview

Hands-on simulation of data exfiltration after obtaining root access on a DVWA lab machine.

A dummy file containing simulated sensitive customer data was created on the target and transferred to the Kali Linux attacker machine using a raw TCP connection with Netcat.

## Objective

- Simulate sensitive data theft after privilege escalation.
- Transfer a file from the compromised target to the attacker machine.
- Analyze the lack of detection during the transfer.
- Identify security controls that could prevent or detect data exfiltration.

## Environment

- Attacker: Kali Linux
- Target: DVWA VM
- Attack Stage: Post-exploitation
- Preceding Stage: SUID nmap privilege escalation

## Tools

- Netcat
- Wireshark
- Kali Linux
- Linux

## Methodology

1. Created a dummy sensitive file on the target after obtaining root access.
2. Started a Netcat listener on Kali Linux to receive the data.
3. Transferred the file from the target to Kali over TCP port 5555.
4. Confirmed the connection and successful transfer.
5. Verified the received file on the Kali machine.
6. Analyzed the transfer using network evidence.

## Finding

**Undetected Data Exfiltration via Raw TCP (Netcat)**

The simulated sensitive file was successfully transferred from the target to the attacker machine over TCP port 5555 without triggering any alerts or detection mechanisms.

The data was transferred in plain text without encryption or obfuscation.

## Impact

- Simulated sensitive customer data was successfully stolen.
- No alerts or detection mechanisms were triggered.
- Root-level access allowed unrestricted access to files on the target.
- Demonstrates the potential impact of inadequate outbound network monitoring and DLP controls.

## Root Cause

- Lack of outbound network monitoring and alerting.
- No Data Loss Prevention (DLP) controls.
- No network segmentation restricting outbound connections.
- Root access obtained through the upstream SUID nmap misconfiguration.

## Remediation

- Monitor and alert on unexpected outbound connections.
- Implement DLP controls for sensitive data.
- Enforce network segmentation.
- Apply firewall egress filtering.
- Restrict outbound connections to required ports and destinations.
- Fix the upstream vulnerabilities that enabled root access.

## Attack Chain

**SQL Injection → Credential Compromise → Command Execution → Privilege Escalation → Data Exfiltration**

> All testing was performed in an authorized and isolated laboratory environment using simulated sensitive data for educational purposes.
