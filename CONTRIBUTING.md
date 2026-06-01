# Contributing to Fudis 4 Business Plugin

## Overview

The plugin is a collection of SKILL.md files, agent markdown files, and shared references. No build step, no dependencies — just markdown and JSON.

## Repository structure

```
fudis-claude-plugin/
├── .claude-plugin/plugin.json   — version and metadata
├── .mcp.json                    — MCP server connection
├── settings.json                — default agent
├── hooks/hooks.json             — session hook
├── references/                  — shared plugin-level references
│   ├── config.md                — adaptation rules (currency, language)
│   ├── benchmarks.md            — industry benchmarks
│   └── terminology.md           — analytics glossary
├── agents/                      — agent markdown files
└── skills/                      — skill directories
    └── <skill-name>/
        ├── SKILL.md             — required
        └── references/          — optional skill-level references
```

## Adding a new skill

1. Create `skills/<skill-name>/SKILL.md` with YAML frontmatter:
   ```markdown
   ---
   description: One sentence on what this does and when to invoke it. This is the trigger mechanism — be specific.
   ---

   [skill instructions here]
   ```

2. Keep SKILL.md under 500 lines. Move detailed content to `skills/<skill-name>/references/` and reference it from SKILL.md.

3. Skills that call MCP tools should list the tools used and their order/parallelism.

4. Skills that don't need MCP should note "No MCP needed" in the description.

5. Do not hardcode currency symbols, language directives, or country-specific examples in SKILL.md. See `references/config.md` for how context adaptation works.

## Adding a new agent

Create `agents/<name>.md`:

```markdown
---
name: agent-name
description: When to invoke this agent. Include trigger scenarios.
model: sonnet
effort: medium | high
maxTurns: 15
---

[agent system prompt here]
```

Agents reference `references/benchmarks.md` for quantitative context. Currency comes from the restaurant's MCP data, not from the agent prompt.

## Modifying shared references

`references/config.md`, `references/benchmarks.md`, and `references/terminology.md` are loaded by multiple skills. Changes affect the whole plugin.

- `benchmarks.md` — add source and region tag to any new benchmark data
- `terminology.md` — keep definitions universal (not language or market specific)
- `config.md` — documents plugin adaptation rules, not a runtime config file

## Updating the version

1. Edit `version` in `.claude-plugin/plugin.json`
2. Update `CHANGELOG.md` with what changed and why
3. The marketplace (`theFudis/fudis-marketplace`) pins to `main` — push to main to ship

## Design principles

**Concise over complete.** The context window is shared with everything else. Every line in a SKILL.md has a cost.

**Global by default.** No hardcoded currency, language, or market-specific pricing. The plugin works for any restaurant in any country.

**One thing per skill.** Skills should do one thing well. If a skill is growing to cover multiple distinct use cases, split it.

**Progressive disclosure.** SKILL.md holds the workflow. Bulk content (examples, schemas, reference data) goes in `references/`. Claude loads reference files only when needed.

## Testing locally

```bash
# Validate the plugin manifest
claude plugin validate .

# Check the full component inventory and token cost estimate
claude plugin details fudis
```

## Submitting changes

Open a pull request against `main` on `theFudis/fudis-claude-plugin`. For new skills, include a brief description of the use case and which tool calls it makes.
