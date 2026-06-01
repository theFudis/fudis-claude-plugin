# Restaurant Analytics Terminology

Universal definitions for Fudis analytics metrics. Use when an operator asks what a metric means.

## RFM Segments

RFM classifies guests by three dimensions: **Recency** (when last visited), **Frequency** (how often they visit), **Monetary** (how much they spend).

| Segment | Who they are | What to do |
|---|---|---|
| **Champions** | Recent, frequent, high-spend | Reward loyalty, ask for referrals, early access to new dishes |
| **At-Risk** | Were frequent, now gone quiet | Win-back window — personalized outreach before they're lost |
| **Lost** | Long-absent, low probability of return | Last-attempt campaign; CLV determines if worth the effort |
| **One-Timers** | Visited once, never returned | Conversion focus — the first visit didn't close the loop |
| **New** | Recent first visit, not yet pattern-established | Nurture into repeat behavior quickly (critical 30-day window) |
| **Loyal** | Regular visitors, not top spenders | Upgrade path — move toward Champion tier |

## CLV — Customer Lifetime Value

Predicted total revenue from a guest over their expected relationship with the restaurant.
Calculated using BG/NBD (visit probability) + Gamma-Gamma (spend distribution).

- `predicted_clv_12m` — expected revenue in the next 12 months
- `p_alive` — probability this guest is still an active customer (0–1)
- `clv_segment` — high / medium / low tier

**Why it matters:** sorting by CLV tells you *who to call first* — a guest with high CLV and falling p_alive is your highest-priority win-back target.

## Churn

A guest is considered churned when `p_alive` drops below 0.3 — statistically unlikely to return.
Churn is not binary; it's a probability that increases with each passing week of absence.

Industry context: see `references/benchmarks.md` for regional churn rate norms.

## Campaign Triggers

Guests flagged by the system as being in an actionable state today:
- **Win-back window** — at-risk, still recoverable
- **Milestone** — anniversary, birthday, or visit count threshold
- **Post-first-visit** — visited once, now in the 7–30 day follow-up window

## Retention Rate

Percentage of guests who visited in a given period who return in the next equivalent period.
Higher is better. See `references/benchmarks.md` for regional baselines.

## Basket Affinity / Lift Score

How much more likely two items are to be ordered together vs. by chance.
Lift > 1.5 = meaningful pairing; lift > 2.5 = strong upsell opportunity.
