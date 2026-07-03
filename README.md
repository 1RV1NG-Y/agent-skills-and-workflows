# agent-skills-and-workflows

Skills and config I use with Claude Code and Codex, kept here so they're easy to share.

## Layout

- **`skills/`** — the skills in use.
  - `distill` — pull the useful information and the alpha out of any content (videos, articles, posts, PDFs, screenshots).
  - `alpha-extraction` — strict triage across many sources: keep only the edge-giving insights, most sources correctly yield nothing.
  - `twitter-x-extraction` — recover clean text, metadata, and quoted context from X/Twitter posts.
  - `codex-delegation` — route token-heavy legwork from Claude to gpt-5.5 via `codex exec`, saving the smarter model for judgment.
- **`reference/`** — Codex-authored takes on the same problems (`extract-useful-info`, `extract-alpha`). The `skills/` versions are the ones in use; these stay as reference.
- **`claude-md/`** — sections of my global `CLAUDE.md`, one file each.
  - `model-routing.md` — which model gets which kind of work.

## Using a skill

Copy its folder into your agent's skills directory (`~/.claude/skills/` for Claude Code). Each skill is a `SKILL.md`; most also carry `agents/openai.yaml` so they work with Codex too (`codex-delegation` doesn't — it's Claude-side by nature).
