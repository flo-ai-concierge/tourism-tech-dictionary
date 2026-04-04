# Daily Schedule Classification (Turnover Logic)

## What it is
The logic that determines what type of cleaning/preparation each property needs on a given day, based on check-in and check-out data from the property management system.

## Tourism translation
Every morning, the housekeeping manager needs to know: which rooms need a full deep clean (guest leaving + guest arriving), which just need a checkout clean (guest leaving, nobody coming), and which just need a welcome setup (no checkout, guest arriving).

In vacation rentals, this is the daily schedule — sent to cleaners and ops teams so they know exactly what to do at each property.

## Classifications

| Label | Color | Meaning | Cleaning required? |
|-------|-------|---------|-------------------|
| TURNOVER | 🔴 Red | Guest checks out AND new guest checks in same day | Full turnover clean |
| TURNOVER (NO CHECK-IN) | 🟡 Yellow | Guest checks out, no new guest arriving yet | Full turnover clean (still required!) |
| CHECK-IN ONLY | 🟢 Green | New guest arriving, no checkout | No clean — welcome prep only |
| No Activity | ⚪ None | No check-in or check-out | Nothing needed |

## Critical lesson
"CHECK-OUT ONLY" was the original label, but cleaners interpreted it as less work than a "TURNOVER." In reality, ANY checkout requires a full turnover clean — whether or not a new guest is arriving. The label was changed to "TURNOVER (NO CHECK-IN)" so cleaners always know: checkout = full clean.

## Common bugs
- **Status filter too aggressive**: Property management systems have booking statuses like "new" (received but not processed by host). Filtering out "new" drops paid bookings from the schedule. Fix: only filter truly dead statuses (cancelled, declined, expired).
- **Stale data**: Local database may show old dates if a reservation was modified in the PMS. Use live API for real-time schedule, database for historical analysis.

## Related concepts
- [Turnover](turnover.md) — the physical cleaning process
- [Check-in/Check-out Boundaries](checkin-checkout-boundaries.md) — date handling
