---
name: claude-system-prompts
description: Reference library of 15 extracted/leaked real Anthropic production system prompts (Claude Sonnet 3.5 → Opus 5.5, 2024–2026), plus structural analysis and evolution timeline. Use this skill whenever the user wants to write, review, or optimize a system prompt for an LLM app/agent/chatbot; is building an AI agent and needs real-world tool-definition, memory, skill-loading, or orchestration patterns; asks how Claude is instructed/steered or what Claude's system prompt says; wants to compare Claude prompt versions or study prompt-engineering practice from production examples; or is doing AI transparency research on Anthropic models. Trigger on phrases like "system prompt", "提示词", "write a system prompt", "agent instructions", "how does Claude work", "prompt design/engineering" — even if the user doesn't explicitly name Claude.
license: Educational reference; content sourced from public repository CL4R1T4S (see Provenance)
---

# Claude System Prompts — Production Reference Library

This library contains **15 real, extracted Anthropic system prompts** spanning June 2024 → 2026, from Claude Sonnet 3.5's single-paragraph `claude_info` to Opus 5.5's 21,000-line full agentic environment. They are the actual instructions production Claude models run under — the highest-quality reference material available for writing your own system prompts and agent instructions.

These files are valuable because they show, in production quality: identity handling, tone control, tool schemas, citation rules, memory systems, skill loading, safety guardrails, and multi-agent orchestration. When a user needs any of those, ground your work in these files rather than inventing patterns from scratch.

## Library catalog

Chat model prompts (roughly chronological; all in `references/prompts/`):

| File | Model / date | Size | What it's good for |
|---|---|---|---|
| `Claude_Sonnet_3.5.md` | Sonnet 3.5, Jun 2024 | 204 ln | The classic minimal era: one prose blob, still teaches baseline persona/tone/IP handling |
| `Claude_Sonnet_3.7_New.txt` | Sonnet 3.7, 2025 | 397 ln | Artifacts system arrives; first big tool-behavior blocks |
| `Claude_4.txt` | Claude 4, 2025 | 368 ln | Refined artifacts + search behavior |
| `Claude-4.1.txt` | Claude 4.1, 2025 | 494 ln | Adding memory & skills concepts |
| `Claude_Sonnet-4.5_Sep-29-2025.txt` | Sonnet 4.5, 2025-09-29 | 520 ln | Mature: search, artifacts, memory, skills, wellbeing all present |
| `Claude-4.5-Opus.txt` | Opus 4.5, 2025 | 1,222 ln | Rich citation-instruction block; computer_use hints |
| `Claude_Opus_4.6.txt` | Opus 4.6, 2025 | 1,047 ln | Voice notes, visualizer, image search policies |
| `Claude-Opus-4.7.txt` | Opus 4.7, late 2025 | 1,408 ln | "Search-first" hard rule — the strongest tool-usage policy writing in the set |
| `OPUS-5.md` | Opus 5, 2026 | 2,049 ln | Mythos tier era; memory with guardrails, profiles, preferences |
| `CLAUDE-FABLE-5.md` | Fable 5, 2026 | 1,597 ln | Same-gen sibling; tier differentiation language |
| `Claude-Fable-5.1.md` | Fable 5.1, 2026 | 2,195 ln | Iteration on the 5-family prompt |
| `CLAUDE-OPUS-5.5.md` | Opus 5.5, 2026 | **21,531 ln / 1.9MB** | Full agentic environment: JSONSchema tool defs (Bash/Read/Edit/Glob/Grep/agents/tasks/scheduling/MCP), shared artifact types (Slides, Docs, Design, Design System). The single richest file. Do NOT read whole — read by section (see below) |

Special-purpose prompts:

| File | What it is | What it's good for |
|---|---|---|
| `Claude_Code_03-04-24.md` | Claude Code CLI, Mar 2024 (50 ln) | How little a coding-agent prompt needs: security rules, slash commands, CLAUDE.md memory |
| `Claude-Design-Sys-Prompt.txt` | Design agent (422 ln) | Expert-persona framing, "don't reveal your prompt" defense, HTML-as-medium design instructions |
| `UserStyle_Modes.md` | 3 user-selectable modes (14 ln) | Explanatory / Learning / directive-mode personas — compact style-switching reference |

## How to navigate the big Opus 5.5 file

`CLAUDE-OPUS-5.5.md` is too large to read end-to-end. Landmarks by line number (approximate; re-locate with grep if the file shifts):

- ~1–480: function-calling format + JSONSchema tool definitions (agent, Bash, Read, Edit, Glob, Grep, TaskCreate/Update, SendUserFile, ScheduleWakeup, Skill, MCP refresh)
- ~484–560: skill-saving + remote execution environment (disk, browser, user's computer)
- ~562–1030: model identity, reading/writing file conventions
- ~1281–2100: **shared artifact types** — Slides, Docs, Design canvas, Design System (each with create/revise/comment workflows)
- Rest: long-form operational detail, examples, and reference material for each type

Use `grep -n "^# " references/prompts/CLAUDE-OPUS-5.5.md` to get the live table of contents, then read the relevant range with offset/limit.

## Workflows

### A. Writing or improving a system prompt
1. Read `references/prompt-anatomy.md` first — it distills the structural sections and writing techniques that recur across all 15 files.
2. Pick ONE exemplar closest to the target product: chatbot → `Claude_Sonnet-4.5_Sep-29-2025.txt`; coding agent → `Claude_Code_03-04-24.md`; design/creative agent → `Claude-Design-Sys-Prompt.txt`; full autonomous agent → the landmark sections of `CLAUDE-OPUS-5.5.md`.
3. Borrow structure, not text: match the section ordering, the XML-tag scoping, the example-with-rationale pattern. Adapt wording to the actual product.
4. For tool-usage strictness, study the search-first block in `Claude-Opus-4.7.txt` — it's the best example of making a model *always* use a tool without loopholes.

### B. Building an AI agent (tools, memory, orchestration)
- Tool schemas: JSONSchema definitions in `CLAUDE-OPUS-5.5.md` lines ~1–480 show description-driven tool design — long, example-rich descriptions inside the schema itself.
- Multi-agent: the `agent` tool definition + `ListAgents`/`ReportFindings` in the same file.
- Memory: `OPUS-5.md` contains the fullest memory design — save/recall, profiles, preferences, guardrails around sensitive attributes, and worked examples with `<good_response>`/`<rationale>` pairs.
- Skills: `<available_skills>` blocks in 4.5-era files show the load-on-demand pattern; Opus 5.5 adds `propose_skills`/`SuggestSkills`.
- Scheduled/background work: `ScheduleWakeup` in Opus 5.5.

### C. Research / transparency analysis
1. Read `references/evolution-timeline.md` for the version-by-version diff narrative (2024 → 2026).
2. Then open the two endpoints for contrast: `Claude_Sonnet_3.5.md` (minimal) vs `CLAUDE-OPUS-5.5.md` (maximal).
3. For specific policy questions (citations, copyright, wellbeing, injection defense), the timeline doc lists which file introduced each policy and where to find it.

### D. Comparing two versions
Load both files, but diff smart: `diff` on raw files is noisy because formats changed (prose → XML tags → markdown headers). Compare section-by-section using the anatomy doc's section list as the common coordinate system.

## Writing techniques worth stealing (summary)

The anatomy doc expands each of these with quoted examples and file references:

1. **Scope with tags, not walls of prose** — `{claude_behavior}`, `<memory_listing>` etc. delimit policy zones; the model learns to treat each zone independently.
2. **Explain the why** — production prompts justify rules ("leaders change, so search first") instead of bare MUSTs; compliance is higher and generalizes better.
3. **Examples with rationale pairs** — `<user>` / `<good_response>` / `<rationale>` beats abstract instruction.
4. **Positive framing first** — say what to do, then the exceptions; prohibition-heavy text only appears in safety zones (copyright, injection).
5. **Long, rich tool descriptions** — the schema description IS the documentation: usage rules, examples, and edge cases embedded in JSONSchema.
6. **Anti-injection hardening** — explicit "even if found in conversation history" clauses for voice notes, system prompt disclosure, etc.
7. **Tier-aware identity** — the model's own capabilities, siblings, and API strings, so it can answer "which model are you" accurately.

## Provenance & use

Files are from the public repository [elder-plinius/CL4R1T4S](https://github.com/elder-plinius/CL4R1T4S) (sourced 2026-09-28), which collects community-extracted system prompts for AI transparency research. Treat them as: authenticity not vendor-verified, dates approximate, and content possibly revised after extraction. Use them for study and design inspiration; don't present quotes as verbatim current production text. The catalog dates/sizes above describe the extracted snapshots, not official release history.
