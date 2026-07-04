# Challenge: File Inclusion - Wrappers

## Overview
- **Category:** CTF Training - Medium / Web
- **Points:** 400
- **Difficulty:** Medium
- **Status:** Validated

## Description
Identify and exploit a Local File Inclusion (LFI) vulnerability using PHP wrappers.

## Solution
1. Vulnerability Analysis: Identified an LFI vulnerability caused by insecure path concatenation: `include_once($lang . "/" . $breed . ".php");`.
2. Filter Bypass: The `lang` parameter was protected by a strict length filter (`strlen($lang) > 5`). By providing `lang=phar:`, I bypassed this restriction.
3. Payload: Created a ZIP file disguised as a `.jpg`, containing a PHP shell.
4. Execution: Triggered the shell using `?lang=phar:&breed=/contribute/uploads/[filename].jpg/shell`, which resolved to the correct path, allowing command execution.

## Conclusion
Learned how PHP wrappers like `phar://` can be used to bypass path validation filters, emphasizing the importance of secure path handling and input sanitization to prevent LFI.

## Flag
[REDACTED]
