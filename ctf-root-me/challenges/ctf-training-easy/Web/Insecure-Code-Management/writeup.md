# Challenge: Insecure Code Management

## Overview
- **Category:** CTF Training - Easy / Web
- **Points:** 250
- **Difficulty:** Easy
- **Status:** Validated

## Description
Modernize an internal corporate homepage by finding files left behind by the development team.

## Solution
1. Reconnaissance: Identify the admin login portal (`/admin.php`).
2. Enumeration: Use a directory brute-force tool like `ffuf` to discover hidden files and directories. The scan reveals a publicly accessible `.git` directory.
3. Exploitation: Use `git-dumper` to download the entire contents of the `.git` repository, allowing local reconstruction of the project's source code and version history.
4. Analysis: Explore the Git commit history using `git log` and inspect sensitive files (like `TODO.txt` and `admin.php`) revealed in the codebase.
5. Credential Retrieval: Locate hardcoded administrator credentials within the source code of `admin.php`.
6. Access: Use the retrieved credentials to log in to the admin portal and access the flag.

## Conclusion
Learned the severe security risks associated with exposing version control repositories (like `.git`) to the public, as they provide attackers with the full project source code, including sensitive logic and hardcoded secrets.
