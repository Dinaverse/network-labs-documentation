# Challenge: Discover - Console 2

## Overview
- **Category:** Web Client
- **Points:** 30
- **Difficulty:** Medium
- **Status:** Validated

## Description
Analyze HTTP/HTTPS requests sent by the web page to uncover hidden information.

## Solution
1. Open the browser's developer console (F12 or right-click -> "Inspect").
2. Navigate to the "Network" tab.
3. Refresh the webpage to capture all outgoing requests.
4. Filter or search for requests leading to a `/secret` path.
5. Inspect the response body of the identified request to find the flag.

*Screenshot Reference: Screenshot_20260529_231312.png*

## Conclusion
Learned to use browser developer tools to monitor network traffic, enabling the identification of hidden requests and sensitive data exposed in server responses.
