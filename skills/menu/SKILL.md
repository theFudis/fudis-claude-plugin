---
description: Menu intelligence. Use when the operator asks which dishes sell best, which to cut or promote, what gets ordered together, or wants a full menu engineering breakdown (stars, plowhorses, puzzles, dogs).
---

Use $ARGUMENTS to focus: "engineering" (engineering only), "affinity" (basket pairs only), "performance" (sales only), or a dish name to search. Defaults to the full report.

**Full report:** call `menu_engineering` + `basket_affinity` + `get_menu_performance` in parallel.

Present four sections:
- **Engineering** — quadrant counts with top 3 items per quadrant and one-line action per quadrant (protect Stars, reprice Plowhorses, push Puzzles, cut Dogs)
- **Top combos** — top 3 basket pairs with lift score and upsell angle
- **Dead items** — zero sales in 30+ days: list by name, no justification needed
- **One action** — single most impactful recommendation this week

Be direct. Operators need to know what to do, not get a lecture.

**For item search:** call `search_menu_items` with $ARGUMENTS and show name, price, allergens, dietary flags.
