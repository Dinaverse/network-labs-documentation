# Challenge: PHP Lover

## Overview
- **Category:** CTF Training - Medium / Web
- **Points:** 250
- **Difficulty:** Easy
- **Status:** Validated

## Description
Exploit an administrative panel with restricted access and a debug feature to achieve remote code execution.

## Solution
1. Reconnaissance: List existing pages in the `/app/` directory and discover a backup file (`admin_panel.php.bak`).
2. Analysis: Download and analyze the `.bak` file to understand the server-side code and its access restrictions.
3. Exploitation: Bypass the access restriction by injecting the `X-Forwarded-For: 127.0.0.1` HTTP header, tricking the server into believing the request originates from `localhost`.
4. Execution: Use the identified debug section (which uses the `eval` or `system` function) to execute system commands (e.g., `system('ls')`).
5. Flag Retrieval: Use the resulting web shell to locate and read the flag file (e.g., `system('cat ../flag*')`).

## Conclusion
Learned the importance of not leaving backup files in production environments, the danger of relying solely on `X-Forwarded-For` headers for access control (as they can be easily spoofed), and the extreme risks of exposing command execution functions like `eval` or `system` to end-users.

## Flag
[REDACTED]
