# Challenge: Discover - Secured data 2

## Overview
- **Category:** Steganography
- **Points:** 30
- **Difficulty:** Medium
- **Status:** Validated

## Description
Analyze image metadata to uncover hidden information.

## Solution
1. Understand that digital images can contain metadata (EXIF data) that stores information about the author, creation date, and more.
2. Use a metadata analysis tool, such as `ExifTool` or an online metadata viewer, to inspect the provided image (`donnees_securisees2.png`).
3. Examine the output fields, specifically looking for unusual or hidden information in fields like "Artist".
4. The flag was found within the "Artist" metadata field.

*Screenshot Reference: Screenshot_20260529_231444.png*

## Conclusion
Learned the importance of checking image metadata for sensitive or hidden data, demonstrating a simple but effective technique for steganography.
