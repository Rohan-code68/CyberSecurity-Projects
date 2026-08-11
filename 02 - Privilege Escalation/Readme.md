# Linux Privilege Escalation – SUID Misconfiguration

## Overview

Hands-on Linux privilege escalation testing performed in a controlled DVWA/Metasploitable-style lab environment.

The assessment identified an SUID misconfiguration on `/usr/bin/nmap`, which allowed escalation from the low-privileged `www-data` account to root.

## Objective

- Enumerate SUID binaries.
- Identify misconfigured binaries with elevated privileges.
- Analyze the security impact of the SUID misconfiguration.
- Demonstrate privilege escalation from `www-data` to root.
- Provide remediation recommendations.

## Environment

- Target: DVWA / Metasploitable-style VM
- Attacker: Kali Linux
- Initial Access: DVWA Command Execution
- Initial Privilege: `www-data`
- Vulnerability: SUID Misconfiguration

## Tools

- Kali Linux
- Nmap
- Linux shell

## Methodology

1. Obtained an initial reverse shell as `www-data` through DVWA Command Execution.
2. Enumerated SUID binaries on the target system.
3. Identified `/usr/bin/nmap` with the SUID permission.
4. Analyzed the legacy interactive functionality of the installed Nmap version.
5. Used the interactive shell-escape functionality to obtain a privileged shell.
6. Verified successful privilege escalation by checking the current user.

## Finding

**SUID misconfiguration on `/usr/bin/nmap`**

Nmap was configured with the SUID bit, causing it to execute with the privileges of its file owner. The installed legacy version also provided interactive shell-escape functionality.

This combination allowed the low-privileged `www-data` account to obtain a root shell.

## Result

**Privilege escalation successfully achieved:**

`www-data → root`

## Impact

Successful exploitation could provide complete control of the target system, including:

- Unauthorized file access
- User creation
- Malware installation
- Persistent backdoors
- Full administrative control

## Root Cause

The root cause was unnecessary SUID permission assigned to Nmap combined with legacy shell-escape functionality.

## Remediation

- Remove the SUID bit from Nmap unless explicitly required.
- Regularly audit SUID binaries.
- Apply the principle of least privilege.
- Keep Nmap and other system software updated.
- Remove or restrict unnecessary privileged functionality.

> All testing was performed in an authorized and isolated laboratory environment for educational purposes.
