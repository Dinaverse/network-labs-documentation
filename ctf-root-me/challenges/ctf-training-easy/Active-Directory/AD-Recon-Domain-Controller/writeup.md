# Challenge: AD Recon - Domain Controller

## Overview
- **Category:** CTF Training - Easy / Active Directory
- **Points:** 100
- **Difficulty:** Very easy
- **Status:** Validated

## Description
Perform basic domain controller reconnaissance.

## Solution
1. Identify the domain using discovery tools (`ROOTME.LOCAL`).
2. Scan for services allowing anonymous connections (`WIN-SRV02`).
3. Check domain policies for weak configurations (minimum password length 6).
4. Identify active protocols (detected SMBv1).
5. Enumerate domain controllers (`WIN-DC01` and `WIN-DC02`).
6. Concatenate the findings in the specified order to form the flag.

## Conclusion
Learned fundamental Active Directory reconnaissance techniques to gather information about domains, policies, and infrastructure.
