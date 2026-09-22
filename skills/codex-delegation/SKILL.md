---
name: codex-delegation
description: Delegate transcript-heavy work from a GPT-5.6 Sol primary to GPT-5.6 Sol subagents at matched reasoning effort, with GPT-5.6 Luna reserved for strictly menial work. Use for broad codebase investigation, implementation from a clear contract, computer use, long verification or data analysis, or when the user asks to delegate, parallelize, use Codex, or save context.
---

# Delegation for GPT-5.6 Sol

Delegation buys context isolation and parallel execution; it does not transfer ownership of intent. The primary Sol scopes the work, defines shared contracts, handles judgment-heavy decisions, integrates the result, and verifies the claims.

## Delegate or keep inline

Delegate when the transcript would dwarf the answer: broad searches, independent implementation slices, browser or computer-use sessions, long verification output, bulk transformations, and data analysis.

Keep work inline when it is the top-level decomposition, a shared prerequisite, ambiguous or taste-heavy, or small enough that writing a complete handoff costs more than doing it. Never spawn one agent and sit idle behind it; fan out genuinely independent slices or continue useful work locally.

## Route models by task difficulty

Use the lowest effort that reliably covers the task:

| Selector | Use for |
|---|---|
| `openai-codex/gpt-5.6-sol:low` | Bounded mechanical work that still requires code comprehension |
| `openai-codex/gpt-5.6-sol:medium` | Default investigation, routine implementation, and verification |
| `openai-codex/gpt-5.6-sol:high` | Cross-file debugging, integration, difficult implementation, and substantive review |
| `openai-codex/gpt-5.6-sol:xhigh` | Hard architecture, security, underspecified reasoning, or taste-sensitive work that is genuinely safe to delegate |
| `openai-codex/gpt-5.6-sol:max` | Exceptional cases only; never the reflexive default when `xhigh` is sufficient |
| `openai-codex/gpt-5.6-luna:max` | Exact, reversible, menial collection or transformation with an obvious correct result |

Luna is not a cheaper general worker. Never give it design, debugging, security analysis, code review, ambiguous edits, or multi-file implementation. Prefer the `sonic` agent type for Luna-shaped work. A higher effort never compensates for an incomplete prompt.

Use the Task tool for normal delegation, specialist routing, and parallel slices. Use Eval's `agent()` bridge when an exact model/effort override or structured output is required:

```python
result = agent(prompt, model="openai-codex/gpt-5.6-sol:medium")
menial = agent(prompt, agent="sonic", model="openai-codex/gpt-5.6-luna:max")
```

Check what context the subagent inherits; explicitly supply any missing context, scope, constraints, and acceptance criteria. Pick the most specific agent type (`scout`, `designer`, `reviewer`, `librarian`, `sonic`) before falling back to the general worker.

## Write a complete handoff

State the unsaid and make success observable:

```text
Context: project purpose, absolute working path, relevant decisions and shared contracts
Target: exact files, symbols, or data; explicit non-goals
Change: what to investigate or implement, including required patterns and edge cases
Constraints: user work to preserve, commands not to run, and boundaries not to cross
Acceptance: observable behavior and the narrow proof to run
Report: files changed plus proof, or findings with file:line/source evidence
```

For read-first work, say `investigate and propose; change nothing`. Apply only after the proposal is accepted. Do not weaken the filesystem sandbox as a substitute for a clear prompt.

## Codex CLI fallback

Native OMP subagents are preferred for GPT-5.6 Sol/Luna. The local Codex CLI may expose a different model catalog; pin only a model verified as available there.

Run non-interactively with automatic approval while retaining the workspace sandbox:

```sh
codex -a never -s workspace-write exec --skip-git-repo-check \
  -m gpt-5.6-sol -c model_reasoning_effort=high \
  -C /abs/path/to/workdir -o /path/to/scratch/last-message.md "PROMPT" </dev/null
```

- `-a never` is the non-interactive auto-approval policy: approval prompts never stall the run and command failures return to the model.
- `-s workspace-write` keeps writes inside the workspace. Add a specific writable location with `--add-dir`; never use `--dangerously-bypass-approvals-and-sandbox` or `danger-full-access` as an automatic retry.
- `</dev/null` prevents waiting on stdin. `-o FILE` captures the final answer; use the harness process/job facility for long runs rather than shell backgrounding.
- Set `model_reasoning_effort` deliberately. Do not rely on the user's Codex default.
- Resume with the same policy: `codex -a never -s workspace-write exec resume --last "..."`.
- On a usage-limit error, do not retry-loop. Use a native subagent, continue inline, or report the reset time.

## Review delegated work

Verify the returned patch or claims against the workspace and run the narrow scenario that proves the requested behavior. If the result missed, tighten the contract and follow up with the same agent/session rather than starting over. Delegated output is evidence to inspect, not completion by itself.
