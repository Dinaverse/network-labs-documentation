# Challenge: Linux Privesc - Module Hijacking

## Overview
- **Category:** CTF Training - Medium / System
- **Points:** 300
- **Difficulty:** Medium
- **Status:** Validated

## Description
Escalate privileges by hijacking a Python module imported by a root-level cron job.

## Solution
1. **Reconnaissance:** Use `pspy` to monitor system processes and identify a Python script (`tcp_monitor.py`) executing with root privileges (`UID=0`) periodically via cron.
2. **Analysis:** Examine the cron job configuration (`/etc/cron.d/tcp_monitor`) and identify that the script runs from `/opt/backup_tool`.
3. **Vulnerability Assessment:** Inspect the permissions of the directory `/opt/backup_tool`, finding it is world-writable (777). Furthermore, understand that Python imports modules from the current directory, allowing an attacker to place a malicious module that the script will import instead of the standard one.
4. **Exploitation:**
   - Create a malicious `glob.py` file in `/opt/backup_tool` that shadows the standard library module.
   - Inject code into the `glob` function to execute arbitrary commands, such as exfiltrating a flag to `/tmp/flag.txt` or modifying `/etc/sudoers` to grant the current user passwordless root access.
5. **Execution:** Wait for the cron job to execute the script as root, which triggers the malicious module's code.
6. **Flag/Access:** Read the exfiltrated flag from `/tmp/flag.txt` or use the newly acquired sudo privileges (`sudo su`) to gain full root access.

## Conclusion
Learned to identify insecure Python module imports, highlighting the extreme risk of running scripts as root when they have dependencies located in writeable directories. This emphasizes the need for restricted permissions and explicit import paths.

## Flag
[REDACTED]
