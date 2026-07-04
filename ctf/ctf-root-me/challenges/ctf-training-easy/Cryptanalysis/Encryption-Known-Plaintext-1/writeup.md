# Challenge: Encryption - Known Plaintext 1

## Overview
- **Category:** CTF Training - Easy / Cryptanalysis
- **Points:** 200
- **Difficulty:** Easy
- **Status:** Validated

## Description
Perform a known-plaintext attack on an XOR-encrypted PNG file.

## Solution
1. Identify the encryption type as XOR and note the key length (8 bytes).
2. Leverage the known structure of PNG files (the first 8 bytes are the magic bytes: `\x89\x50\x4e\x47\x0d\x0a\x1a\x0a`).
3. Calculate the XOR key by XORing the known magic bytes with the corresponding 8 bytes of the encrypted file.
4. Apply the derived key to decrypt the entire file using the XOR function.

## Conclusion
Learned how to perform a known-plaintext attack against XOR encryption when the file format is known, highlighting the insecurity of using weak keys or fixed patterns in XOR ciphering.
