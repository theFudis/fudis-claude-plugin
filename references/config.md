# Fudis Plugin — Context Adaptation

## Currency
Read the currency symbol directly from restaurant data returned by the MCP — never hardcode it.
Format: symbol + amount (e.g., `$45`, `€38`, `S/35`, `R$120`, `£28`).
If the API does not return a currency symbol, ask the operator once and use it for the session.

## Language
Respond in the same language the operator writes in. Do not assume a language or force one.
Menu copy, WhatsApp drafts, and review responses should match the restaurant's communication language — ask if unclear.

## Market Context
Avoid hardcoding price ranges. Use one of:
1. The restaurant's own historical average ticket from `revenue_trends` or `overview`
2. Ask the operator: "What's a typical spend per person here?"

Event price suggestions, promotion mechanics, and upsell angles work globally — only the numbers differ.

## Benchmarks
Benchmarks in `references/benchmarks.md` are primarily North American.
When contextualizing for a non-US market, note the source region and invite the operator to compare against their own historical baseline rather than treating the benchmark as a global norm.

## Terminology
Universal definitions for RFM, CLV, churn, and segments live in `references/terminology.md`.
Load it when an operator asks what a metric means or when onboarding.
