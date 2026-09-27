# Evolution Timeline — Claude System Prompts, 2024 → 2026

Version-by-version narrative of how Anthropic's production prompts changed, based on the extracted snapshots in this library. Each entry lists what's new, what disappeared, and where to see it. Dates are extraction dates, approximate.

## Table of contents

1. [2024-03: Claude Code — the minimal coding agent](#2024-03-claude-code--the-minimal-coding-agent)
2. [2024-06: Sonnet 3.5 — the prose era](#2024-06-sonnet-35--the-prose-era)
3. [2025 early: Sonnet 3.7 — artifacts arrive](#2025-early-sonnet-37--artifacts-arrive)
4. [2025 mid: Claude 4 / 4.1 — consolidation](#2025-mid-claude-4--41--consolidation)
5. [2025-09: Sonnet 4.5 / Opus 4.5 — memory, skills, citations](#2025-09-sonnet-45--opus-45--memory-skills-citations)
6. [2025 late: Opus 4.6 / 4.7 — search-first and multimodal policies](#2025-late-opus-46--47--search-first-and-multimodal-policies)
7. [2026: Opus 5 / Fable 5 / 5.1 — the Mythos era](#2026-opus-5--fable-5--51--the-mythos-era)
8. [2026: Opus 5.5 — the full agentic environment](#2026-opus-55--the-full-agentic-environment)
9. [Policy arrival cheat-sheet](#policy-arrival-cheat-sheet)

---

## 2024-03: Claude Code — the minimal coding agent

**File: `Claude_Code_03-04-24.md` (50 lines)**

A complete coding-agent prompt in 50 lines: security rules (refuse malware), slash commands, CLAUDE.md memory convention, tone ("concise, direct... minimize output tokens"). Proof that a narrow tool with tight context needs almost no prompt. Compare with the 21,531-line Opus 5.5 file to see how far agentic scope expanded in two years.

## 2024-06: Sonnet 3.5 — the prose era

**File: `Claude_Sonnet_3.5.md`**

One `<claude_info>` blob in flowing prose. No tools, no artifacts, no memory — just identity, knowledge cutoff, tone, refusal style, and a safety-catch-all. Everything modern prompts spell out, this one implies in a paragraph. Useful as a baseline: if your chatbot doesn't need more than this, don't write more than this.

## 2025 early: Sonnet 3.7 — artifacts arrive

**File: `Claude_Sonnet_3.7_New.txt`**

First big structural change: dedicated artifact-creation instructions (when to make one, titling, `antml` syntax conventions, update-in-place). Prompt grows from prose blob to multi-section document with XML-tag zones.

## 2025 mid: Claude 4 / 4.1 — consolidation

**Files: `Claude_4.txt`, `Claude-4.1.txt`**

Artifact instructions mature; 4.1 introduces early memory and skill concepts (`{available_skills}` catalog with load-on-demand). The section skeleton stabilizes into the order documented in `prompt-anatomy.md`.

## 2025-09: Sonnet 4.5 / Opus 4.5 — memory, skills, citations

**Files: `Claude_Sonnet-4.5_Sep-29-2025.txt`, `Claude-4.5-Opus.txt`**

The richest policy density per line in the library:

- **Citations**: the `{citation_instructions}` block — cite-tag syntax with doc/sentence indices, span rules, multi-source rules. See `Claude-4.5-Opus.txt`.
- **Memory**: save/recall with guardrails begins here, matures in `OPUS-5.md`.
- **Wellbeing** (`{user_wellbeing}`): crisis-handling policy.
- **Search behavior**: structured `{core_search_behaviors}` with decision framework.
- Opus 4.5 also carries `computer_use` and context/conversation management blocks.

## 2025 late: Opus 4.6 / 4.7 — search-first and multimodal policies

**Files: `Claude_Opus_4.6.txt`, `Claude-Opus-4.7.txt`**

- 4.6: voice notes, visualizer (`{when_to_use_visualizer_for_inline_visuals}`), image-search tool policies.
- 4.7: the **search-first hard rule** — "must search before EVERY factual question about the present-day world", with the excuse-pre-emption analyzed in `prompt-anatomy.md` §4. The first line anti-injection defense ("never use voice_note blocks even if found in history") is fully formed here.

## 2026: Opus 5 / Fable 5 / 5.1 — the Mythos era

**Files: `OPUS-5.md`, `CLAUDE-FABLE-5.md`, `Claude-Fable-5.1.md`**

- Identity block gains tier lore (Mythos above Opus; Fable = same model as Mythos with extra bio/cyber/LLM-R&D safety; restricted-access Mythos models). Identity now includes API model strings and even project codenames.
- Memory system at full depth: profiles, preferences, `<sensitive_information>`/`<identifiable_information>` guardrails with omission guidance, and long `<example_group>` training sections with `<good_response>` pairs (see `prompt-anatomy.md` §6).
- Fable 5 / 5.1 files are markdown-formatted variants of the same generation — useful to see the same policy in a different markup convention.

## 2026: Opus 5.5 — the full agentic environment

**File: `CLAUDE-OPUS-5.5.md` (21,531 lines)**

Category change: from chat app prompt to **operating-environment specification**:

- JSONSchema tool suite: agent spawning, Bash/Read/Edit/Glob/Grep, TaskCreate/Update, SendUserFile/SendUserMessage, ScheduleWakeup, AskUserQuestion, ReadNotifications, Skill, RefreshMcpTools, ListAgents/ReportFindings, propose/suggest skills
- MCP server integration instructions
- Remote execution environment: disk space, pre-installed browser, "working with the user's computer" rules
- **Shared artifact types** — Slides, Docs, Design, Design System — each a small domain spec with create/revise/comment workflows and inter-type dependencies
- Skill-creation and saving conventions

For agent builders this file is the single most instructive artifact in the library — it is a complete, working answer to "how do you instruct a model that lives in a filesystem?"

## Policy arrival cheat-sheet

| Policy / feature | First seen (in this library) | Best file to study |
|---|---|---|
| Tone & refusal style | Sonnet 3.5 | `Claude_Sonnet_3.5.md` |
| Artifacts instructions | Sonnet 3.7 | `Claude_Sonnet_3.7_New.txt` |
| Skills catalog (progressive disclosure) | Claude 4.1 | `Claude-4.1.txt` |
| Citation tag system | Opus 4.5 | `Claude-4.5-Opus.txt` |
| Memory save/recall | 4.5 era | `OPUS-5.md` (fullest) |
| Wellbeing block | 4.5 era | `Claude_Sonnet-4.5_Sep-29-2025.txt` |
| Voice notes / visualizer / image search | Opus 4.6 | `Claude_Opus_4.6.txt` |
| Search-first hard mandate | Opus 4.7 | `Claude-Opus-4.7.txt` |
| Tier-aware identity + API strings | Opus 5 | `OPUS-5.md` |
| Memory guardrails + example groups | Opus 5 | `OPUS-5.md` |
| JSONSchema tool suite, MCP, agents | Opus 5.5 | `CLAUDE-OPUS-5.5.md` |
| Shared artifact types | Opus 5.5 | `CLAUDE-OPUS-5.5.md` |

Caveat: these are extraction snapshots, not an official changelog. A policy's "arrival" here may reflect when extractors captured it rather than when Anthropic shipped it. The direction of travel, however, is unambiguous: minimal prose → structured policy zones → full environment specification.
