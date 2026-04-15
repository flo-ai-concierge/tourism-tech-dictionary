# API Proxy

## What it is
A middleman server that sits between an outside company and your real system. The proxy receives their requests, checks if they're allowed (e.g., read-only), and only forwards the safe ones to your actual data. The external party never touches your real API credentials.

## Tourism Translation
**"Like a hotel concierge desk — outside vendors can ask questions through the desk, but they never get the master key to walk the halls themselves."**

Your revenue management company needs to see reservation data. Instead of handing them the key to your entire property management system (where they could also cancel bookings, change prices, or read guest messages), you put a concierge desk in between. They ask the desk "show me last month's reservations" and the desk fetches it for them. If they ask "cancel reservation #5012" the desk says "not authorized" and blocks it. You also have a log of every question they asked.
