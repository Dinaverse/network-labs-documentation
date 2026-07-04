# Challenge: SOC - Windows - Registry

## Overview
- **Category:** CTF Training - Hard / SOC
- **Points:** 400
- **Difficulty:** Medium
- **Status:** Validated

## Description
Analyze Windows logs to identify a persistence mechanism hidden in the Registry.

## Solution
1. **Detection:** Used a targeted ELK/Kibana query to monitor for persistence mechanisms added to the Windows Registry's "Run" keys:
   ```kql
   winlog.event_id:13 AND registry.path:"\\CurrentVersion\\Run\\"
   ```
2. **Analysis:** Identified four legitimate entries and one suspicious entry named "Persistence" associated with host `WS06`.
3. **Investigation:** Inspected the event details, identifying the originating process as `powershell.exe` and a suspicious Base64-encoded string in the `Details` field.
4. **Decoding:** Decoded the Base64 content to reveal the hidden flag:
   ```bash
   echo "<BASE64_STRING>" | base64 -d
   ```

## Conclusion
Learned how to detect persistence mechanisms in Windows environments by monitoring Registry modification events (Event ID 13) and analyzing process lineage (e.g., PowerShell initiating Registry changes), highlighting the necessity of centralized logging for anomaly detection.

## Flag
[REDACTED]
