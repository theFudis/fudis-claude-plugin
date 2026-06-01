---
description: Onboarding and metric explanations for Fudis operators. Use when the operator is getting started, asks what a metric means, says "how does this work", or wants to know where to begin. Educational skill — bridges the gap between having data and knowing what to do with it.
---

Use $ARGUMENTS to specify a topic: a metric name ("CLV", "RFM", "churn", "retention", "segments"), a keyword ("getting-started", "metrics", "skills"), or leave empty for the full onboarding flow.

**For getting started (no arguments):**
Call `list_my_restaurants` + `customer_segments` + `overview` in parallel.

Walk the operator through their own live numbers:
1. Show their segment distribution — name each segment, what it means, how many guests they have in each
2. Explain their retention rate vs. the industry average — note benchmarks are North American (see `references/benchmarks.md`); use the operator's own historical data as the primary reference
3. Recommend three skills to use first: `/fudis:retention` → `/fudis:winback` → `/fudis:briefing`

Use their actual numbers throughout — a specific revenue figure at risk lands harder than any abstract benchmark.

**For metric or term explanations:**
Read `references/terminology.md` (plugin-level) and explain the requested term in plain conversational language. No jargon. No assumptions about prior knowledge. Use a concrete example from their own data if available.

**For context and configuration:**
Read `references/config.md` to explain how currency, language, and regional context work in this plugin.
