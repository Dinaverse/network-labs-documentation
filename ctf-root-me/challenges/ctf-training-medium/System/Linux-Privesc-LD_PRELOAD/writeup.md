# Challenge: Linux Privesc - LD_PRELOAD

## Overview
- **Category:** CTF Training - Medium / System
- **Points:** 300
- **Difficulty:** Medium
- **Status:** Validated

## Description
Escalate privileges by exploiting an insecure sudo configuration involving `LD_PRELOAD`.

## Solution
1. **Reconnaissance:** Identify the sudo configuration using `sudo -l`. Discovered that the `LD_PRELOAD` environment variable is preserved (`env_keep+=LD_PRELOAD`) and that the user can execute `/usr/bin/ls` as root without a password.
2. **Vulnerability:** The combination of `env_keep+=LD_PRELOAD` in sudoers and allowed root command execution allows an attacker to preload a malicious shared library into the address space of a root-privileged process.
3. **Exploitation:**
   - Create a C file (`shell.c`) with a `_init()` constructor function that sets UID/GID to 0 (root) and executes `/bin/sh`.
   - Compile this into a shared object file (`shell.so`) using `gcc -fPIC -shared -o shell.so shell.c -nostartfiles`.
   - Execute the permitted command with the library preloaded: `sudo LD_PRELOAD=/path/to/shell.so /usr/bin/ls`.
4. **Access:** The `_init()` function executes before the `ls` command, spawning a root shell.

## Conclusion
Learned that `LD_PRELOAD` can be exploited to hijack execution flow if a privileged binary allows it to be preserved. This underscores the importance of the principle of least privilege in sudo configurations and strictly restricting dangerous environment variable inheritance.

## Flag
[REDACTED]
