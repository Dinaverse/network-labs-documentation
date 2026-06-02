# Challenge: Discover - Secure access 3

## Overview
- **Category:** Web Server
- **Points:** 30
- **Difficulty:** Medium
- **Status:** Validated

## Description
Delicious cookies.

## Solution
This challenge builds on previous techniques by requiring the simultaneous manipulation of a URL parameter and a browser cookie to escalate privileges.
1. Navigate to the initial challenge URL, noting the parameter `/?use_cookie=0`.
2. Modify this parameter in the address bar to `/?use_cookie=1` to instruct the application to use cookies for identification.
3. Open the browser's developer tools (F12), go to the **Application** (or **Storage**) tab, and locate the cookies for the site.
4. Find the `username` cookie, which is initially set to `visitor`, and change its value to `admin`.
5. Refresh the page. The application validates both the URL parameter and the modified cookie, granting administrative access and revealing the flag.

## Conclusion
Learned that security checks often involve multiple data sources (parameters and cookies). This challenge reinforces the principle that all client-supplied data is untrusted and must be securely validated on the server to prevent privilege escalation attacks.

## Flag
[REDACTED]
