# Scoped API Token

## What it is
An API key that is restricted to only certain permissions — for example, read-only access instead of full read/write. Scoped tokens let you give external partners just enough access to do their job, without exposing your entire system. Not all platforms support this (Hostaway, for example, only has one all-or-nothing token).

## Tourism Translation
**"Like giving a cleaning crew a key that opens guest rooms but not the safe, the office, or the cash register."**

When you hire a third-party cleaning company, you don't give them the GM's master key that opens every door in the hotel — the vault, the accounting office, the security room. You give them a scoped key: it opens the rooms they need to clean, and nothing else. If the platform doesn't support scoped keys (like Hostaway), you have to build your own restriction layer — an API proxy — to enforce the limits yourself.
