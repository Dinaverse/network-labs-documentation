# Challenge: Discover - Capture 1

## Overview
- **Category:** Network
- **Points:** 30
- **Difficulty:** Medium
- **Status:** Validated

## Description
Let's do some networking.

## Solution
The challenge provides a network capture file which needs to be analyzed to find sensitive information.
1. Open the provided `PCAPNG` file using a network packet analyzer like **Wireshark**.
2. Inspect the captured traffic, specifically looking for unencrypted protocols like HTTP.
3. Identify an HTTP `GET` request and its corresponding response.
4. Locate the request to the `/flag.txt` endpoint.
5. Examine the body of the HTTP response for this request to reveal the flag.

## Conclusion
Learned the basics of network traffic analysis using Wireshark and the risks of transmitting sensitive data over unencrypted HTTP.

## Flag
[REDACTED]
