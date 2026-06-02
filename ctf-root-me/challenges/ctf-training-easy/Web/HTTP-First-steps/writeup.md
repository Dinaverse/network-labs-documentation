# Challenge: HTTP - First steps

## Overview
- **Category:** CTF Training - Easy / Web
- **Points:** 50
- **Difficulty:** Very easy
- **Status:** Validated

## Description
Retrieve a flag by submitting data via an HTTP form that satisfies specific layout requirements.

## Solution
1. Reconnaissance: Inspect the index page to find requirements for displaying the flag (e.g., the words "pineapple" and "pizza" must be present, with at least 7 lines between them).
2. Identification: Notice that the form input (`"form": {}`) on the page is reflected in the server response.
3. Exploitation: Use `curl -X POST` to submit the data required by the layout rules. Include the word "pineapple" in one parameter, add at least 7 empty or filler parameters, and place "pizza" in the last parameter.
4. Access: The server processes the form data and reflects it in the response, satisfying the requirements and displaying the flag on the page.

## Conclusion
Learned how HTTP POST requests can be used to send arbitrary form data and how server-side reflection of user-supplied data can sometimes be exploited to control the output or satisfy conditions set by a challenge.
