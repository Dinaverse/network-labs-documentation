# Challenge: API - Broken Access

## Overview
- **Category:** CTF Training - Easy / Web
- **Points:** 100
- **Difficulty:** Very easy
- **Status:** Validated

## Description
Exploit an Insecure Direct Object Reference (IDOR) vulnerability on an eHealth platform to access unauthorized medical records.

## Solution
1. Reconnaissance: Create a patient account, log in, and navigate to the dashboard to load the medical record.
2. HTTP Request Analysis: Use browser developer tools (Network tab) to inspect the request that loads the patient's record (e.g., `GET /api/patients/2`).
3. Vulnerability Exploitation: Recognize that the numerical identifier in the URL path is the object reference. Modify the ID (e.g., changing `2` to `1`) to attempt access to another resource.
4. Access: The application fails to perform proper authorization checks, returning the administrator's record. Retrieve the flag from the `secret_note` field.

## Conclusion
Learned about IDOR vulnerabilities, which occur when applications expose internal object references in URLs or parameters without adequate authorization checks, allowing attackers to access unauthorized resources.
