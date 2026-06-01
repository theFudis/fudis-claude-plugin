---
description: Win-back campaign execution. Use when the operator wants to recover lapsed guests or needs ready-to-send WhatsApp messages for at-risk customers. Delivers a prioritized contact list with personalized message drafts, not just ideas.
---

Use $ARGUMENTS to filter by segment ("at-risk", "lost", "one-timers") or a guest name. Defaults to all win-back candidates today.

Call: `campaign_triggers` → `customer_clv` (cross-reference for CLV priority) → `get_diner_profile` for the top 5–10 candidates.

For each guest (max 10, sorted by CLV descending) present:
- Name, VIP flag, last visit, predicted CLV in S/, RFM segment
- Any preferences or notes on file
- A ready-to-send WhatsApp draft: conversational, warm, under 3 sentences, references their preferences or last visit if available — never sounds like a broadcast

Close with: total candidates, estimated revenue if 30% return (industry benchmark for personalized outreach vs. 8% for broadcast), and aggregate CLV at stake.

Message tone: sound like a person who remembers you, not a marketing tool.
