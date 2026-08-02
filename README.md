# Flight Price Tracker

Tracks JFK ↔ LAX round-trip fares for a trip alongside my sister (outbound 2026-10-30, return 2026-11-02) and flags whether it's a good time to buy.

See [`flights/criteria.md`](flights/criteria.md) for the exact route/time/price rules the daily check follows, and [`flights/price_log.csv`](flights/price_log.csv) for the price history.

## How it works
A daily automated check (Claude Code Remote Routine) searches for nonstop JFK↔LAX flights matching the criteria, logs the cheapest qualifying price to `flights/price_log.csv`, commits the update to this branch, and sends a push notification with a BUY/WAIT recommendation.

- **BUY** signal: round-trip total ≤ $350
- **WAIT** signal: anything above that — current baseline (2026-08-02) is ~$397–407, so we're waiting for now.

To change the route, dates, time window, or price threshold, just edit `flights/criteria.md` — the daily check reads it fresh each run.
