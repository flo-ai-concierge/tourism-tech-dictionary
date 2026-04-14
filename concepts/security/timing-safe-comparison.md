# Timing-Safe Comparison (timingSafeEqual)

## What it is
A special way to compare two strings (like a webhook signature vs. the expected value) that takes the exact same amount of time regardless of how many characters match. Normal string comparison stops at the first mismatch — which means an attacker can measure response time to guess a secret one character at a time. Timing-safe comparison always checks every character.

## Tourism Translation
**"A front desk clerk who always takes exactly 10 seconds to verify an ID, whether it's obviously fake or almost perfect."**

If the clerk glanced at a clearly fake ID and said "no" in 1 second, but spent 8 seconds studying a nearly perfect fake, a con artist would learn "I'm getting closer" from the delay. The timing-safe clerk takes 10 seconds every time — so there's no feedback to exploit.

## Why it matters
This is a subtle but real attack called a "timing attack." In practice:
- Compare signatures with `crypto.timingSafeEqual()` in Node.js
- Never use `===` for secret comparison in security-critical code
- The time difference is milliseconds, but automated tools can detect it over thousands of attempts

## In simpler terms
It's like a poker player with a perfect poker face — no matter what cards they're dealt, their reaction time is identical. No tells.
