# Challenge: AD Secrets - Kerberos TGT

## Overview
- **Category:** CTF Training - Medium / Active Directory
- **Points:** 200
- **Difficulty:** Easy
- **Status:** Validated

## Description
Analyze a Kerberos ticket file and extract the Ticket Session Key.

## Solution
1. Analysis: The objective was to analyze a Kerberos ticket file (`administrator.kirbi`). Identified it as a DER-encoded `KRB-CRED` object (Application Tag 22).
2. Extraction: The encryption type was identified as AES256-CTS-HMAC-SHA1-96 (etype 18).
3. Retrieval: Extracted the Ticket Session Key from the plaintext `EncKrbCredPart`.

## Conclusion
Learned to parse and analyze Kerberos ticket files, which is a crucial skill for Active Directory security assessments and understanding ticket-based authentication.

## Flag
[REDACTED]
