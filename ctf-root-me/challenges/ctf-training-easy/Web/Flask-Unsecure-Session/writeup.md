# Challenge: Flask - Unsecure Session

## Overview
- **Category:** CTF Training - Easy / Web
- **Points:** 200
- **Difficulty:** Easy
- **Status:** Validated

## Description
Forge a Flask session cookie using a weak secret key to become an administrator and retrieve the flag.

## Solution
1. Decode the initial `session` cookie using `flask-unsign` to understand its structure (e.g., `{'admin': 'false', 'username': 'guest'}`).
2. Identify that the session relies on a secret key to sign the cookie.
3. Brute-force the Flask server's `secret_key` using `flask-unsign` and a wordlist (e.g., `rockyou.txt`).
4. Once the secret key is discovered, create a new payload setting the administrative privilege (e.g., `{'admin': 'true', 'username': 'admin'}`).
5. Use `flask-unsign` to sign this forged payload with the discovered secret key to generate a new valid session cookie.
6. Replace the browser's session cookie with the forged one and reload the `/administration` page to retrieve the flag.

## Conclusion
Learned that Flask sessions are vulnerable when using weak, predictable secret keys. This demonstrates the necessity of using strong, cryptographically secure random keys to prevent unauthorized session forging and privilege escalation.
