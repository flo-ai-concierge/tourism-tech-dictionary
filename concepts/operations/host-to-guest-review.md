# Host-to-Guest Review

## What it is
The review the host writes about the guest after their stay, separate and opposite from the guest's review of the host. On Airbnb, both sides have 14 days after checkout to submit a review. Hosts rate communication, cleanliness, and adherence to house rules.

## Tourism Translation
**"The private note the front desk writes in the PMS about a guest after they check out."**

Guest checks out. Front desk logs a short internal note: "quiet, polite, left hot tub messy." That note follows the guest's profile forever. The next time they book anywhere in your property management system, the new front desk sees the history and knows what to expect.

Airbnb's host-to-guest review is the public version of that note. Other hosts see it when this guest tries to book their place in the future. It's how the Airbnb community protects itself from bad guests — and how good guests build a reputation for getting easy approvals.

## Why it matters

### Blank reviews are a red flag
If a guest has 10 stays and every host left them a blank or generic review, something's off. Either hosts were too scared to be honest, or the guest's behavior was forgettable in a way that says something. Thoughtful host reviews help other hosts make better decisions.

### Hostaway pre-creates a placeholder
For every completed reservation, Hostaway auto-creates a "host-to-guest" review record with empty text and null rating. It sits there waiting for the host to fill in within 14 days. If nobody does, Airbnb eventually auto-submits a default "no review" on your behalf.

### FLOHOM's auto-template was generic
Brian had Hostaway's built-in auto-review template enabled, producing the same line for every guest: "{Name} was a pleasure to host! We'd welcome them back anytime and we highly recommend them to other hosts." That's fine, but it's the same message no matter how the stay went.

### The FLO Bridge workflow replaces it with personalized reviews
The new `/admin/host-reviews` page lists every pending host-to-guest review. Click one → FLO drafts a personalized 1-3 sentence review using:
- Reservation dates and property
- Message history with the guest
- The guest's own review of us (as a sentiment signal)
- Any tasks or incidents logged during their stay

FLO also suggests a star rating and flags guests with major issues (damage, rule violations) for manual review instead of auto-positive text. Team edits, copies, pastes into Hostaway or Airbnb manually, then marks as sent.

### Why FLO can't submit it directly
Hostaway's public API doesn't expose endpoints for writing reviews. We verified this by probing every plausible POST/PUT path — all 404'd. So the team still has to click through to submit. FLO Bridge just removes the writer's-block and makes the review specific.

## In simpler terms
It's a letter of reference a hotel writes about the guest, not from the guest. Helps the next hotel decide whether to welcome them with open arms or watch them carefully.
