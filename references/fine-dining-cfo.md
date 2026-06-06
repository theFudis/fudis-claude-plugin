# The Brain of a Luxury Restaurant CFO

Knowledge base for the `financial-analyst` agent and `/fudis:finance` skill. Loaded on
demand, not every session. Sourced from a 2026-06-03 research sweep (US-centric
benchmarks; Peru/LatAm localization at the end). Every benchmark here is a **range**,
not a target — judge a restaurant against its own trend first.

> **Honesty rule (non-negotiable):** Fudis has *revenue* and *partial food cost*, not
> labor/rent/overhead. Anything at or above **gross contribution** is real. Anything
> below it (labor %, fixed costs, net margin, break-even) is **modeled from operator
> inputs and must be labeled "modeled."** Never invent a food-cost %, labor %, or net
> margin. See §11 (Fudis data boundary).

---

## 1. The thesis — how a fine-dining CFO thinks

Fine dining runs the **lowest net margins of any format: ~2–5%** (QMK 2–4%; Sauce 2–5%;
evergreenhq 4–7%). Prestige ≠ profit. The cost base is heavy on all three big lines at
once: premium food cost, brigade labor, flagship rent. At 2–5% net there is almost no
error budget — **a single point of prime-cost drift can erase the year's profit.** That
fact drives everything below: the weekly cadence (§9), the obsession with prime cost
(§2), and the reliance on the regular guest (§10).

The structural escape valves are two:
1. **Beverage (esp. wine) is the profit center, not food.** Food is brand and traffic;
   the wine list pays the rent (§5).
2. **The regular guest is an annuity.** ~65% of business comes from the existing base;
   a 5% retention lift → 25–95% profit lift (§10). This is exactly where Fudis's CLV +
   diner CRM is a *margin* tool, not a marketing toy.

---

## 2. Prime cost — the single most important number

> **Prime Cost = COGS (food + beverage) + Total Labor** (fully loaded: wages + payroll
> tax + benefits)
> **Prime Cost % = Prime Cost ÷ Total Revenue**

| Band | Reading |
|---|---|
| 55–60% | well-run, healthy |
| 60–65% | full-service / fine-dining normal (target ceiling **<65%**) |
| >65% | margin is bleeding — investigate food, bev, or labor |

Leverage: **a 1% prime-cost improvement on $1M revenue = $10,000** straight to the
bottom line. Max acceptable blind spot: **7 days** — never go a week without knowing
prime cost. Fine dining sits at the *higher* end because food and labor are both
structurally high; judge it on absolute dollars + productivity, not % alone.

---

## 3. Food cost, COGS & variance

> **COGS = Beginning Inventory + Purchases − Ending Inventory**
> **Food Cost % = COGS ÷ Revenue**

- Normal **28–35%**; "good" 28–32%. Fine dining accepts **30–35%+** (premium inputs).
- **Beverage COGS is far lower (15–25%)** than food (30–40%) — a strong wine program
  pulls the *blended* cost down. Track food and beverage cost **separately**.

**Theoretical vs Actual vs Variance** (the CFO's waste detector):
> **Theoretical (ideal) food cost** = Σ(recipe cost × portions sold) — perfect world.
> **Actual food cost** = from inventory counts — includes waste/theft/over-portioning.
> **Variance % = (Actual − Theoretical) ÷ Revenue × 100**

| Variance | Reading |
|---|---|
| <2% | excellent (few sustain it) |
| 2–5% | acceptable for full-service; monitor |
| >5% | structural problem — investigate now |

Drivers, ranked: portioning drift → yield gaps → unrecorded waste (4–10% of purchases)
→ theft/staff meals → price creep not updated in recipes → counting errors →
overproduction. **Decision rules:** track variance at the *ingredient* level (a 4%
blended number hides salmon at 10%); sort by **dollar impact, not %** (15% on parsley is
noise; 4% on salmon is thousands); count high-value SKUs weekly. The AP-vs-EP trap:
cost recipes at *edible-portion* (yield-adjusted) price, not as-purchased — fixing this
alone yields 3–5% COGS improvement.

> **Yield %: (EP weight ÷ AP weight) × 100.** 10 lb − 2 lb trim = 8 lb → 80% yield → at
> ½-lb portions that's **16, not 20** portions. EP cost = ingredient cost ÷ usable
> portions = the true plate input.

---

## 4. The restaurant P&L (fine-dining % of revenue)

| Line | Definition | FD % of revenue |
|---|---|---|
| **Revenue** | food + beverage + other | 100% |
| − COGS | food 30–35%, beverage 15–25% | ~28–35% |
| **= Gross profit** | | **65–70%** |
| − Labor | fully loaded | 30–40% (FD high) |
| **= Prime cost** (COGS+labor) | controllable | **55–65%** |
| − Occupancy | rent + property tax + insurance | ~6–10% |
| − Operating/controllable | utilities, supplies, R&M, marketing, G&A | ~15–25% |
| **= EBITDA / 4-wall** | unit-level operating profit | **8–15%** |
| − D&A, interest, tax | | |
| **= Net profit** | | **2–7%** (FD) |

**4-wall EBITDA** = profit within the four walls *before* corporate G&A/interest/tax/
D&A — the truest unit-level health metric and what investors underwrite.

> **Contribution margin (per item) = Menu Price − Item Variable (food) Cost.** The dollars
> each dish contributes to fixed costs + profit. Engine of menu engineering (§6).
> **Break-even (covers) = Fixed Costs ÷ (Avg Revenue/Guest − Variable Cost/Guest)**
> **Break-even (sales $) = Fixed Costs ÷ Contribution-Margin Ratio**

---

## 5. Beverage / wine — the profit center

Food = 60–70% of revenue but beverage = **80%+ of gross-profit dollars** (SevenFifty).
Why: less spoilage, less prep labor, less variation. A server opens a bottle in 2 min;
10 cocktails take 10 min of skilled labor.

> **Pour cost % = Beverage COGS ÷ Beverage Sales.** A 20% pour cost = 80% margin.

| Category | Target pour cost |
|---|---|
| Total beverage program | 18–24% |
| Spirits | 15–20% |
| Wine (by bottle) | 30–40% (can run higher on premium) |
| Draft beer | 21–22% · Bottled 23–25% |
| Cocktails | ~20% (craft up to ~30%, balanced by volume drinks) |

**Markup conventions:** bottles 2.5–3× wholesale, but *graduated* — cheap bottles 3.5×,
$150+ bottles only 1.5–2× (protect gross-profit dollars without pricing out big spends).
**BTG:** charging ~the wholesale cost of the bottle for the first glass recovers the
bottle; ~5 pours/750ml. **CFO caveat: dollars go in the bank, not percentages** — accept
a higher COGS % on a bottle that contributes $100 gross profit over one that contributes
$40. Avoid price gaps on the list (an $80→$150 jump with nothing between makes guests
trade *down*, leaving $40 of gross revenue on the table). Beverage **attachment rate per
cover** is a top-watched KPI; pairing flights guarantee per-cover beverage spend.

---

## 6. Menu engineering (Kasavana–Smith) — Fudis already computes this

Two axes: **Contribution Margin** (vs menu average) × **Menu Mix %** (popularity vs
expected share; "high" ≈ ≥70% of fair share). *Gross profit trumps food cost %.*

| Quadrant | CM | Popularity | Action |
|---|---|---|---|
| **Star** | High | High | Protect. Hold/test small price ↑, feature as anchor, never cut quality. |
| **Plowhorse** | Low | High | Popular but thin. Modest price ↑, shrink portion / re-engineer recipe, bundle — carefully (price-sensitive). |
| **Puzzle** | High | Low | Profitable but under-ordered. Rename/reposition, add copy, move to sweet spot, server upsell, or lower price. |
| **Dog** | Low | Low | Remove or rework — unless it's a strategic anchor/decoy or dietary need. |

CFO move: migrate items *up-and-right* (Plowhorse→Star by lifting CM; Puzzle→Star by
lifting popularity). Re-cost recipes each time; re-engineer the menu ~2×/year, review
quarterly. **Pricing psychology:** drop currency symbols (`28`, not `$28.00` →
**+~8% spend**, Cornell/CIA 2009); anchor with a high-priced decoy near the target dish;
nest prices inline (no right-aligned price column → stops cheapest-scan); use sweet spots
(first/last in a category). **Prix-fixe/tasting** trades à-la-carte ceiling for
predictability + guaranteed beverage attachment (single high-CM path per cover,
predictable prep → lower variance).

---

## 7. Revenue management — the master equation

> **RevPASH = Total Revenue ÷ (Seats × Hours Open) = Seat Occupancy × Average Check**

The second form is the diagnostic: yield = **how full × how much each guest spends**.
No universal benchmark — it's self-relative; **segment by daypart/day-of-week** (Friday
dinner and Tuesday lunch are two different businesses). RevPASH beats occupancy: a full
room with slow turns + low checks can underperform a half-full room with quick turns +
high spend. **Staff to RevPASH, not covers** — a high-check night supports more labor
than a high-cover/low-check one.

- **PPA (per-person average) = Revenue ÷ covers.** Fine-dining ticket ~$75–$200+.
- **Table turns:** fine dining **1–1.5/night** (~2-hr seating) vs casual 2–3. This
  *structurally caps the occupancy term* — fine dining can't out-volume casual, so it
  must win on **check (PPA, beverage)** and **yield discipline (no empty/no-show seats)**.
- Levers to raise the check term: premium add-ons reframed as experience (one group
  +14% PPA), beverage attachment, menu engineering placement, right-sizing tables to
  party, peak-time minimum spend / premium-seat upcharges.
- **Revenue per sq ft:** FD $400–1,000+ (survival floor ~$200).

---

## 8. No-show economics — the biggest fine-dining yield leak

Low turns ⇒ a no-show seat is **gone for the night** (unrecoverable). At Alinea, two
no-shows can erase a night's profit. Rates: industry 5–20%; big-city ~20% ("1 in 5"); FD
**without** a deposit **25–30%**; prix-fixe **with** prepay **<5–8%**. *"That gap is
policy, not luck."*

| Mechanism | Avg no-show (Tock) |
|---|---|
| Full prepay / ticketing | **0.9%** |
| Deposit (as little as 10% of avg check) | **1.7%** |
| Credit-card hold | **3.0%** |
| Automated reminders alone | −25–40% |

A 10% deposit isn't about recovering the loss — it's **skin in the game**; POS auto-
deducts it from the bill, neutral to the honest guest. **CFO trade-off:** prepay also
suppresses *bookings* (some guests won't commit) — it's a demand-elasticity vs
no-show-elasticity trade, not a pure win. Model both. Discounting to fill weak times
often lifts occupancy while *destroying* RevPASH — watch the yield number, not the seat
count.

---

## 9. Labor & the weekly operating cadence

> **Labor Cost % = Total Labor (wages + payroll tax + benefits) ÷ Revenue.** FD 35–45%
> (highest of any format) — brigade kitchens, 1:3–1:4 server ratios, sommeliers, runners.
> Judge on absolute dollars + productivity, not % (% swings with seasonal volume).

> **SPLH = Net Sales ÷ Labor Hours** (tips excluded). FD ~$50–80 (low end).
> **Labor Hour Budget = Forecast Sales ÷ Target SPLH** ← schedule to the forecast.
> e.g. $6,000 Saturday ÷ $95 SPLH ≈ 63 labor hours. Track FOH and BOH SPLH separately.

Scheduling quality alone = 3–5 pts of labor cost. Levers: staggered starts, real-time
send-homes, cross-training. Overtime costs +50% — chronic OT means hire part-time
instead. **Tip vs service charge (accounting trap):** *tips pass through, do NOT hit the
P&L*; *service charges are revenue → become wages when distributed* (inflate both top
line and labor line). Going "service-included" makes labor % jump optically even when
economics are similar.

### The Weekly Flash Report (the agent's operating output)
*"Monthly reports tell you what happened; weekly reports let you fix it."* Read in 5 min:
1. **Prime cost %** (the headline)
2. Food cost % (+ variance vs budget)
3. Beverage / pour cost % (separate)
4. Labor by department (FOH vs BOH)
5. Sales summary (WoW; food vs beverage split)
6. SPLH (productivity)
7. Inventory turnover (= COGS ÷ avg inventory; FD aim tight, count high-value weekly)
8. Food waste (actual vs theoretical; 4–10%)
9. Variance/budget alerts — flag drift *before the next service*

### Questions a sharp CFO asks each period
- Did prime cost hold target? Was the drift food, bev, or labor — price, waste, or theft?
- Which menu items carry margin, which drag it? What gets re-priced/re-engineered?
- SPLH by daypart — where are we over/understaffed? Is OT creeping?
- Are comps up on **traffic** (covers) or just **check/price**? (price-only growth is fragile)
- What share of covers are **returning regulars** vs new? Where is **CLV** trending?
- Is **beverage attachment per cover** holding? (the profit center)
- Liquidity to cover prime cost, debt, expansion without surprises?

---

## 10. Guest economics — the regular *is* the model

- ~**65%** of business comes from the existing base.
- A **5% retention lift → 25–95% profit lift** (Bain/Reichheld).
- Loyal guests visit ~20% more often, spend ~20–33% more per visit.
- Retention is 5–25× cheaper than acquisition → **CLV should govern marketing spend, not
  cover count.**

**Danny Meyer / Enlightened Hospitality:** stakeholder order = employees → guests →
community → suppliers → investors (returns are the *output* of the cycle). The "51%
solution": 51% emotional/hospitality, 49% technical. Under-investing in service breaks
the cycle that produces the high-CLV regulars the thin-margin model depends on. **The
CFO's tension: fund hospitality *and* hold prime cost** — both, not either.

This is Fudis's wedge: CLV, RFM segments, and the diner CRM are **financial line items**.
Knowing who the regulars are, their spend, and their preferences is margin protection.

---

## 11. Fudis data boundary — real vs modeled

| CFO metric | Fudis can compute? | Source / note |
|---|---|---|
| Revenue, trend, forecast | ✅ real | `revenue_trends`, `demand_forecast` |
| Average check / PPA, covers, revenue per cover | ✅ real | purchase history + bookings |
| Item revenue, menu mix | ✅ real | `menu_engineering`, `get_menu_performance` |
| Item contribution margin, menu quadrants | ✅ real where RMS `unit_cost` known, else **32% flat assumption** | `menu_engineering` |
| Channel mix | ✅ real | `channel-breakdown` |
| CLV, RFM, retention value, revenue-at-risk from churn | ✅ real | `customer_clv`, `customer_segments`, `campaign_triggers` |
| Revenue concentration (top items/customers/channel share) | ✅ derivable | compose existing reads |
| No-show count / lost-cover revenue | ⚠️ partial | bookings status; lost-revenue = no-shows × PPA (modeled) |
| **Food cost % (blended)** | ⚠️ real only where RMS cost exists | else needs operator food-cost % input |
| **Pour cost / beverage cost %** | ❌ needs input | no beverage-cost data |
| **Labor cost %, SPLH** | ❌ needs input | no labor/scheduling data |
| **Occupancy/rent, fixed costs** | ❌ needs input | no expense data |
| **Prime cost, EBITDA, net margin, break-even** | ❌ **modeled only** | from operator-supplied labor % + fixed costs |
| Inventory turnover, theoretical-vs-actual variance, waste | ❌ not yet | needs inventory data (POS Phase 3) |

**So the `financial-analyst` does two layers:**
- **Layer 1 (real, no caveats):** revenue + average check + covers + revenue
  concentration + menu contribution + channel mix + CLV/retention + revenue-at-risk.
- **Layer 2 (modeled, labeled):** ask the operator for food-cost % (or use RMS), labor %,
  and fixed monthly costs → compute prime cost, contribution, **break-even covers/
  revenue**, modeled EBITDA/net. Every modeled line marked as such.

---

## 12. Peru / LatAm localization

- **IGV (VAT) = 18%** on restaurant sales — a heavy wedge between menu price and net
  revenue. All margin math is **post-IGV**; price and break-even must net it out. (Peru
  has run reduced-IGV relief windows for restaurants/hotels — verify the current statutory
  rate before quoting.)
- **No US tipping model.** US labor benchmarks assume a tipped-wage structure (low base +
  tips off-payroll). Peru pays statutory wages + employer social charges → **fully-loaded
  labor % runs higher** than US bands; don't import the 35–45% FD figure blindly.
- **Informality** distorts competition: informal operators evade IGV/payroll/labor-law
  costs a formal fine-dining venue carries. Cost discipline, supplier formalization, and
  **retention economics** (where formal operators can't win on price) matter more.
- Tailwind: Peru gastronomy is a real engine ($1.8B culinary tourism 2024; Lima among the
  world's top dining cities) → genuine pricing power at the top end.

---

## 13. Voice — how the agent should talk

A real CFO: leads with the one number that matters (prime cost / the biggest $ swing),
quantifies in the restaurant's currency, separates **real** from **modeled** out loud,
names the *action* not just the metric, and is honest about thin margins ("at 4% net,
this 1.5-point food-cost drift is ~30% of your profit"). Never fabricates a benchmark to
sound precise — says "modeled on your inputs" or "I need your rough rent + labor % to
take this further." Frames retention as a margin lever, not marketing.
