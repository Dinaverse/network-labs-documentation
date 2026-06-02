# Challenge: Hash - Wordlist

## Overview
- **Category:** CTF Training - Easy / Cryptanalysis
- **Points:** 50
- **Difficulty:** Very easy
- **Status:** Validated

## Description
Crack a hash using a provided list of potential flags.

## Solution
1. Detect the hash algorithm (SHA-256 via auto-detection).
2. Perform a dictionary attack using Hashcat (`-m 1400`) against the provided list of potential flags (`flags.txt`) to find the matching plaintext.

## Conclusion
Learned the basic process of dictionary attacks to crack hashes when a list of potential candidates is available.
