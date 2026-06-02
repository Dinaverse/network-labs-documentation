# Challenge: SOC Web - Command injection

## Overview
- **Category:** CTF Training - Medium / SOC
- **Points:** 250
- **Difficulty:** Easy
- **Status:** Validated

## Description
Reconstruct an attacker's activity on a web application by analyzing Nginx and ModSecurity logs.

## Solution
1. **Initial Analysis:** Sorted logs chronologically to understand the attack timeline.
2. **Attacker Identification:** Used log frequency analysis (client IP counting) to identify the attacker's IP (`99.101.27.71`), which generated the vast majority of requests.
3. **Log Filtering:** Filtered for the attacker's IP and excluded 404 responses to focus on successful malicious activity.
4. **Endpoint Discovery:** Identified intensive fuzzing on the `/development/` path and subsequent exploitation via POST requests.
5. **Log Correlation:** Switched to ModSecurity audit logs to examine request bodies, revealing exploitation of a `find` command through an `options` parameter to execute external `curl` and `wget` commands, used to download a web shell (`th1s1sn0tAsh3ll_.php`) from a malicious domain (`files.rawndesome.ware`).
6. **Web Shell Analysis:** Analyzed successful requests to the web shell with command execution parameters (e.g., `whoami`, `ls`, `id`) and decoded Base64-encoded payloads to extract a secret message.
7. **Metric Extraction:** Filtered logs for the `/home` path to count total requests (38).

## Conclusion
Learned to perform deep log analysis by correlating data across multiple log sources (Apache/ModSecurity), identify attack patterns (fuzzing, command injection, web shell backdoor), and use forensic techniques like Base64 decoding and infrastructure mapping to reconstruct an attack.
