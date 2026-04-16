# Bearer Token Auth

## What it is
An authentication method where you send "Bearer {key}" in the HTTP Authorization header. Some APIs require the "Bearer " prefix, others use the raw key directly. Using the wrong format causes silent auth failures — the API rejects you with no helpful error.

## Tourism translation
Like a hotel key card — some doors need you to tap AND turn the handle, others just tap. Use the wrong combo and the door won't open, but it won't tell you why. You'll just stand there thinking it's broken.

## When you'd see it
- Connecting to any third-party API (payment processors, messaging platforms, CRMs)
- OpenPhone/QUO uses raw key auth, while GoHighLevel uses Bearer token auth
- Getting 401 Unauthorized errors that seem unexplainable

## Learned from
QUO (OpenPhone) SMS sync broke on Apr 15, 2026 when Bearer prefix was incorrectly added. The API silently returned empty results for 24+ hours.
