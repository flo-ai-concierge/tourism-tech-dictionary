# Channel Override Reply (Cross-Channel Messaging)

## What it is
The ability to reply to a guest via a DIFFERENT channel than their original message came through. For example, a guest books via Airbnb (conversation lives in the Airbnb channel), but you want to send them an SMS via QUO/OpenPhone. The inbox shows a channel selector dropdown that lets you override the default reply channel. The backend routes the message through the correct API (Hostaway for Airbnb, QUO for SMS) based on your selection.

## Tourism Translation
**Like a hotel concierge who can reach a guest through multiple channels.** The guest originally emailed a question, but the concierge knows a text message will get a faster response — so they reply via text instead of email. The conversation history still shows both the email and the text in one unified thread, but the concierge picked the best channel for that specific reply.

## How it works
1. Guest messages via Airbnb → conversation shows "via Airbnb" as default reply channel
2. Admin opens the channel dropdown → sees: Airbnb, Email, SMS, SMS (QUO)
3. Admin selects "SMS (QUO)" → message is sent via OpenPhone to the guest's phone number
4. The sent message is stored in the same conversation with `channel_name: 'quo_sms'`
5. Guest's SMS reply comes back via QUO webhook → lands in the same conversation thread

## Requirements
- Guest must have a phone number on file (from the reservation)
- The system auto-picks the correct market-specific phone number (MD/VA/SC)
- If no phone number exists, the SMS option is hidden

## Related concepts
- Market-aware routing — selecting the right sender number by geography
- E.164 phone format — standardized phone number format for APIs
