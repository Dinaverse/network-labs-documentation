# Challenge: SOC Network - DNS Exfiltration

## Overview
- **Category:** CTF Training - Hard / SOC
- **Points:** 350
- **Difficulty:** Medium
- **Status:** Validated

## Description
Investigate unusual DNS queries to detect potential data exfiltration.

## Solution
1. **Log Analysis:** Filtered DNS logs in Kibana to show only queries that received a valid answer, reducing noise from fake queries.
2. **Anomalous Domain Discovery:** Identified suspicious domains frequently queried, specifically `oastify.com` and `git-claude.fr`.
3. **Information Gathering:** Analyzed the `git-claude.fr` traffic, revealing queries related to AES-CBC configuration parameters, which provided the key and IV for decryption.
4. **Data Identification:** Filtered for long DNS query strings (longer than 60 characters) targeting `oastify.com` to isolate the exfiltrated ciphertext.
5. **Decryption:**
   - Collected the observed ciphertext segments.
   - Utilized a Python script with `pycryptodome` (AES-CBC) and the discovered parameters to decrypt the data.
   - Performed PKCS7 unpadding to reveal the final flag.

## Conclusion
Learned that DNS exfiltration often involves data being encrypted or encoded and smuggled within DNS query subdomains. Effective detection requires filtering for successful queries, analyzing anomalous domain traffic, identifying configuration parameters (like AES keys) within traffic, and reassembling/decrypting the exfiltrated data.

## Flag
[REDACTED]
