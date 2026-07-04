# Challenge: SQL - Truncation

## Overview
- **Category:** CTF Training - Medium / Web
- **Points:** 300
- **Difficulty:** Medium
- **Status:** Validated

## Description
Exploit SQL string truncation to perform an account takeover.

## Solution
1. **Vulnerability Analysis:** Identified that the application is vulnerable to SQL truncation. Due to database column length constraints, any input exceeding the maximum allowed length is silently truncated by the database engine.
2. **Payload Crafting:** Created a registration payload consisting of `admin` + sufficient padding characters + an additional character (e.g., `a`). When inserted into the database, the username is truncated to match the existing `admin` account name.
3. **Registration:** Registered this crafted payload with a new password of my choice. Due to the truncation behavior, the database updated the existing `admin` account's password with the new one provided during this registration.
4. **Authentication:** Successfully logged in as `admin` using the password set during the crafted registration process.

## Conclusion
Learned that database-level string truncation can lead to severe security flaws, including account takeover. This highlights the absolute necessity of application-side input length validation, rather than relying on database-level constraints to enforce data integrity and security.

## Flag
[REDACTED]
