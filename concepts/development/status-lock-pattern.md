# Status Lock Pattern

## What it is
A software pattern where a manual decision by a human is protected from being overwritten by automated processes. When an admin manually sets a status (like marking a conversation "Done"), a lock flag is set so that background jobs or scheduled tasks can't reset it. The lock is released when a new event legitimately requires the status to change (like a new incoming message).

## Tourism Translation
**A "Do Not Disturb" sign for task status.** When a hotel manager personally marks a room issue as resolved, you don't want the automated housekeeping system to reopen the ticket just because it sees the room hasn't been cleaned yet — the manager already handled it differently. The lock is the digital equivalent of a DND sign. But if the guest calls with a new complaint, the sign comes off and the ticket reopens.
