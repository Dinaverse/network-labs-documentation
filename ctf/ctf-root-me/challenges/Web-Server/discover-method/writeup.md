# Challenge: Discover - Method

## Overview
- **Category:** Web Server
- **Points:** 30
- **Difficulty:** Medium
- **Status:** Validated

## Description
HTTP methods are "commands" used in the HTTP protocol to specify the action desired by the client on a particular resource on the server. The server behaves differently depending on the method used.

## Solution
1. Use the `OPTIONS` method to query the server and identify the allowed HTTP methods for the resource.
   ```http
   OPTIONS / HTTP/1.1
   Host: <HOST>
   ```
2. Inspect the `Allow` header in the server's response to see which methods are supported (e.g., `GET, POST, OPTIONS, HEAD`).
3. Modify the HTTP request to use a different allowed method, such as `POST`, to see how the server responds.
   ```http
   POST / HTTP/1.1
   Host: <HOST>
   ```
4. Examine the server's response body. In this case, switching to `POST` revealed the hidden message.

*Screenshot Reference: Screenshot_20260529_231003.png*

## Conclusion
Learned how to use the `OPTIONS` method to discover supported HTTP methods on a server and how changing the request method can sometimes alter the server's behavior to reveal hidden information.
