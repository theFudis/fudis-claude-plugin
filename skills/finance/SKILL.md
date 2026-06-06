---
description: Restaurant financial analysis — margin health, P&L modeling, cost benchmarks, and revenue risk. Adapts to your restaurant type (pollería, cevichería, bar hybrid, ghost kitchen, or multi-location group). Use when the operator asks about profitability, food cost, labor efficiency, delivery margins, or wants to model a P&L.
---

Use $ARGUMENTS to set the mode and optional context:
- `overview` — financial health snapshot across all available data
- `margin` — menu contribution margin deep-dive (which items earn, which cost you)
- `pnl` — model a full P&L (requires operator to supply labor % and fixed costs)
- `forecast` — revenue outlook with margin and risk implications
- `risk` — flag prime cost pressure, cost variance, and delivery fee drag

If no mode given, run `overview`.

---

### Step 0 — Category intake (always first)

If the restaurant category is not already known from context, ask before pulling data:

> "Before I run the numbers — what type of restaurant is this? So I can use the right benchmarks.
> *Pollería / criollo / casual · Cevichería · Bar or pisco bar · Delivery / ghost kitchen · Multi-location group · Fine dining*"

Once category is confirmed, load the matching section from `references/restaurant-finance.md` (or `references/fine-dining-cfo.md` for fine dining). This determines which benchmarks apply, which metric is primary, and what questions to ask for modeled inputs.

---

### Mode: `overview`

Pull in parallel: `get_menu_performance` + `revenue_trends` + `customer_segments` + `customer_clv`

Present in four blocks:

**Revenue** — total period revenue in S/, trend direction vs prior period, best and worst day.

**Menu margin** — top 3 earners by contribution margin (S/ per item × volume); flag any item where revenue rank and margin rank diverge by >3 positions (volume leader with poor margin = strategic risk).

**Customer value** — Champion count + avg CLV; At-Risk count + revenue at stake (guests × avg CLV). One-liners only.

**Benchmark gap** — compare food cost % against the category benchmark from `references/restaurant-finance.md`. State clearly if it's real (from RMS cost cards) or estimated (32% flat default). Flag if food cost is above the category ceiling.

Close with one line: the single most important financial lever right now and why.

---

### Mode: `margin`

Pull in parallel: `menu_engineering` + `get_menu_performance`

This is Kasavana-Smith applied to the operator's actual data. Present:

**Quadrant summary** — Stars / Plowhorses / Puzzles / Dogs with counts and total revenue share.

**Top 5 margin opportunities** — items where a S/5–10 reprice, bundle, or push would have the largest margin impact. Each opportunity: current price · current margin % · proposed action · estimated monthly revenue impact in S/.

**Bottom 3 margin risks** — Plowhorses with highest sales volume but below-category food cost %. These are the items dragging the average down.

**Category note** — for bar hybrids: surface beverages separately. Ask if beverage cost data is available; if not, note that beverage margin analysis requires actual pour cost input.

Data rule: if cost cards are missing for > 30% of items, state this clearly and note that the 32% flat default understates actual variance between items.

---

### Mode: `pnl`

This mode builds a P&L overlay. Fudis provides revenue and estimated food cost. The operator must provide the rest.

Ask for the inputs not yet known:
1. **Labor %** — total wages + benefits + EsSalud as % of revenue (remind: informal labor = underreported; real burden typically 25–30%)
2. **Rent** — monthly fixed in S/
3. **Other fixed costs** — utilities, insurance, equipment (monthly S/)
4. **Delivery mix** — if any sales are through Rappi/PedidosYa, what % and which platform (for commission adjustment)

Once inputs are provided, compute and present:

```
Revenue (period)                S/ [X]
  IGV-adjusted revenue          S/ [X ÷ 1.18]         ← note if used
  Platform commission adj.      S/ [−X] if delivery    ← net revenue
Food cost                       S/ [X]   [%]
Labor                           S/ [X]   [%]
Prime cost                      S/ [X]   [%]
Rent                            S/ [X]   [%]
Other fixed                     S/ [X]   [%]
EBITDA                          S/ [X]   [%]
```

Compare prime cost against category benchmark. If prime cost > category ceiling, flag it in bold and identify which of food or labor is the problem.

Offer: "Want me to model what prime cost looks like if labor drops 2%?" (sensitivity table).

If operator won't provide inputs, offer to run with assumed ranges from the category benchmark and clearly label the output as a model, not an actuals report.

---

### Mode: `forecast`

Pull in parallel: `demand_forecast` + `revenue_trends`

Present:
- **30-day revenue outlook** — forecast total S/, peak demand dates, trough period
- **Margin implication** — if revenue drops X% vs current, what does that do to fixed cost coverage? (only if `pnl` inputs are already known)
- **Staffing signal** — high-demand dates = prime cost risk if labor not pre-scheduled. Low-demand dates = SPLH drops; assess over-staffing risk.
- **Top 3 dates** requiring an operational decision (inventory pre-order, booking caps, staffing spike)

---

### Mode: `risk`

Pull: `revenue_trends` + `menu_engineering` + `customer_segments` + `campaign_triggers`

Flag financial risks in priority order:

1. **Revenue risk** — trend direction; if declining, quantify: at current rate, monthly revenue shortfall in S/ vs prior period
2. **Food cost risk** — items above category benchmark ceiling; concentration risk (if top 3 items = > 60% of revenue, any one going wrong hurts badly)
3. **Customer concentration risk** — Champions as % of total revenue; if > 50%, churn risk from top 10 guests = S/ X at stake
4. **Delivery commission drag** (if applicable) — estimated commission cost per month based on delivery revenue mix
5. **At-Risk revenue** — segments × CLV as monthly revenue at risk from churn

Each risk: one line description + S/ impact estimate + mitigation in ≤ 10 words.

---

### Output rules (all modes)

- Every number in S/ (the restaurant's currency). Never convert to USD unless asked.
- Real data vs modeled: always state which. Never present a modeled number as fact.
- If food cost data is the 32% flat default, say so once at the top of the analysis — don't repeat on every line.
- Never compute prime cost or EBITDA without labor %. If not available, ask or offer to model with assumed range.
- IGV: if precision matters (pnl mode), adjust. For trend and margin analysis, gross revenue is fine.
- Close every mode with a max **3-item action list**: action · owner (operator vs Fudis tool) · timeline.
- For the `financial-analyst` agent: hand off the full context — category, inputs collected, data pulled — so the agent doesn't re-ask.
