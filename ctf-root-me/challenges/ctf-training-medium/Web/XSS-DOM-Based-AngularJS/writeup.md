# Challenge: XSS - DOM Based - AngularJS

## Overview
- **Category:** CTF Training - Medium / Web
- **Points:** 400
- **Difficulty:** Medium
- **Status:** Validated

## Description
Find a DOM-based XSS vulnerability in an AngularJS application to obtain user account details.

## Solution
1. Reconnaissance: Navigate to the login page and confirm the use of AngularJS. Analyze the page source and loaded scripts (`script.js`).
2. Probing: Test various XSS payloads (e.g., `<script>`, Angular interpolation `{{ }}`, `ng-click`) in input fields and URL parameters.
3. Analysis: Investigate the role of "TrigonometryJS" and examine how the application processes inputs.
4. Identification: Recognize environmental limitations (such as restricted access to `window` and `localStorage` objects) that complicate standard DOM XSS exploitation.
5. Note: The investigation indicated that standard vectors were ineffective, suggesting the vulnerability is tied to subtle AngularJS processing or less common data sources.

## Conclusion
Learned that client-side XSS vulnerabilities in modern frameworks like AngularJS can be complex, often requiring deep understanding of the framework's data-binding and processing logic, and that environmental restrictions can significantly alter exploitation methods.
