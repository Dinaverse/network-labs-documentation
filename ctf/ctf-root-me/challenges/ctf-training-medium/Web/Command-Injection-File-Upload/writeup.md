# Challenge: Command Injection - File Upload

## Overview
- **Category:** CTF Training - Medium / Web
- **Points:** 250
- **Difficulty:** Easy
- **Status:** Validated

## Description
Exploit a command injection vulnerability triggered during file upload by injecting malicious commands into a filename.

## Solution
1. Reconnaissance: Observe that the web application processes uploaded `.zip` files and returns both `stdout` and `stderr` from the server-side command execution.
2. Hypothesis: The server is likely executing a system `unzip` command, embedding the uploaded filename directly into the shell command string without proper sanitization.
3. Exploitation: Use the `;` (semicolon) instruction separator to chain malicious commands to the expected `unzip` command. 
   - Create an archive with a crafted name: `zip "file.zip;ls;cat flag.txt" file.txt file2.txt`.
4. Execution: Upload the crafted ZIP file. The server executes the `unzip` command followed by the injected commands (`ls` to list files, then `cat flag.txt` to read the flag).
5. Flag Retrieval: Analyze the `stdout` of the response to locate the contents of `flag.txt`.

## Conclusion
Learned that system commands must never execute using unsanitized user input (like filenames). This challenge highlights the critical vulnerability of command injection when input is directly embedded into shell commands, emphasizing the need for robust input validation, command argument escaping, or alternative APIs that do not invoke the shell.

## Flag
[REDACTED]
