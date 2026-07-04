# Challenge: Hash - MD5

## Overview
- **Category:** CTF Training - Easy / Cryptanalysis
- **Points:** 50
- **Difficulty:** Very easy
- **Status:** Validated

## Description
Crack an MD5 hash.

## Solution
1. Identify the hash algorithm as MD5.
2. Use a password cracking tool like Hashcat (`-m 0`) or John the Ripper.
3. Perform a dictionary attack using a standard wordlist (e.g., `rockyou.txt`) to find the corresponding plaintext.

## Conclusion
Reinforced the understanding that MD5 is insecure due to its susceptibility to fast dictionary and brute-force attacks.
