# Challenge: Discover - Secure access 1

## Overview
- **Category:** Web Server
- **Points:** 20
- **Difficulty:** Easy
- **Status:** Validated

## Description
Are you a 1 or a 0 ?

## Solution
This challenge demonstrates a basic vulnerability in user permission management where administrative access is controlled by a simple URL parameter.
1. Access the challenge page and observe the URL structure, noting the parameter `/?admin=0`.
2. Recognize that this parameter likely controls the user's privilege level.
3. Manually modify the URL in the browser's address bar, changing the value to `/?admin=1`.
4. Reload the page. The application interprets the modified parameter as a request for administrative access and displays the flag.

## Conclusion
Learned how insecure parameter handling can lead to unauthorized access. This highlights the importance of performing robust, server-side authorization checks rather than relying on easily manipulated client-side parameters to define user roles.

## Flag
[REDACTED]
