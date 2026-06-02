# Challenge: File Upload - Null bytes

## Overview
- **Category:** CTF Training - Easy / Web
- **Points:** 200
- **Difficulty:** Easy
- **Status:** Validated

## Description
Bypass file upload restrictions using null byte injection to execute malicious code.

## Solution
1. Identify the vulnerability: The application performs weak file extension validation that is susceptible to null byte (`%00`) injection.
2. Create a malicious PHP file (`shell.php`) designed to execute commands passed via URL parameters (e.g., `cmd`, `ls`, `cat`).
3. Craft a `multipart/form-data` POST request where the filename includes a null byte before the authorized extension (e.g., `shell.php%00.jpg`). This causes the validation system to see `.jpg` while the underlying filesystem processes it as `.php`.
4. Upload the file and locate the directory where it was stored.
5. Access the uploaded file directly via its URL (without the `.jpg` extension) to execute the shell.
6. Use the shell to browse the directory structure, identify hidden directories (starting with `.`), and read the target file (`flag.txt`) to retrieve the flag.

## Conclusion
Learned how null byte injection can be used to bypass file upload validation and the critical importance of secure file handling and sanitization on the server side to prevent remote code execution.
