# Challenge: Encryption - Known Plaintext 2

## Overview
- **Category:** CTF Training - Medium / Cryptanalysis
- **Points:** 250
- **Difficulty:** Easy
- **Status:** Validated

## Description
Solve a repeating-key XOR cipher on a PDF file using a known-plaintext attack.

## Solution
1. Analysis: The challenge utilized a repeating-key XOR cipher on a PDF file.
2. Key Derivation: Leveraging the known PDF header structure (`%PDF` / Hex `25 50 44 46`), I derived the 5-byte XOR key.
3. Decryption: XORed the ciphertext with the derived key to recover the PDF document.
4. Flag: The flag was found within the PDF stream.

## Conclusion
Reinforced understanding of XOR ciphers and the effectiveness of known-plaintext attacks when the file structure is predictable.

## Flag
[REDACTED]
