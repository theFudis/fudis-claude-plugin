# restaurant-finance.md — Multi-Category Financial Reference
*Agent knowledge base for the `financial-analyst` agent. Companion to `fine-dining-cfo.md` (fine dining deep-dive).*
*Sources: National Restaurant Association 2025 Abstract, PANCA.pe Peru benchmarks, PRODUCE 2025 sector report, VantaInsights 2026, GoodSource, 7shifts, BlackBox Intelligence, Dataintelo, Rappi/Contrary Research.*

---

## §0 — How to Use This Reference

**The agent's first move:** identify restaurant category, then load the matching section. Categories share the same cost-structure skeleton (food cost → labor → prime cost → fixed → EBITDA → net) but differ in what moves the needle.

```
Category intake → which section to load → which metrics to surface → which benchmarks to apply
```

### Category Map
| Category | Key Lever | Risk Anchor | Primary Metric |
|---|---|---|---|
| Fine dining | Menu contribution margin + CLV | Empty seats + no-shows | RevPASH |
| Casual / pollerías / criollas | Labor efficiency | Labor overstaffing + food waste | SPLH |
| Bar hybrid (cevichería + bar) | Beverage program margin | Pour cost variance (theft/waste) | Pour cost % |
| Ghost kitchen / delivery-only | Net revenue after commission | Platform fee drag | Net commission-adjusted revenue |
| Multi-location group | Central purchasing leverage | Per-location variance | Location P&L delta |

> Fine dining: see `fine-dining-cfo.md`. This file covers the other four categories.

---

## §1 — Data Boundary (applies to all categories)

| Data point | What Fudis has | Reliability |
|---|---|---|
| Revenue | ✅ Real (POS sync or booking-derived) | High |
| Menu sales mix | ✅ Real (item-level via RMS) | High |
| Menu COGS | ⚠️ Real where RMS has cost cards; else 32% flat default | Medium |
| CLV / RFM | ✅ Real (computed from purchase history) | High |
| Labor % | ❌ Operator must provide | None until input |
| Rent + fixed costs | ❌ Operator must provide | None until input |
| Delivery commission | ❌ Operator must provide platform/rate | None until input |
| Pour cost (actual) | ❌ Requires beverage-specific POS | None until input |

**Agent rule:** never estimate EBITDA or net profit without operator-supplied labor % and fixed costs. State this clearly. Offer to model with assumed inputs if operator agrees.

---

## §2 — Casual Dining / Pollerías / Comida Criolla

### Why this category is different
Higher volume, shorter check averages, faster turns. Profit comes from throughput and labor efficiency — not from table experience or beverage upsell. The margin is thin but the volume compensates. Labor scheduling is the #1 controllable lever.

### Peru-Specific Benchmarks (PANCA.pe, 2024–2025)
| Type | Food Cost | Gross Margin | Net Margin | Avg Ticket |
|---|---|---|---|---|
| Pollería | 32–38% | 62–68% | 8–14% | S/ 35–65 (pollo entero) |
| Cevichería (food-only) | 30–38% | 62–70% | 10–16% | S/ 35–65 |
| Chifa | 22–28% | 72–78% | 12–18% | S/ 20–40 |
| Menú del día | 35–45% | 55–65% | 6–12% | S/ 10–18 |
| Criollo / carta | 28–33% | 67–72% | 8–13% | S/ 35–60 |

### Global Casual Benchmark (NRA 2025)
- Food cost: 30–34% (Olive Garden averaged ~33%)
- Labor (full-service median): 36.5% of sales
- Labor for **profitable** full-service operators: 34.2% (vs 42.9% for loss-making ones)
- Casual dining labor target: 25–30% (less service-intensive than fine dining)
- Prime cost target: <65%
- Net margin: 3–5% (full-service); 6–9% (fast casual)

### The Primary Metric: SPLH (Sales Per Labor Hour)
```
SPLH = Total Revenue ÷ Total Labor Hours
```
| Concept | SPLH Benchmark |
|---|---|
| Casual dining (full-service) | $40–80 / hr (USD equivalent) |
| Fast casual | Between casual and QSR |
| QSR | ~$150 / hr |
| Fine dining | $75–100 / hr (high revenue per cover, low volume) |

- Low SPLH → overstaffed relative to sales
- SPLH rising → good (more revenue per hour worked, or leaner scheduling)
- Review cadence: **daily by shift**, not monthly

### Operational Watch Points
1. **Labor scheduling vs sales forecast** — the single biggest casual lever. Static schedules lose 1.5–2% of labor ratio vs demand-adjusted schedules.
2. **Plate mix by margin** — chaufa (75% food margin) vs lomo saltado (~62%) in Peru context. Know your Stars vs Plows.
3. **Portion control** — in high-volume casual, 10g over-portion on every plate × 300 covers × 365 days = significant waste.
4. **Daypart efficiency** — many criollas are profitable at lunch, break-even at dinner. Know which daypart earns vs which covers overhead.

### Fudis Opportunity
Fudis knows revenue and item sales mix (real). Labor % comes from operator. With both, can compute:
- SPLH per shift (if labor hours tracked)
- Contribution margin by item (identifies menu over-performers)
- Revenue trend vs prior periods (organic growth vs seasonal)
- RFM: identify if the "almuerzo habitual" customer is being retained

### The Question to Ask First
> "What percentage of your sales is from delivery apps (Rappi/PedidosYa) vs dine-in? And do you want to focus on food cost, labor efficiency, or both today?"

---

## §3 — Bar Hybrid (Cevichería + Cocktail Bar / Pisco Bar)

### Why this category is different
The bar program is the margin engine. Food (ceviche, tiraditos, causas) brings people in; the pisco sour and cocktail program is where money is actually made. A 30% beverage mix completely changes the P&L vs a food-only cevichería. The #1 diagnostic is **beverage revenue as % of total** — it predicts net margin better than any other single variable.

### Bar Margin Structure
| Beverage type | Pour cost | Gross margin | Net margin driver |
|---|---|---|---|
| Spirits / pisco / cocktails | 18–22% | 78–82% | Volume × price discipline |
| Premium/craft cocktails | 18–25% | 75–82% | Recipe standardization |
| Draft beer | 15–18% | 82–85% | Keg turnover, waste |
| Bottled beer | 24–28% | 72–76% | Consistent |
| Wine by glass | 30–40% | 60–70% | Spoilage risk |
| Wine by bottle | Better margin | Higher AOV | Upsell opportunity |

### Hybrid Model Economics
- Pure bar net margin: **7–12%** (vs restaurant 3–9%)
- Restaurant with strong bar program: **5–10%** blended (bar program subsidizes food margins)
- **Beverage mix % is the blended margin predictor**: every 5pp shift toward beverages lifts net margin ~0.5–1pp
- A S/ 45 ceviche at 70% food gross margin generates S/ 31.50 gross profit
- A S/ 40 pisco sour at 20% pour cost generates S/ 32.00 gross profit — same absolute profit, higher margin %

### The Primary Metric: Pour Cost %
```
Pour cost % = Cost of beverages sold ÷ Beverage revenue
Target: 18–24% overall
```
**The gap between theoretical and actual pour cost = money leaving the building**
- Theoretical pour cost: what pour cost *should* be based on recipes and prices
- Actual pour cost: what it *is* based on inventory counted
- Gap > 2%: investigate over-pouring, spillage, theft, comps without recording

### Operational Watch Points
1. **Inventory reconciliation** — count weekly, not monthly. Daily reconciliation at high-volume bars. The gap is where the problem lives.
2. **Recipe cards** — every cocktail standardized. A bartender who free-pours will blow 3pp of pour cost.
3. **Comp and waste tracking** — every free drink must be recorded. Untracked comps inflate "actual" pour cost.
4. **High-margin cocktail placement** — the signature pisco cocktail at 20% pour cost should be on every table tent. Engineering applies to beverage as much as food.
5. **Staffed vs unstaffed bar hours** — bar labor is fixed over the shift; revenue scales with covers. Late shifts with low covers destroy bar EBITDA.

### Fudis Opportunity
Fudis has total revenue and item-level data. With beverage items tagged (requires menu categorization):
- Compute beverage % of revenue (the single most predictive ratio)
- Surface which cocktails are volume leaders vs margin leaders
- CLV: bar hybrid customers often have higher frequency and check averages — segment them
- Retention: the customer who comes for a pisco sour at 8pm Thursday is different from the lunch ceviche crowd

### The Question to Ask First
> "What share of your revenue comes from beverages — cocktails, pisco, beer? Roughly what percentage?"

---

## §4 — Ghost Kitchen / Delivery-Only (Cocina Virtual)

### Why this category is different
No FOH, no waiters, no ambiance. Lower fixed costs (rent, FOH labor) but a hidden structural cost: platform commissions eat 15–30% of gross revenue **before the restaurant sees a sol**. Most operators calculate food cost % against the gross ticket price — the fatal mistake. The correct anchor is **net revenue after commission**.

### Platform Commission Structure in Peru
| Platform | Commission range (restaurant side) | Additional context |
|---|---|---|
| Rappi | 15–25% of order value | Market leader in Lima/Cusco |
| PedidosYa | 15–25% (absorbed Glovo Peru) | Widest restaurant selection |
| Delivery Hero / iFood | 20–25% | LatAm standard |
| Direct ordering (own app/WhatsApp) | 0% | But requires marketing investment |

**Commission 20–25% is the Peru working assumption** unless the operator provides the actual rate from their contract.

### The Corrected P&L Structure
```
Gross revenue (what customer pays)        S/ 100.00
- Platform commission (20–25%)            S/ -22.00
= Net revenue (what restaurant receives)  S/  78.00
- Food cost (% of NET, not gross)         S/ -28.00 (36% of net)
- Packaging (3–5% of gross)               S/  -4.00
- Labor (no FOH, kitchen only)            S/ -18.00 (23% of net)
= Kitchen contribution                    S/  28.00 (28% of net / 28% of gross)
- Fixed (rent, utilities, equipment)      S/ -12.00
= EBITDA                                  S/  16.00
```

**The mistake:** if you calculate food cost % on the gross S/ 100 ticket, food cost looks like 28%. On net revenue of S/ 78, it's 36% — much closer to the danger zone. The platform commission must be treated as a cost-of-revenue line, not a marketing expense.

### Well-Managed Ghost Kitchen Benchmarks (Dataintelo 2025)
| Model | EBITDA margin |
|---|---|
| Purpose-built multi-brand cloud kitchen | 18–28% |
| Traditional dine-in (for comparison) | 8–14% |
| Commissary/shared kitchen model | 12–18% |
| Single-brand delivery (commission drag unaddressed) | Often < 5% |

### The Multi-Brand Leverage
The EBITDA advantage of ghost kitchens comes from running multiple virtual brands from one kitchen:
- One kitchen crew, one rent, multiple menus on multiple platforms
- Each additional brand runs at near-zero marginal fixed cost
- Utilization rate (% of kitchen hours revenue-generating) is the key operational KPI

### Operational Watch Points
1. **Commission rate negotiation** — operators who hit volume thresholds can negotiate lower rates. Know your monthly GMV per platform.
2. **Direct channel development** — every order through WhatsApp/direct = 20–25% more margin. Loyalty and CRM investment pays back here at 20x the rate of dine-in.
3. **Menu optimization for delivery** — not all menu items travel well or photograph well. Delivery-only menus should be engineered for 4-5 stars on app + high margin. Stars and Question Marks look different in delivery.
4. **Packaging cost** — 3–5% of gross, often ignored. Standardize and buy in volume.
5. **Peak hour scheduling** — kitchen labor must match delivery demand curves. Rappi/PedidosYa have weekend lunch and Friday/Saturday evening spikes. Staff accordingly.

### Fudis Opportunity
Fudis has revenue and item data. Agent can:
- Reframe food cost % against net revenue (expose the real margin)
- Identify best and worst margin items on delivery menu
- Compute delivery-adjusted CLV (a customer who orders S/ 80 delivered 3x/month = S/ 2,880 gross / year, but net to restaurant ~S/ 2,160)
- Flag when delivery % of mix is rising and what it costs the P&L

### The Question to Ask First
> "What platform are you on — Rappi, PedidosYa, or both? And do you know your commission rate, or should we use the 20–22% industry average for Peru?"

---

## §5 — Multi-Location Group

### Why this category is different
Two P&Ls always: per-location (operational) and consolidated (strategic). The key tension is that a location can look healthy in isolation but drag the group, or vice versa. The financial advantage of being multi-location is buying leverage — but only if used.

### Group P&L Structure
```
Consolidated P&L
├── Location A P&L (granular, weekly)
├── Location B P&L (granular, weekly)
├── Location C P&L (granular, weekly)
└── Corporate overhead (allocated or separate line)
```

Management reports must answer:
1. Which location has the lowest prime cost? → that's the practice to replicate
2. Which has the highest food cost variance? → that's the problem to fix
3. Where is SPLH weakest? → staffing or scheduling problem
4. What is the cross-location purchasing savings vs independent?

### Central Purchasing Leverage
| Scale | Savings vs independent purchasing |
|---|---|
| 2–5 locations | 5–10% food cost reduction |
| 5–10 locations | 8–15% |
| 10+ locations / GPO | 10–35% |

**Mechanism:** volume commitments to a single supplier trigger price tier discounts. A chain buying 500kg of chicken/week gets better per-kg pricing than 5 restaurants each buying 100kg. Beyond price: consistent quality, fewer invoice lines, simpler compliance.

### Key Group Metrics
| Metric | What it reveals |
|---|---|
| Location P&L delta (best vs worst) | Replication opportunity / turnaround priority |
| Cross-location food cost variance | Purchasing consistency or waste problem |
| Per-location SPLH | Labor efficiency at each site |
| Consolidated EBITDA margin | Group health; what investors see |
| Corporate overhead as % of revenue | Whether the center is earning its cost |
| Cross-location CLV | Are customers loyal to the brand or the location? |

### Cross-Location CLV: Fudis's Unique Edge
Every other analytics tool is single-tenant — they can't see a customer across multiple locations. Fudis can (where customer identity can be linked via phone, WhatsApp, or loyalty).

A customer who visits Location A 4x/year and Location B 3x/year is a **7-visit annual regular** from a brand perspective. The operator sees them as a 4-visit customer and a 3-visit customer. Fudis sees the full picture.

**The question this unlocks:** "If we open Location C in district X, which of our existing customers live nearby and would likely transfer?"

### Operational Watch Points
1. **Standardized P&L template** — all locations must report on identical line items. Apples-to-apples comparison impossible otherwise.
2. **Weekly flash P&L per location** — don't wait for month-end. Problems compound weekly.
3. **Manager-level P&L accountability** — location managers who see their own P&L and benchmark vs other locations outperform those who don't.
4. **Shared labor vs dedicated** — some roles (bookkeeper, social media, purchasing manager) can be shared across locations. This is where the second location reaches breakeven faster than the first.
5. **Brand vs location loyalty distinction** — know whether your CRM follows the customer across locations or treats them as independent records.

### Fudis Opportunity
Fudis has per-location revenue, item mix, and CLV data. Agent can:
- Surface per-location revenue comparison
- Identify best-margin menu items that should be shared across locations
- Compute cross-location CLV (the unique differentiator)
- Flag locations underperforming on same-week revenue vs prior year
- Help allocate marketing spend based on where loyal customers live

### The Question to Ask First
> "Do you want to look at all locations together, or focus on a specific one? And do you want to compare performance across locations?"

---

## §6 — Peru Market Context (applies to all categories)

### Sector Scale (PRODUCE 2025–2026)
- Restaurant sector GDP contribution: S/ 14,895 million value-added (2.5% of national GDP)
- Sector grew 2.3% in 2025, 3.5% in 2024 (7% CAGR 2021–2025)
- 161,000+ formal restaurants in Peru; 99.8% are MYPE
- 19.2 million Peruvians consume in restaurants
- Lima concentrates 34% of formal restaurants
- 82.5% informal employment in the sector (labor cost reporting is unreliable)

### IGV (VAT) — the Peru wedge
- IGV = 18% on all restaurant sales
- All benchmarks in this file are on **revenue inclusive of IGV** (what the customer pays)
- True revenue to the restaurant = ticket ÷ 1.18
- True margin base = ticket ÷ 1.18
- Example: S/ 100 ticket → S/ 84.75 net of IGV → food cost and labor % calculated on S/ 84.75
- **Note:** Many operators and benchmarks (including PANCA.pe's local data) report on gross ticket prices inclusive of IGV. Be explicit about which base you're using.

### Informality Distortion
- 8 in 10 restaurant jobs in Peru are informal
- This means labor cost reporting by operators is typically underreported
- "Labor" may not include social benefits, EsSalud contributions, or gratificaciones
- Formal labor costs are materially higher than what operators report
- When operator says "my labor is 20%," real total labor burden is likely 25–30%

### Currency Note
All Fudis data in Peruvian soles (S/). Reference benchmarks in USD (global sources) use approximate exchange rate. In-conversation, always state values in S/ unless operator requests USD.

---

## §7 — Cross-Category Benchmark Summary

| Metric | Fine Dining | Casual / Pollería | Bar Hybrid | Ghost Kitchen | Multi-Location |
|---|---|---|---|---|---|
| Food cost % | 28–35% | 28–38% | 25–35% (food only) | 35–40% (of NET) | Varies by concept |
| Beverage cost % | N/A or 30–40% | N/A | 18–24% pour cost | N/A | Varies |
| Labor % | 30–35% | 25–30% | 25–35% | 15–20% (kitchen only) | 30–36% (full-service mix) |
| Prime cost | <60% | <65% | <60% | <60% of net | <65% consolidated |
| Net margin | 5–12% | 8–14% (Peru) | 7–12% | 15–25% (if well-managed) | Varies by mix |
| Primary metric | RevPASH | SPLH | Pour cost % | Net revenue (post-commission) | Per-location P&L delta |
| Fudis data (real) | Revenue, CLV, menu margin | Revenue, CLV, item mix | Revenue (total), item mix | Revenue (needs commission adj.) | Per-location all above |
| Fudis data (needs input) | Rent, labor | Labor, rent | Beverage breakdown, pour | Commission rate, packaging | Corporate overhead |

---

## §8 — Agent Behavioral Rules

1. **Identify category before surfacing metrics.** Ask if not obvious from context.
2. **State the data boundary clearly** — distinguish real Fudis data from modeled assumptions.
3. **Never estimate prime cost or EBITDA without labor %.** Offer to model with an assumed range if operator agrees.
4. **Adjust for IGV when precision matters** — flag which revenue base you're using.
5. **Delivery commission is a cost of revenue line, not a footnote** — always show net revenue in ghost kitchen analysis.
6. **For bar hybrids, ask beverage mix % first** — it's the single most predictive variable.
7. **For multi-location, default to per-location view unless operator asks for consolidated** — location-level is more actionable.
8. **Use Peru benchmarks (PANCA.pe) when available, note when using global proxies** — the Peruvian food cost ranges differ materially from the US.
9. **Informality caveat:** if labor % seems low (< 20%), note that formal labor burden with benefits is typically 25–30%.
10. **Tone:** practical, numbers-first, no jargon without definition. The operator is running a restaurant, not reading a finance textbook.
