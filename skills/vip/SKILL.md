---
description: VIP guest management. Use when the operator wants to see all their VIP guests, identify VIPs who are going cold, manage VIP status for a guest, or prepare for an upcoming VIP visit. Different from /fudis:clientes which looks up one guest at a time.
---

Use $ARGUMENTS to focus: "cold" (cold VIPs only), "upcoming" (upcoming VIP reservations), "manage [name]" (manage one guest's VIP status), or leave empty for the full VIP view.

**Full view:** call `customer_clv` (filter VIP-flagged) + `list_bookings` (this week) + `campaign_triggers` (VIPs in at-risk window) in parallel.

Present three sections:
- **Upcoming VIP visits** — VIPs with reservations this week: name, date/time, party size, notes on file. Add a note to review their profile before service.
- **Cooling VIPs** ⚠️ — VIPs with no visit in 30+ days, sorted by CLV: name, last visit, CLV in S/, one personal outreach line. These deserve a call or personal WhatsApp — not a broadcast.
- **Active VIPs** — visited in last 30 days: name, last visit, CLV

Close with the VIP tier summary: total, active, cold, upcoming this week, and estimated combined annual value in S/.

**For managing status:** `search_customers` to find the guest, then `set_diner_vip` to flag/unflag. Show the change as before → after.
