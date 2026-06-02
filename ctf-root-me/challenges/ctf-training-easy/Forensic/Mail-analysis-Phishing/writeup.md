# Challenge: Mail analysis - Phishing

## Overview
- **Category:** CTF Training - Easy / Forensic
- **Points:** 150
- **Difficulty:** Easy
- **Status:** Validated

## Description
Analyze an email file to identify a phishing attempt.

## Solution
1. Identify all unique senders in the email logs using `grep` and `uniq` to find suspicious entries (e.g., a domain similar to the legitimate one).
2. Isolate and search for the specific phishing email.
3. Identify the target recipient by inspecting the email headers.
4. Extract the body and attachments of the email using tools like `ripmime` to analyze the content.
5. Search the extracted email body for URLs containing parameters to identify the phishing link.
6. The link reveals a credential harvesting attempt targeting a specific domain.

## Conclusion
Learned to analyze email headers and bodies to detect phishing, including identifying spoofed domains, extracting attachments, and discovering malicious URLs.
