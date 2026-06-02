# Challenge: Hash - Rules

## Overview
- **Category:** CTF Training - Easy / Cryptanalysis
- **Points:** 100
- **Difficulty:** Very easy
- **Status:** Validated

## Description
Crack a modified hash by applying rule-based transformations.

## Solution
1. Identify the rules applied before hashing: reversing the string, appending a specific string, and inserting a character at a specific position.
2. Create a Hashcat rule file (`rules.rule`) that replicates these transformations (`r` for reverse, `$@...` for appending, `i5?` for inserting '?' at the 5th position).
3. Use Hashcat with the rule file to brute-force or match the provided hash from a list of potential flags.

## Conclusion
Learned to leverage Hashcat's powerful rule-based engine to handle complex hash transformations, a critical skill for cracking modified or salted hashes.
