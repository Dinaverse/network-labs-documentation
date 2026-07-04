# Challenge: SQL Injection - File Read

## Overview
- **Category:** CTF Training - Hard / Web
- **Points:** 450
- **Difficulty:** Medium
- **Status:** Validated

## Description
Perform an SQL injection to read sensitive files from the server.

## Solution
1. **Reconnaissance:** Identified a film catalog application vulnerable to SQL injection through the `/movie/<movie_name>` endpoint.
2. **Injection Detection:** Confirmed the vulnerability by injecting a single quote (`'`), which resulted in a server error.
3. **Filter Bypass:** Discovered that keywords like `OR` and `--` were filtered. Bypassed this using alternative SQL comment syntax (`#` encoded as `%23`) and `UNION ALL` instead of just `UNION`.
4. **Vulnerability Exploitation:** Determined the correct number of columns (3) and successfully executed a `UNION` injection to exfiltrate data.
5. **File Exfiltration:** Used the `load_file()` function to read local files (like `app.py`). To bypass URL-based path issues and character length limitations, the file path was converted to hexadecimal.
6. **Flag Retrieval:** Analyzed the application source code (`app.py`) to find the path to `flag.txt` and used the shortened injection payload to read it directly.

## Conclusion
Learned sophisticated SQL injection techniques, including bypassing keyword filters using alternative syntax, using hexadecimal encoding to overcome path character issues, and exploiting `load_file()` for server-side file exfiltration.

## Flag
[REDACTED]
