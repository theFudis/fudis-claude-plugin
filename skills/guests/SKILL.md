---
description: Look up a customer, check their history and value, or manage their profile (VIP status, notes, preferences). Use when the operator asks about a specific diner or wants to find a customer by name or phone.
---

Use $ARGUMENTS as the customer name or phone number to search.

Steps:
1. `search_customers` with the provided name/phone
2. If one clear match: `get_diner_profile` for full history, CLV, and segment
3. If multiple matches: present the list with RFM segment badges and ask which one
4. If no match: say so clearly and offer to search by different term

After showing the profile, offer the operator these actions:
- Mark/unmark as VIP (`set_diner_vip`)
- Add a note (`add_diner_note`)
- Add a preference (`add_diner_preference`)
- Opt out of marketing (`set_diner_marketing_opt_out`)

Show VIP badge, segment, lifetime value (in the restaurant's currency), and last visit date prominently.
