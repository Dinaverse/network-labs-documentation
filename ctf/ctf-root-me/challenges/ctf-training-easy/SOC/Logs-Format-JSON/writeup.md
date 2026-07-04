# Challenge: Logs Format - JSON

## Overview
- **Category:** CTF Training - Easy / SOC
- **Points:** 100
- **Difficulty:** Very easy
- **Status:** Validated

## Description
Analyze JSON-formatted Nginx access logs to investigate a database compromise.

## Solution
1. Identify the suspicious IP address by analyzing request frequency using `jq` to parse the logs.
2. Filter the logs to analyze the interactions of the suspicious IP with the server.
3. Identify the attack pattern (SQL Injection) targeting the `/management/search.php` endpoint.
4. Reconstruct the attack sequence:
    - Determine table column count via `UNION SELECT`.
    - Exfiltrate data from the `users` table and save to a file on the server.
    - Download the exfiltrated file.
    - Delete the table.
5. Identify the critical moments: server integrity was compromised when the file was created, and availability was affected when the table was dropped.
6. Construct the flag using the identified IP, time, status code, and exfiltrated URI.

## Conclusion
Learned to parse and analyze structured JSON logs to reconstruct complex attack patterns, identify SQL injection vulnerabilities, and trace the timeline of a database compromise.
