# DB Session Injection (Test Bypass)

## What it is
A local development technique where you insert a valid login session directly into the database and then set the session cookie manually in the browser — bypassing the login form entirely. Used when you need to test authenticated pages but don't have (or don't want to use) a real password.

## Plain English
Instead of logging in the normal way, you create a fake-but-valid "I'm logged in" entry in the database, then tell the browser to use it. The app can't tell the difference — it sees a valid session and lets you in. Only works locally; never used in production.

## Tourism Analogy
**"Like a hotel inspector who gets a master key made at the key shop so they can audit rooms without going through the front desk check-in process."**

The front desk has a login procedure — name, ID, credit card. But the inspector needs to audit 30 rooms quickly without creating 30 real reservations. They get a master key made, walk in, do their job, and leave. The doors opened because the key was real — even though no guest registration happened.

## The pattern (PostgreSQL)
```sql
INSERT INTO admin_sessions (token, admin_user_id, email, name, role, expires_at)
SELECT 'test-session-abc123', id, email, name, role, NOW() + INTERVAL '1 hour'
FROM admin_users WHERE email = 'pray@flohom.com';
```
Then in the browser console:
```javascript
document.cookie = "admin_session=test-session-abc123; path=/";
window.location.reload();
```

## Safety rules
- Only use in local dev environment
- Always delete the test session when done: `DELETE FROM admin_sessions WHERE token = 'test-session-abc123'`
- Never insert test sessions into production DB
- Use a recognizable token name (e.g. `test-session-*`) so it's obvious what it is

## Learned from
May 14, 2026 — needed to test the AirROI badge on a local report page but the local dev server had no login credentials available. Injected a session directly, tested the badge, then deleted the session on cleanup.
