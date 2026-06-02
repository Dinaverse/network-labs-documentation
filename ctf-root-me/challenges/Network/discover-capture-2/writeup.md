# Challenge: Discover - Capture 2

## Overview
- **Category:** Network
- **Points:** 40
- **Difficulty:** Hard
- **Status:** Validated

## Description
This challenge involves analyzing a network capture containing numerous HTTP requests. The objective is to identify a hidden pattern within the traffic.

## Solution
1. Upon analyzing the network capture, notice that a series of HTTP `GET` requests are made to different URL paths.
2. Isolate the path component from each `GET` request.
3. Observe that these paths represent individual characters.
4. Note that some characters are URL-encoded (e.g., `%7B`, `%3C`). Decode them:
   - `%7B` = `{`
   - `%7D` = `}`
   - `%3C` = `<`
5. Concatenate the decoded characters in order to reconstruct the flag.

*Screenshot Reference: Screenshot_20260529_231119.png*

## Conclusion
Learned how to extract information hidden within the URL paths of HTTP traffic and the importance of recognizing URL encoding when performing network forensics.
