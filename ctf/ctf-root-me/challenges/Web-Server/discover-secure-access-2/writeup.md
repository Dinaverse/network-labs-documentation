# Challenge: Discover - Secure access 2

## Overview
- **Category:** Web Server
- **Points:** 20
- **Difficulty:** Easy
- **Status:** Validated

## Description
It's all in the name.

## Solution
Similar to the previous challenge, this task explores vulnerabilities related to insecure parameter handling in the URL, specifically targeting user identification.
1. Navigate to the challenge page and observe the URL ending in `/?username=visitor`.
2. Recognize that the application uses this parameter to determine the current user's identity.
3. Manually modify the URL in the address bar, changing the value to `/?username=admin`.
4. Reload the page. The application erroneously accepts the user-supplied value as truth and grants administrative access, revealing the flag.

## Conclusion
Learned that using URL parameters to identify or authorize users is highly insecure. Robust authentication and authorization must be handled on the server side (e.g., using session tokens) to prevent attackers from simply "impersonating" roles by modifying client-side inputs.

## Flag
[REDACTED]
