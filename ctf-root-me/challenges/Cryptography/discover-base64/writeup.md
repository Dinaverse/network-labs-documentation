# Challenge: Discover - Base64

## Overview
- **Category:** Cryptography
- **Points:** 20
- **Difficulty:** Easy
- **Status:** Validated

## Description
We're repeating ourselves!

## Solution
1. Understand the principle of Base64 encoding, which represents data in a specific character set.
2. Use an online tool or a script to perform Base64 decoding on the provided string.
3. Observe that a single round of decoding results in a string that is still obfuscated or not clearly legible.
4. Recognize that the data has been encoded multiple times.
5. Apply Base64 decoding several times in succession to peel back the layers of encoding.
6. The final round of decoding reveals the plaintext flag.

## Conclusion
Learned about the common practice of multi-layered encoding and the importance of recognizing the structure of Base64 strings to determine when further decoding is necessary.

## Flag
[REDACTED]
