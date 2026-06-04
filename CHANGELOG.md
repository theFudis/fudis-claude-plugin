# Changelog

All notable changes to the Fudis 4 Business Claude Code plugin.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/). This project uses [semantic versioning](https://semver.org/).

---

## [1.2.0] — 2026-06-03

### Added — Live events

- **`/fudis:events`** — new Tier 1 (MCP-backed) skill for running ticketed events that already exist in Fudis. Surfaces the six new event tools on the `mcp.fudis.app` server:
  - `list_events` — what's on, with status counts and next-date / cupos summary
  - `get_event` — one event's full definition
  - `list_event_occurrences` — the dates (occurrences) of an event with per-date status
  - `list_event_attendees` — the door / guest list (issued + checked-in tickets)
  - `check_in_attendee` — live door check-in by confirmation code (`issued → checked_in`; staff role, no capability gate)
  - `update_occurrence_status` — change a date's status; cancelling cancels all confirmed orders and notifies every attendee (manager role)
- SessionStart status line now advertises `/fudis:events`.

### Changed

- Tier 2 `/fudis:event` clarified as the event **planner** (content, no account). Live event operations now live in `/fudis:events`, mirroring the existing `bookings`(live) vs `event`(planning) split.
- `plugin.json` description + keywords mention events; version → 1.2.0.

---

## [1.1.0] — 2026-05-31

### Changed — Global architecture

- **English skill names**: renamed 8 skills to English for global use — `clientes→guests`, `reservas→bookings`, `campana→campaigns`, `carta→menu-copy`, `mensaje→message`, `evento→event`, `oferta→promo`, `responder→review`
- **Currency-agnostic**: removed all hardcoded `S/` (Peruvian soles) references. Currency is now read from the restaurant's own data via the MCP and rendered dynamically
- **Language-agnostic**: removed all `Respond in Spanish` directives from skill and agent instructions. Claude now matches the language the operator writes in
- **English skill/agent instructions**: all SKILL.md bodies and agent prompts converted to English for better model reasoning and global readability
- **Plugin description**: removed Peru-specific wording from `plugin.json`

### Added

- `references/config.md` — plugin-level reference explaining how currency, language, and market context are resolved. Loaded by `setup` skill
- `references/terminology.md` — universal analytics glossary for RFM, CLV, churn, and segments. Previously lived only inside `setup/`, now shared across all skills
- `references/benchmarks.md` — updated with regional tags (North America source noted), currency conversion guidance, and a "how to localize" section per metric
- `skills/menu-copy/references/examples.md` — multi-cuisine menu copy transformation examples (Peruvian, Italian, Japanese, Mexican, French) loaded on demand

### Removed

- `skills/setup/references/glossary.md` — superseded by plugin-level `references/terminology.md`
- Hardcoded event price ranges (Valentine's, NYE) — replaced with "anchor to the restaurant's own average ticket" guidance

---

## [1.0.0] — 2026-05-31

### Added — Initial release

**11 analytics skills** (require Fudis account):
- `/fudis:briefing` — daily operations briefing
- `/fudis:retention` — Retention-Led Growth dashboard
- `/fudis:winback` — win-back campaign execution with message drafts
- `/fudis:vip` — VIP guest management
- `/fudis:guests` — guest CRM and profile management
- `/fudis:bookings` — reservations — list, create, update, reschedule
- `/fudis:campaigns` — campaign planning and customer targeting
- `/fudis:menu` — menu engineering and basket affinity
- `/fudis:revenue` — revenue trends and demand forecast
- `/fudis:weekly` — weekly performance report
- `/fudis:setup` — onboarding and metric explanations

**5 content skills** (no account needed):
- `/fudis:review` — online review response writer
- `/fudis:menu-copy` — menu item description writer
- `/fudis:message` — guest message drafter
- `/fudis:event` — special event planner
- `/fudis:promo` — brand-safe promotion designer

**4 agents**:
- `restaurant-ops` — general operations agent (default)
- `retention-analyst` — deep churn analysis
- `campaign-strategist` — full campaign briefs
- `menu-optimizer` — data-justified menu decisions

**Plugin infrastructure**:
- MCP connection to `mcp.fudis.app` with OAuth authentication
- `SessionStart` hook showing connected restaurant and available skills
- Plugin-level `references/benchmarks.md` with North American industry data
- `defaultEnabled: false` — requires explicit opt-in after install
