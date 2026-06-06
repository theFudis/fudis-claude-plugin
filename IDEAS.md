# Fudis Plugin — Backlog & Ideas

Working notes for what to add next. Not a public commitment. Grounded in the
actual MCP surface (`mcp.fudis.app`) and backend data as of 2026-06-03.

---

## 0. Data reality check (read this first)

The plugin can only be as honest as the data. What Fudis actually has:

| Domain | Status | Source |
|---|---|---|
| Revenue (daily, trend, forecast) | **Real** | `revenue_trends`, `demand_forecast` |
| Average ticket / covers | **Real** | purchase history + bookings |
| Item revenue + menu mix | **Real** | `menu_engineering`, `get_menu_performance` |
| Item **contribution margin** | **Real where RMS cost known, else 32% flat assumption** | `menu_items.unit_cost` (Memmos `venta_prod_margen`); fallback `FOOD_COST_PCT = 0.32` |
| Channel mix (dine-in/delivery/…) | **Real** | `channel-breakdown` |
| Customer economics (CLV, RFM) | **Real** | `customer_clv`, `customer_segments` |
| Bookings, events, attendees | **Real** | bookings + events tools |
| **Labor cost, rent, overhead, full P&L** | **NOT IN FUDIS** | `pos` schema = Phase 3 TBD |

**Implication:** anything at or above *gross contribution* is real (modulo the 32%
fallback). Anything below it (labor %, fixed costs, net profit, break-even) must be
**operator-supplied and labeled "modeled."** Never invent a food-cost %, labor %, or
net margin. State whether each item's margin is RMS-real or the 32% proxy.

---

## 1. Financial analyst direction (priority — see §1 detail below)

A CFO-in-your-pocket built on the revenue + gross-contribution data, with an
optional operator cost overlay for modeled prime-cost / break-even.

> **Knowledge base is built:** `references/fine-dining-cfo.md` — the full luxury-
> restaurant CFO brain (formulas, fine-dining benchmark ranges, the weekly flash
> report, no-show/beverage/menu/labor economics, Danny-Meyer guest economics, Peru/IGV
> localization, and a real-vs-modeled Fudis data-boundary table). The `financial-analyst`
> agent loads this; `/fudis:finance` references the relevant sections. Sourced from a
> 2026-06-03 deep-research sweep (US benchmarks, Peru-localized).

### `/fudis:finance` skill (modes)
- `overview` — financial snapshot: revenue (period + trend), average ticket, covers,
  revenue per cover, forecast, **revenue concentration** (top items / customers /
  channel share — concentration = risk), channel mix.
- `margin` — gross-contribution view: item contribution margins + menu mix, prime
  earners, price realization. Flags which items use **real RMS cost** vs the **32%
  assumption** so the operator knows what to trust.
- `pnl` — **modeled** P&L: operator supplies food-cost % (or use RMS), labor %, fixed
  monthly costs → contribution margin → break-even covers/revenue + modeled net.
  Every modeled line labeled.
- `forecast` — forward revenue + peak/trough dates + the staffing/cash implications.
- `risk` — revenue at risk: churn-driven (CLV of at-risk segment), no-show lost
  revenue, and concentration risk (over-reliance on a few items/customers/one channel).

### `financial-analyst` agent (CFO persona, high effort)
Pulls revenue + CLV + forecast + menu margin + channel + bookings, optionally takes
cost assumptions, returns a CFO memo: where the money comes from, where it's
concentrated, what's at risk, the 3 highest-$ actions. Quantified, honest about
modeled vs actual.

### Backend dependencies this would want (flag, don't block on)
1. **Persistent finance assumptions** — somewhere to store an org's labor %, rent,
   fixed costs so `pnl` doesn't re-ask every time. (No table today.)
2. **Labor / scheduling data** — would upgrade `pnl` from modeled to real. (Phase 3+.)
3. `unit_cost` coverage is sparse outside RMS-synced restaurants → most orgs get the
   32% fallback. A "set your food-cost %" input closes this per-org.

---

## 2. Events → retention bridge (differentiated; uses tools we just shipped)
- **`events-producer` agent** — plan (`/event`) → put dates on sale → build invite
  list from own regulars/VIPs (`customer_segments` + `customer_clv` + `campaign_triggers`)
  → per-guest announcement (`message`) → day-of guest list + door check-in.
- **Post-event win-back** — `list_event_attendees` → tagged cohort → follow-up campaign.
- ⚠️ **Gap:** no `create_event` / `create_occurrence` MCP tool yet (only list/get/
  check-in/status). Full "launch an event by chatting" needs that backend add.

## 3. Outcome skills (chain existing tools, no backend work)
- **`/fudis:tonight`** — service snapshot: tonight's bookings + VIPs arriving + any
  event today + check-in readiness. (The 5pm pre-shift open.)
- **`/fudis:fill`** — slow-night rescue: `demand_forecast` flags a soft date →
  `campaign_triggers`/`clv` says who to call → drafts the messages.
- **`/fudis:invite`** — invite-list builder for an event/promo from segments/CLV with
  per-guest message drafts.

## 4. Tier 2 content skills (no account — top of funnel)
- **`/fudis:social`** — IG/WhatsApp post for a dish or event
- **`/fudis:holiday`** — plan a holiday / long weekend (demand + staffing + promo + msg)
- **`/fudis:staff`** — pre-shift staff briefing note

## 5. Plugin infrastructure / cleanup
- **`references/rendering.md`** — document the `_fudis_hint` component vocabulary
  (kpi_strip, badges, ranked_table, confirm_card…) so every skill renders consistently.
  The MCP sends hints; no skill documents them today.
- **Fix:** `agents/restaurant-ops.md` still hardcodes `S/` despite the v1.1.0
  currency-agnostic pass — bundle the fix.

---

## Suggested sequencing
1. `/fudis:finance` (overview + margin + risk) — real data, no backend dep, high value.
2. `financial-analyst` agent — composes the above into a CFO memo.
3. Decide on `pnl` modeled overlay + whether to add a finance-assumptions store.
4. Events-producer agent (+ decide on `create_event` MCP tool).
5. `/fudis:tonight`, then the Tier 2 funnel skills.
