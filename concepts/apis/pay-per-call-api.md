# Pay-Per-Call API

## What it is
A pricing model where you pay a small fixed amount for each individual API request, instead of a flat monthly subscription fee. You only pay when you actually use it.

## Plain English
Like a pay-per-use laundry machine instead of a gym membership. You load credits upfront, and each time your code calls the API to get data, a small amount is deducted. If you don't use it one month, you don't pay anything. If you use it a lot, you pay more — but usually still less than a locked-in subscription.

## Tourism Analogy
Like a taxi vs. a monthly car lease. A taxi (pay-per-call) charges per ride — perfect if you travel occasionally. A lease (subscription API) charges every month whether you use the car or not — better if you need it daily. For FLOHOM's Market Navigator, which runs reports occasionally rather than constantly, pay-per-call wins.

## Real example (AirROI API)
- Market data lookup: $0.01/call
- Full market metrics (ADR, occupancy, RevPAR, listings): $0.25/call
- At 20 market reports/month: ~$5 total
- Minimum load: $10. No contract. No sales call. Cancel anytime.

## Contrast with subscription APIs
AirDNA's API requires a sales call and custom pricing — estimated $1,500–$3,000/yr for the same data. Pay-per-call eliminates that barrier entirely.

## Learned from
AirROI API research for Market Navigator integration, May 13, 2026
