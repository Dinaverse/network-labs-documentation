# Challenge: SOC - Windows - AS-REP Roasting

## Overview
- **Category:** CTF Training - Medium / SOC
- **Points:** 300
- **Difficulty:** Medium
- **Status:** Validated

## Description
Identify and investigate an AS-REP Roasting attack using an ELK stack.

## Solution
1. **Understanding AS-REP Roasting:** Recognize that this attack targets Kerberos accounts with the "Do not require Kerberos pre-authentication" attribute enabled, allowing attackers to request TGTs and crack them offline.
2. **Detection Strategy:** Utilize the ELK stack to search for indicators of this attack.
3. **Kibana/ELK Analysis:** Perform a targeted search for the relevant Windows Event ID:
   ```kql
   winlog.event_id: "4768" AND winlog.event_data.TicketEncryptionType : "0x17"
   ```
4. **Indicators of Compromise (IOCs):**
   - **Event ID:** 4768 (Kerberos authentication ticket request)
   - **PreAuthType:** 0 (No pre-authentication required)
   - **TicketEncryptionType:** 0x17 (RC4-HMAC)
   - **Attacker Source IP:** 192.168.100.55
   - **Target User:** svc_nopreauth@domain.local
5. **Validation:** Correlate these indicators to confirm the AS-REP Roasting attempt and the successful ticket retrieval.

## Conclusion
Learned to detect AS-REP Roasting attacks by analyzing specific Kerberos authentication events (4768) in Windows logs, focusing on the absence of pre-authentication (Type 0) and specific ticket encryption types, which are tell-tale signs of this reconnaissance/exploitation technique.

## Flag
[REDACTED]
