# Challenge: Discover - Javascript

## Overview
- **Category:** Programming
- **Points:** 30
- **Difficulty:** Medium
- **Status:** Validated

## Description
Talking about arrays.

## Solution
This challenge can be solved using either static analysis or dynamic execution to retrieve a hidden string constructed from an array.

### Static Analysis
1. Analyze the provided JavaScript code without executing it.
2. Identify the key components:
   - A `secret` variable initialized with a string.
   - An `alphabet` constant containing an array of characters (letters, numbers, and symbols).
   - An `index` constant containing an array of integers.
   - A `for` loop that iterates through the `index` array.
3. Observe the logic: In each iteration, the character at `alphabet[index[i]]` is appended to the `secret` variable.
4. Manually map the integers in the `index` array to their corresponding characters in the `alphabet` array to reconstruct the flag (e.g., `alphabet[43]` -> "R", `alphabet[38]` -> "M", etc.).

### Dynamic Execution
1. Use a JavaScript interpreter or the browser's developer console (F12 -> "Console" tab) to run the code.
2. Paste the provided script into the console.
3. Add a display instruction, such as `console.log(secret);`, after the loop completes to print the final value of the `secret` variable.
4. The console will output the reconstructed flag instantly.

## Conclusion
Learned the difference between static and dynamic code analysis. While static analysis is safer and builds a deeper understanding of logic, dynamic execution is often faster for retrieving results from obfuscated or algorithmic string construction.

## Flag
[REDACTED]
