# System Pill (UI Pattern)

## What it is
A centered, styled UI element in a chat/message thread that shows a non-message event — like a missed call, status change, or system notification. Visually distinct from actual messages (not a left/right bubble), typically rendered as a small rounded pill in the center of the timeline.

## Tourism translation
Like the timestamp cards in a hotel's guest communication log that say "Guest checked in at 3:00 PM" or "Maintenance visited Room 204" between actual message exchanges. They're not messages TO anyone — they're events that happened in the timeline.

## When you'd see it
- "Missed call" or "Incoming call (2m 25s)" markers in a conversation
- "Chat transferred to agent" notifications
- "Guest checked in" status updates in a messaging thread
- Any event that's informational, not conversational

## Implementation
Use `sender_type = 'system'` in the messages table. The UI detects this and renders a centered pill instead of a left/right chat bubble. Can be enhanced with icons (phone icon for calls).

## Learned from
Built call event pills for QUO integration on Apr 16, 2026. Missed calls, completed calls, and voicemail indicators all render as system pills with phone icons.
