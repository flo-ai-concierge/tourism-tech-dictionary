# Token Retry Pattern (Auth Recovery)

## What it is
When an API call fails because the authentication token has expired, automatically refresh the token and retry the request — instead of telling the user it failed.

## Tourism translation
Your hotel key card stops working at 2 AM. You go to the front desk. The old system: "Card expired, come back in the morning." The new system: front desk re-encodes your card on the spot and hands it back. Same door, same room, no interruption.

Token retry is the "re-encode on the spot" pattern. When the system's access key expires mid-operation, it gets a fresh key and retries automatically — the user never sees the failure.

## How it works
1. App tries to create a task in the property management system
2. PMS returns 401 (unauthorized) or 403 (forbidden) — token expired
3. App clears the cached token
4. App requests a new token from the auth server
5. App retries the original request with the fresh token
6. User sees success — never knew there was a problem

## When you'll encounter it
- Task creation fails at 8 AM because the overnight token expired
- API calls work fine for hours, then suddenly get 403 errors
- Operations that work manually but fail when scheduled/automated

## Real example
FLO's task creation failed with 403 for FLO 6 and FLO 12. The Hostaway OAuth token had expired. Without retry: FLO told the team "permissions issue — ask Pray." With retry: FLO refreshes the token and creates the task. Team never sees the error.

## Related concepts
- [Webhook](../apis/webhook.md) — another integration pattern
- [API Endpoint](../apis/api-endpoint.md) — where tokens are used
