# Challenge: File Upload - Polyglot

## Overview
- **Category:** CTF Training - Hard / Web
- **Points:** 450
- **Difficulty:** Medium
- **Status:** Validated

## Description
Bypass strict file upload validation using a polyglot file to achieve Local File Inclusion (LFI) and Remote Code Execution (RCE).

## Solution
1. **Reconnaissance:** Identified an LFI vulnerability where the `lang` parameter is passed to `include_once("phar://$lang.php")`, utilizing the `phar://` wrapper.
2. **Analysis:** Determined that the application enforces both file extension and MIME-type checks, preventing direct `.phar` file uploads.
3. **Exploitation (Polyglot Creation):**
   - Created a malicious PHAR archive containing a PHP web shell.
   - Used `Phar::setStub` to prepend a valid JPEG header (`\xFF\xD8\xFF\xD9`) to the PHAR archive, tricking the server into classifying it as an image.
   - Renamed the file to `.jpg` to bypass extension filters.
4. **Execution:** Uploaded the polyglot file. Once uploaded, accessed the web shell via LFI by referencing the uploaded file path through the vulnerable `lang` parameter (e.g., `/?lang=.../exploit.jpg/shell&cmd=...`).
5. **Flag Retrieval:** Used the shell to navigate hidden directories, identify the flag file (`flag.txt`), and read its contents.

## Conclusion
Learned that file type validation based on simple extension or MIME-type checks is insufficient. A "polyglot" file can masquerade as one type to bypass security while remaining valid as another to be exploited. This emphasizes the need for deep content analysis and secure path management to prevent LFI/RCE.

## Flag
[REDACTED]
