# Challenge: JavaScript - Obfuscation 2

## Overview
- **Category:** CTF Training - Easy / Web
- **Points:** 150
- **Difficulty:** Easy
- **Status:** Validated

## Description
De-obfuscate JavaScript authentication logic to retrieve the password and log in.

## Solution
1. Identify the obfuscated JavaScript login function in the page source code.
2. Observe that the password verification uses multiple nested `eval()` calls along with `atob()` (Base64 decoding) and `unescape()` (URL decoding).
3. Systematically de-obfuscate the string:
   - Decode the outermost Base64 string.
   - Perform multiple rounds of URL decoding on the resulting string.
   - Convert the character codes (e.g., from `String.fromCharCode(...)`) into their ASCII character representations.
   - Perform a final Base64 decode to reveal the plaintext password.
4. Use the discovered username ("Adm1n") and the de-obfuscated password to authenticate on the `/admin` page and retrieve the flag.

## Conclusion
Learned that client-side obfuscation (using techniques like nested encoding and dynamic execution) is not a security measure, as the client-side code must ultimately be interpreted by the browser, allowing an attacker to reverse the obfuscation process and retrieve hardcoded secrets.
