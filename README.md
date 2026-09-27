# claude-system-prompts

An [Agent Skill](https://agentskills.io) that packages **15 extracted real Anthropic production system prompts** — Claude Sonnet 3.5 (Jun 2024) → Opus 5.5 (2026) — with structural analysis and an evolution timeline.

> "In order to trust the output, one must understand the input."

## What's inside

```
├── SKILL.md                     # Skill entry: catalog, navigation, 4 workflows
└── references/
    ├── prompt-anatomy.md        # Structural analysis + 10 stealable writing techniques
    ├── evolution-timeline.md    # 2024→2026 version-by-version narrative + policy arrival table
    └── prompts/                 # The 15 original extracted files (unmodified)
```

### The prompt collection

| Era | Files |
|---|---|
| 2024 minimal | `Claude_Code_03-04-24`, `Claude_Sonnet_3.5` |
| 2025 artifacts & memory | `Claude_Sonnet_3.7_New`, `Claude_4`, `Claude-4.1`, `Claude_Sonnet-4.5`, `Claude-4.5-Opus`, `Claude_Opus_4.6`, `Claude-Opus-4.7` |
| 2026 Mythos & agentic | `OPUS-5`, `CLAUDE-FABLE-5`, `Claude-Fable-5.1`, `CLAUDE-OPUS-5.5` (21,531 lines) |
| Special-purpose | `Claude-Design-Sys-Prompt` (design agent), `UserStyle_Modes` (3 selectable personas) |

## What it's for

- **Writing system prompts** — ground your work in production examples instead of inventing patterns: identity blocks, tone policy, tool mandates, refusal style
- **Building AI agents** — JSONSchema tool suites, multi-agent orchestration, memory with privacy guardrails, skills/progressive disclosure (from the 21k-line Opus 5.5 environment spec)
- **Research & transparency** — which prompt introduced citations, anti-injection defenses, search-first mandates, and how prompts grew 400× in two years

## Usage

**As a skill** (Claude / Claude Code / any Agent Skills runtime): point your skills directory at this repo, or package it with your skill tooling (the folder follows the [Agent Skills](https://agentskills.io) spec: `SKILL.md` frontmatter + bundled `references/`).

**As a reading library**: start with `references/prompt-anatomy.md`, then `references/evolution-timeline.md`, then open the two endpoints for contrast — `Claude_Sonnet_3.5.md` (minimal) vs `CLAUDE-OPUS-5.5.md` (maximal).

## Provenance & disclaimer

All prompt files are sourced from the public repository [elder-plinius/CL4R1T4S](https://github.com/elder-plinius/CL4R1T4S) (sourced 2026-09-28), which collects community-extracted system prompts for AI transparency research.

- Authenticity is **not vendor-verified**; dates are extraction dates, approximate
- Content may have been revised by Anthropic after extraction
- Use for study, education, and design inspiration — don't present quotes as verbatim current production text
- This repository is educational; prompts remain the property of their creators and are reproduced here under fair-use transparency research conventions
