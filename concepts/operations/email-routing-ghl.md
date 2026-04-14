# Email Routing (GHL / Google Workspace)

## What it is
The chain of settings that control where outbound emails come FROM, where replies go TO, and who gets hidden copies (BCC). In GHL, this includes: From Address (who sends), Reply-To (where replies land), Forwarding Address (where copies go), and BCC (silent copies to additional inboxes). When emails mysteriously appear in an inbox that isn't configured anywhere in GHL, the leak is usually at the Google Workspace level — routing rules, Google Groups, or account-level forwarding.

## Tourism Translation
**Like a hotel's mail sorting room.** The front desk sends a letter to a guest (From: Front Desk). The letter says "reply to: Reservations" (Reply-To). A copy goes to the General Manager (BCC). But if the mail sorting room has a rule that says "copy everything to the Concierge too" — the concierge gets mail nobody intended. To find the leak, you check the sorting room rules (Google Workspace Admin → Routing), not just the front desk settings (GHL Email Services).

## Key components
- **From Address**: The sender shown to the recipient (e.g., info@goflohom.com)
- **Reply-To Address**: Where responses go when the recipient hits Reply (e.g., reservations@flohom.com)
- **Forwarding Address**: Gets a copy of all replies in GHL's conversation view AND in their personal inbox
- **BCC**: Gets a hidden copy of every outgoing email — recipients never see these addresses
- **Google Workspace Routing**: Admin-level rules that can copy/redirect mail before it reaches anyone's inbox — operates independently of GHL

## Debugging steps
1. Check GHL Email Services (Reply & Forward Settings, all tabs)
2. Check GHL Workflows for any email forwarding actions
3. Check Google Admin Console → Gmail → Routing for server-level rules
4. Check if the mystery address is a Google Group member
5. Check the mystery address's own Gmail forwarding/filter settings

## Related concepts
- Webhook — inbound event notifications (similar concept, different medium)
- Kill switch — environment gates for email features
