# ADR (Average Daily Rate)

## What it is
The average price a short-term rental or hotel charges per night, calculated across all bookings in a given period.

## Plain English
If you had 10 bookings at $200/night and 5 bookings at $300/night in a month, your ADR is $233. It tells you what guests are actually paying on average — not your listed price, but your realized price.

## Tourism Analogy
Like a hotel's average room rate. A resort might list rooms at $400 but after discounts, promotions, and slow-night deals, the actual ADR might be $310. That's what operators and investors care about.

## Why it matters
ADR is one of the three core STR performance metrics (with occupancy and RevPAR). It's used in underwriting to model how much a property will earn per night and to benchmark against competitor listings.

## How it's used in FLOHOM
Pulled from AirDNA exports (or AirROI API) and injected as grounding facts into the Market Navigator's Hotel & STR Comps and Underwriting criteria.

## Learned from
AirDNA → Market Navigator integration research, May 13, 2026
