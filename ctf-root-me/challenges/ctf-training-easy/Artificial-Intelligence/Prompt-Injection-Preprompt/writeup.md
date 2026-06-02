# Challenge: Prompt Injection - Preprompt

## Overview
- **Category:** CTF Training - Easy / Artificial Intelligence
- **Points:** 10
- **Difficulty:** Medium
- **Status:** Validated

## Description
Leak the AI's system prompt (preprompt) and use provided context to test limitations.

## Solution
1. Explicitly request the AI to reveal its system prompt (preprompt).
2. Use the revealed context to understand how the AI is configured.
3. Use the provided information (e.g., a "password") in a follow-up query to test how the AI handles restricted information when combined with specific contexts.

## Conclusion
Learned how to probe for system instructions and test AI limitations, highlighting the vulnerability of LLMs to prompt leaking.
