# Challenge: SOC Linux - Cron - Backup

## Overview
- **Category:** CTF Training - Medium / SOC
- **Points:** 200
- **Difficulty:** Easy
- **Status:** Validated

## Description
Analyze Auditd logs to reconstruct an attack originating from a compromised CRON job that led to data leakage and backdoor deployment.

## Solution
1. **Identification of Exploited Program:** Analyzed Auditd logs in the ELK stack, focusing on frequent executions. Identified `cron` as the most common executable running with elevated privileges.
2. **Identification of Compromised File:** Filtered logs using `CRON AND CMD` to observe executed tasks. Identified a recurring Bash script, `backup_home.sh`, which was periodically executed by Cron.
3. **Backdoor Analysis:** Filtered Auditd logs for `EXECVE` type events to detect suspicious activity. Identified an entry with the key `susp_activity` at a specific timestamp.
4. **Command Reconstruction:** Extracted the arguments from the suspicious `EXECVE` log entry to reconstruct the network command used to establish a remote connection (a reverse shell) to an attacker-controlled IP and port. 
5. **Confirmation:** Correlated the command execution with subsequent SSH activity, confirming the establishment of a persistent backdoor.

## Conclusion
Learned how to analyze system-level audit logs to detect process execution anomalies, identify compromised scheduled tasks, and reconstruct malicious command-line activity that establishes unauthorized network access.
