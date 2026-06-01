# Fudis 4 Business — Claude Code Plugin

> Restaurant intelligence for Claude Code. Connect your Fudis account and get bookings, customer analytics, CRM, and campaign tools directly in your AI assistant.

[![Version](https://img.shields.io/badge/version-1.1.0-blue)](https://github.com/theFudis/fudis-claude-plugin/releases)
[![License](https://img.shields.io/badge/license-Elastic--2.0-blue)](LICENSE)
[![Marketplace](https://img.shields.io/badge/marketplace-fudi-orange)](https://github.com/theFudis/fudis-marketplace)

> **License notice:** Free to install and use for your restaurant. Not permitted for resale, courses, agency services, or redistribution. See [NOTICE.md](NOTICE.md).

---

## What This Is

**Fudis 4 Business** is a Claude Code plugin that connects your restaurant's data — guests, bookings, revenue, and menu performance — to Claude's reasoning. Instead of logging into a dashboard, you ask questions and get answers backed by live data.

It's built on the Retention-Led Growth philosophy: the guests you already have are your most valuable asset. The plugin is designed to surface who's at risk, who needs attention today, and what actions have the highest revenue impact.

Works for any restaurant, any currency, any language. Claude responds in the same language you write in.

---

## Installation

### Option A — Claude Code CLI (recommended)

```bash
# Add the Fudis marketplace
claude plugin marketplace add theFudis/fudis-marketplace

# Install the plugin
claude plugin install fudis@fudi

# Enable it
claude plugin enable fudis@fudi
```

On first use, Claude Code will prompt you to authenticate with your Fudis account (OAuth).

### Option B — Claude Desktop

1. Download [`fudis-claude-plugin.zip`](https://github.com/theFudis/fudis-claude-plugin/releases/latest)
2. Open Claude Desktop → Settings → Plugins → **Upload local plugin**
3. Drop the ZIP file and click Upload
4. Authenticate via your Fudis account when prompted

---

## Skills Reference

### Analytics & Operations

Skills that connect to your live Fudis data. Require a Fudis operator account.

| Skill | Arguments | What it does |
|---|---|---|
| `/fudis:briefing` | `[date]` | Daily ops summary — reservations, priority actions, segment health. Default: today. |
| `/fudis:retention` | `[days]` | Retention-Led Growth dashboard — churn risk, win-back targets, CLV top guests, revenue signal. Default: last 90 days. |
| `/fudis:winback` | `[segment\|name]` | Win-back execution — prioritized list with ready-to-send message drafts per guest. Segments: `at-risk`, `lost`, `one-timers`. |
| `/fudis:vip` | `[cold\|upcoming\|manage name]` | VIP tier management — who they are, who's going cold, upcoming visits this week. |
| `/fudis:guests` | `[name or phone]` | Guest CRM — look up any customer, view their history and CLV, manage VIP status, notes, and preferences. |
| `/fudis:bookings` | `[date\|create\|cancel\|reschedule]` | Reservations — list today's floor, create bookings (preview before confirm), update status, reschedule. |
| `/fudis:campaigns` | `[winback\|vip\|new]` | Campaign planning — 2-3 campaign ideas with target segment, message angle, and revenue potential. |
| `/fudis:menu` | `[engineering\|affinity\|performance\|dish name]` | Menu intelligence — quadrant analysis, basket affinity pairs, dead items, and one recommended action. |
| `/fudis:revenue` | `[trends\|forecast]` | Revenue trends + 30-day demand forecast with operational actions for peak dates. |
| `/fudis:weekly` | `[summary\|full]` | Weekly performance report — revenue, retention, bookings, menu highlights, next week outlook. |
| `/fudis:setup` | `[metric\|getting-started\|segments]` | Onboarding — metric explanations using your own live numbers, not abstract examples. |

### Content Skills

Skills that work without a Fudis account. Useful for any restaurant.

| Skill | Arguments | What it does |
|---|---|---|
| `/fudis:review` | `[paste review text]` | Craft responses to Google, TripAdvisor, or any platform — positive, negative, or aggressive. |
| `/fudis:menu-copy` | `[dish name\|section\|review]` | Write menu item descriptions, improve existing copy, or restructure sections. |
| `/fudis:message` | `[occasion or context]` | Draft any direct guest message — event, VIP invite, post-visit follow-up, apology, booking reminder. |
| `/fudis:event` | `[type, date, capacity]` | Plan a special event — structure, pricing mechanics, guest communications, ops checklist. |
| `/fudis:promo` | `[fill slow hours\|reward regulars\|launch new dish]` | Design brand-safe promotions that don't train guests to wait for discounts. |

---

## Agents

Agents handle multi-step, open-ended tasks that span multiple data sources. Invoke them by asking Claude to use a specific agent, or let `restaurant-ops` handle general questions.

| Agent | Model | Best for |
|---|---|---|
| `restaurant-ops` | Sonnet | General ops — any multi-step question combining bookings, guests, analytics, and menu |
| `retention-analyst` | Sonnet | Deep churn investigation — root cause analysis, pattern detection, quantified action plans |
| `campaign-strategist` | Sonnet | Full campaign briefs — target list, message drafts per guest, timing, ROI estimate |
| `menu-optimizer` | Sonnet | Strategic menu decisions — remove, reprice, bundle, and push with data justification |

---

## Architecture

```
fudis-claude-plugin/
├── .claude-plugin/
│   └── plugin.json          — plugin manifest
├── .mcp.json                — connects to mcp.fudis.app
├── settings.json            — default agent: restaurant-ops
├── hooks/
│   └── hooks.json           — SessionStart: shows connected restaurant
├── references/              — shared across all skills and agents
│   ├── config.md            — currency, language, and market context rules
│   ├── benchmarks.md        — industry benchmarks (North America, regional-tagged)
│   └── terminology.md       — universal glossary: RFM, CLV, churn, segments
├── agents/                  — 4 specialized agents
└── skills/                  — 16 skills (11 with MCP, 5 content-only)
    └── menu-copy/
        └── references/
            └── examples.md  — multi-cuisine menu copy examples
```

**Plugin-level references** (`references/`) are shared across all skills — loaded on demand when relevant, not injected into every conversation. This keeps the always-on token cost to ~1,100 tokens.

**Currency and language** are resolved dynamically from your restaurant's data and from the language you write in. Nothing is hardcoded.

---

## Requirements

- Claude Code v2.1.143 or later
- A Fudis operator account — [business.fudis.app](https://business.fudis.app)
- Content skills (`review`, `menu-copy`, `message`, `event`, `promo`) work without an account

---

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to extend or improve the plugin.

---

## Support

[business.fudis.app](https://business.fudis.app) · [hello@fudis.app](mailto:hello@fudis.app)
