# Challenge: Linux Privesc - Argument Injection

## Overview
- **Category:** CTF Training - Hard / System
- **Points:** 400
- **Difficulty:** Medium
- **Status:** Validated

## Description
Escalate privileges by exploiting argument injection via wildcards in a backup script.

## Solution
1. **Reconnaissance:** Identified a script (`backup.sh`) running as root via cron that performs backups using `zip -r /root/backups/backup_$DATE.zip *` inside a directory.
2. **Vulnerability:** The script uses the wildcard character `*` in the `zip` command. Since the directory is world-writable, an attacker can create files with names that are interpreted as command-line arguments to `zip`. This is a "wildcard injection" vulnerability.
3. **Exploitation:** Used the `--unzip-command` option of the `zip` utility to execute arbitrary code. 
   - Created a malicious shell script (`shell.sh`) that modifies `/etc/sudoers` to grant the user passwordless root access.
   - Created files in the backup directory named `-T` and `--unzip-command=sh shell.sh`.
4. **Access:** When the cron job executed the `zip` command, it interpreted these filenames as command-line arguments, executing `shell.sh` with root privileges. Subsequently, used `sudo su` to become root and read the flag.

## Conclusion
Learned that wildcards in shell commands can lead to dangerous argument injection vulnerabilities. This emphasizes the need to avoid wildcards in command arguments or use `--` to indicate the end of command options.

## Flag
[REDACTED]
