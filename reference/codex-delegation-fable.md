---
name: codex-delegation
description: Delegate token-heavy legwork to gpt-5.5 through the Codex CLI (codex exec) or to Claude subagents, so Fable's context and limits are spent on judgment. Use when the work means sweeping a codebase, bulk implementation from a clear spec, computer use, long verification or data analysis — or when the user says "use codex", "delegate this", or "save tokens".
---

# Codex delegation

gpt-5.5 via Codex has much higher limits than Fable and handles whole-codebase context well, but it is literal: it does exactly what the prompt says and nothing more. The trade is always the same — write a complete spec, let it do the legwork, review what comes back.

## Delegate or keep inline

Delegate when the transcript would dwarf the answer: codebase-wide investigation, implementation from a spec you can state completely, computer use, verification runs, bulk edits, data analysis.

Keep inline when the task is ambiguous, needs judgment or taste, or is small enough that writing the spec costs more than doing the work.

## Write the prompt

Codex sees nothing of your conversation and fills no gaps — say the unsaid. Cover:

```
Context: what the project is and the absolute working path
Task: exactly what to do or find
Boundaries: what not to touch
Report: what to output when done (files changed + summary, or answer with file:line evidence)
```

When you want eyes on the work before anything changes, get that by prompting, not sandbox flags: first run "investigate and propose a plan; change nothing yet", review it, then apply with `codex exec resume --last "apply the plan"`.

## Run it

```
codex exec --dangerously-bypass-approvals-and-sandbox --skip-git-repo-check \
  -C /abs/path/to/workdir -o /path/to/scratch/last-message.md "PROMPT" </dev/null
```

- If `codex` isn't on PATH (typical on Windows), the desktop app bundles the CLI — call it as `~/.codex/.sandbox-bin/codex.exe`. Same flags, same behavior.
- Full permissions always — that's the user's standing choice. Exec mode never shows approval prompts, and the bypass flag means nothing stalls or silently fails. Caution comes from the prompt (two-phase above).
- `</dev/null` keeps it from waiting on stdin.
- `-o FILE` writes codex's final message to a file. For long runs: launch in the background, send stdout to a log, and read just the `-o` file when it finishes.
- If codex's writes get blocked, that's the harness's own Bash sandbox, not codex — rerun the Bash call with the sandbox disabled.
- Effort defaults to xhigh (user config). For mechanical bulk work, `-c model_reasoning_effort=medium` is faster and plenty.
- Follow-up in the same codex session: `codex exec resume --last "..."`.
- Usage-limit error: it fails fast and names the reset time. Don't retry-loop — do the work inline or report the reset time to the user.

## Review what comes back

Read the diff or spot-check the claims against the files before accepting. If it missed, the spec had a gap: tighten it and rerun (resume), or escalate to doing it yourself.

## Claude subagents (Agent tool)

- opus: creative or taste-heavy work, reading between the lines. Package the context it needs into the prompt; it is not reliable at foraging for its own.
- sonnet: plumbing only — e.g. a disposable wrapper that babysits parallel codex runs and returns digested results.
- fable: subproblems that genuinely need it. Effort high, not xhigh.
- A direct Bash call to codex beats a wrapper agent unless you're fanning out several runs in parallel or the raw output needs digesting before it reaches your context.
