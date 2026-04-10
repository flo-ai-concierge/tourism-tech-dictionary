# Bot Token vs User Token (Slack)

## What it is
Slack has two types of API tokens with different permission levels. A **bot token** (xoxb-) can read channels, post messages, and react — but cannot search message history. A **user token** (xoxp-) has full workspace access including the search.messages API, which does real full-text search across all channels and all history.

## Tourism Translation
**"A bellhop badge vs a general manager keycard."**

The bellhop badge lets you enter guest areas, carry luggage, and open common doors. But only the general manager's keycard opens every room, the archives, and the security office. If a guest asks "what happened in Room 14 last month?" — the bellhop can't help, but the GM can pull the records instantly.

## Why it matters
FLO's Slack search was using a bot token, which meant it couldn't use Slack's real search API. Instead, it faked search by reading the last 100 messages from each channel and doing substring matching — missing older messages entirely. Adding a user token (SLACK_USER_TOKEN) enabled real full-text search across all channels, all history. Travis's pump-out log from April 6 was finally findable.
