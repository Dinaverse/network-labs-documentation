# Challenge: Discover - Capture 3

## Overview
- **Category:** Network
- **Points:** 40
- **Difficulty:** Hard
- **Status:** Validated

## Description
It's all about status.

## Solution
This challenge involves analyzing a network capture of authentication attempts to a web server.
1. Open the capture file and identify two HTTP exchanges to the `/login` endpoint.
2. Observe that the first attempt resulted in an HTTP `401 Unauthorized` status code, indicating a failed login with credentials `admin:not my password`.
3. Observe that the second attempt resulted in an HTTP `200 OK` status code, indicating a successful login.
4. Inspect the credentials sent in the successful request. Because the traffic is unencrypted (HTTP without TLS), the username and password are visible in plain text.
5. The password used in the successful attempt corresponds to the flag.

## Conclusion
Reinforced the understanding of HTTP status codes and the critical importance of using HTTPS (TLS) to encrypt credentials in transit, as unencrypted HTTP allows anyone with access to the network traffic to steal sensitive information.

## Flag
[REDACTED]
