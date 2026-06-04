```
╔═══════════════════════════════════════════════════════════════╗
║                                                               ║
║   🍽️  FUDIS 4 BUSINESS                                       ║
║   Claude Code Plugin · v1.2.0                                 ║
║                                                               ║
║   17 skills · 4 agents · 1 MCP · any currency · any language  ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
```

[![License](https://img.shields.io/badge/license-Elastic--2.0-4B6FFF?style=flat-square)](LICENSE)
[![Marketplace](https://img.shields.io/badge/marketplace-fudi-FF6B35?style=flat-square)](https://github.com/theFudis/fudis-marketplace)
[![MCP](https://img.shields.io/badge/MCP-mcp.fudis.app-22C55E?style=flat-square)](https://mcp.fudis.app)

> **Not for resale, courses, or redistribution.** See [NOTICE.md](NOTICE.md).

---

## What lives in this repo

A Claude Code plugin that connects restaurant operators to their live data. No dashboard. No app switching. You ask Claude, Claude calls the tools, you get answers.

Built on **Retention-Led Growth** — the philosophy that the guests you already have are your highest-ROI asset. Every skill in this plugin is designed around that lens: who's at risk, who deserves attention today, what action moves the most revenue.

---

## 📁 Repo structure

```
fudis-claude-plugin/
│
├── 🔧 .claude-plugin/plugin.json     plugin manifest (name, version, license)
├── 🔌 .mcp.json                      connects to mcp.fudis.app via OAuth
├── ⚙️  settings.json                  default agent → restaurant-ops
│
├── 🪝 hooks/
│   └── hooks.json                    SessionStart: shows connected restaurant + skill list
│
├── 📚 references/                    shared across ALL skills and agents
│   ├── config.md                     how currency, language & market context are resolved
│   ├── benchmarks.md                 industry benchmarks (North America, regional-tagged)
│   └── terminology.md                universal glossary: RFM, CLV, churn, segments
│
├── 🤖 agents/                        4 specialized agents (see below)
│
└── 🎯 skills/                        17 skills across 2 tiers (see below)
    └── menu-copy/
        └── references/
            └── examples.md           multi-cuisine menu copy examples (loaded on demand)
```

---

## 🎯 Skills — 17 total

### Tier 1 · Analytics & Operations
> Require a Fudis operator account. Call the live MCP at mcp.fudis.app.

| Skill | Args | What it pulls | What you get |
|---|---|---|---|
| 🌅 `/fudis:briefing` | `[date]` | bookings · actions · segments · overview | Daily ops summary. Read at shift start. |
| 📊 `/fudis:retention` | `[days]` | segments · CLV · triggers · revenue | Full Retention-Led Growth dashboard. Who's churning, who to call. |
| 🪃 `/fudis:winback` | `[segment\|name]` | triggers · CLV · profiles | Prioritized list + ready-to-send message drafts per guest. |
| ⭐ `/fudis:vip` | `[cold\|upcoming\|manage]` | CLV · bookings · triggers | VIP tier — who they are, who's going cold, this week's VIP visits. |
| 👤 `/fudis:guests` | `[name or phone]` | search · profile | Full guest CRM: history, CLV, segment, VIP status, notes, preferences. |
| 📅 `/fudis:bookings` | `[date\|create\|cancel\|reschedule]` | bookings | List floor, create (preview first), update status, reschedule. |
| 🎟️ `/fudis:events` | `[name\|date\|check in\|cancel]` | events · occurrences · attendees | Live ticketed events: what's on, door/guest list, check guests in by code, put a date on sale or cancel (notifies attendees). |
| 📣 `/fudis:campaigns` | `[winback\|vip\|new]` | triggers · segments · CLV | 2-3 concrete campaign ideas with segment, message angle, revenue estimate. |
| 🍽️ `/fudis:menu` | `[engineering\|affinity\|performance\|dish]` | engineering · affinity · performance | Stars/plowhorses/puzzles/dogs · basket pairs · dead items · one action. |
| 💰 `/fudis:revenue` | `[trends\|forecast]` | revenue · forecast | Trend direction + 30-day demand forecast + ops actions for peak dates. |
| 📈 `/fudis:weekly` | `[summary\|full]` | revenue · segments · bookings · menu · forecast | Full week: revenue, retention, bookings, menu, next week outlook. |
| 🎓 `/fudis:setup` | `[metric\|getting-started\|segments]` | restaurants · segments · overview | Onboarding using your own live numbers. No abstract examples. |

### Tier 2 · Content Skills
> No Fudis account needed. Works for any restaurant.

| Skill | Args | What you get |
|---|---|---|
| ⭐ `/fudis:review` | `[review text]` | Crafted response to any online review — Google, TripAdvisor, any platform. Tone-matched to positive / constructive / aggressive. |
| ✍️ `/fudis:menu-copy` | `[dish\|section\|review]` | Menu item descriptions, pricing framing, section restructuring. Pulls multi-cuisine examples from `references/examples.md`. |
| 💬 `/fudis:message` | `[occasion]` | Direct guest message for any occasion — event, VIP invite, apology, post-visit, booking reminder. |
| 🎉 `/fudis:event` | `[type, date, capacity]` | *Plans* a new special event — structure, pricing mechanics, two guest messages, ops checklist. (To run events that already exist in Fudis, use the live `/fudis:events` skill above.) |
| 🎁 `/fudis:promo` | `[goal]` | Brand-safe promotion design. No percentage discounts. Mechanics that don't train guests to wait for deals. |

---

## 🤖 Agents — 4 specialists

Agents handle open-ended, multi-step tasks. The default (`restaurant-ops`) activates automatically. Others are invoked by name.

```
┌─────────────────────────────────────────────────────────────────┐
│  🏪  restaurant-ops      (default · Sonnet · medium effort)      │
│      General ops. Any question combining bookings, guests,       │
│      analytics, and menu. The starting point for everything.     │
├─────────────────────────────────────────────────────────────────┤
│  🔬  retention-analyst   (Sonnet · high effort · 20 turns)       │
│      Deep churn investigation. Root cause, pattern detection,    │
│      quantified action plans. Goes further than /fudis:retention │
├─────────────────────────────────────────────────────────────────┤
│  📢  campaign-strategist  (Sonnet · high effort · 20 turns)      │
│      Full campaign brief. Target list, message drafts per guest, │
│      timing, ROI estimate. Execution-ready, not ideation.        │
├─────────────────────────────────────────────────────────────────┤
│  🍳  menu-optimizer       (Sonnet · high effort · 15 turns)      │
│      Data-justified menu decisions: REMOVE / REPRICE / BUNDLE /  │
│      PUSH. Pulls engineering + affinity + performance + forecast. │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📚 Shared References

Three files in `references/` are loaded on demand across all skills and agents — never injected into every session:

| File | Loaded when | Contains |
|---|---|---|
| `config.md` | setup skill, any config question | How currency (from MCP data), language (from operator input), and market context are resolved. Nothing hardcoded. |
| `benchmarks.md` | retention · winback · campaigns · agents | North American industry benchmarks, regionally tagged, with localization guidance |
| `terminology.md` | setup + any metric question | Universal glossary: RFM segments, CLV, churn probability, basket affinity, campaign triggers |

**Always-on token cost: ~1,100 tokens.** Skills load their references only when needed.

---

## ⚡ Install

### Claude Code CLI

```bash
claude plugin marketplace add theFudis/fudis-marketplace
claude plugin install fudis@fudi
claude plugin enable fudis@fudi
```

### Claude Desktop

Settings → Plugins → Upload local plugin → drop the ZIP from [Releases](https://github.com/theFudis/fudis-claude-plugin/releases/latest)

---

## Requirements

- Claude Code v2.1.143+
- Fudis operator account at [business.fudis.app](https://business.fudis.app) *(Tier 1 skills only)*
- Tier 2 content skills work for any restaurant without an account

---

[CHANGELOG.md](CHANGELOG.md) · [CONTRIBUTING.md](CONTRIBUTING.md) · [NOTICE.md](NOTICE.md) · [hello@fudis.app](mailto:hello@fudis.app)
