# Webhook Payload

## What it is
The actual data package a system sends when it fires a webhook notification. A payload can be complete (all available fields including attachments) or partial (only some fields like text, missing media). The receiving system can only work with what's in the payload — if fields are missing, that data is lost in transit.

## Tourism Translation
**The contents of a front desk handoff note.** When the night shift leaves a note for the morning shift about a guest issue, the note might say "Guest in Room 204 reported a leak — see attached photo." If the photo fell off the note, the morning shift only gets the text description. The payload is the note plus everything attached to it. A complete payload includes the photo; an incomplete one just has the words.
