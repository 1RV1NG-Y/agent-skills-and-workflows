# agent-skills-and-workflows

Personal skills and configuration for Claude Code, Codex, and OMP, kept here so they're easy to review and share. Installed copies are the source of truth for actual behavior; project edits must be synced to the relevant harness to take effect.

## Layout

- **`skills/`** — the main skill versions, including additions awaiting installation in a harness.
  - `distill` — pull the useful information and the alpha out of any content (videos, articles, posts, PDFs, screenshots).
  - `alpha-extraction` — strict triage across many sources: keep only the edge-giving insights, most sources correctly yield nothing.
  - `twitter-x-extraction` — recover clean text, metadata, and quoted context from X/Twitter posts.
  - `codex-delegation` — delegate context-heavy work to Sol subagents at matched effort, with Luna `max` reserved for menial work. The primary owns intent, integration, and final review; handoffs account for the context each subagent inherits.
  - `gauntlet-loop` — refine artifacts through independent builder–critic cycles against an inspectable external quality bar.
  - `research-fast-moving-tech` — research current/bleeding-edge tech questions with fresh evidence and coverage audits, never trusting model memory as the search space.
- **`reference/`** — secondary extraction variants (`extract-useful-info`, `extract-alpha`) and archived Fable-era delegation/model-routing documents. These remain references even where a secondary version is installed in a harness.
- **`claude-md/`** — sections of my global `CLAUDE.md`, one file each.
  - `model-routing.md` — which model gets which kind of work.
- **`omp/`** — copies of OMP-specific global instructions.
  - `RULES.md` — exact copy of `~/.omp/agent/RULES.md`, containing the deletion-confirmation policy.

## Using a skill

Copy the full skill folder into the target harness's skills directory, such as `~/.claude/skills/` or `~/.codex/skills/`. Each skill has a `SKILL.md`; most also carry `agents/openai.yaml` for Codex display metadata and a suggested prompt. Delegation currently describes OMP-native orchestration with a Codex CLI fallback.

OMP can load the installed Claude and Codex skills when those sources are enabled in its configuration. This repository does not automatically configure or install skills in any harness.

`claude-md/model-routing.md` mirrors the live global `~/.claude/CLAUDE.md`, excluding its provenance note. Keep it synchronized with the delegation skill when routing policy changes. `omp/RULES.md` is a stored copy of the live OMP rules. There is no repository-wide `CLAUDE.md` or `AGENTS.md` here.
