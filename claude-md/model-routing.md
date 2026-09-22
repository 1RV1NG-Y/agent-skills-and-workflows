> Copy of `~/.claude/CLAUDE.md` (the live one is the source of truth). Companion mechanics: `skills/codex-delegation/`. Updated 2026-09-22.

# Model routing — delegate the legwork

The primary GPT-5.6 Sol owns user intent, top-level decomposition, shared contracts, integration, and final review. Delegate work whose transcript would dwarf its answer; the gain is isolated context and parallel execution, not access to a smarter model. Mechanics live in the `codex-delegation` skill.

| agent/model | use for | keep in mind |
|---|---|---|
| Sol `low` | bounded mechanical work that still needs code comprehension | Exact scope and an obvious proof |
| Sol `medium` | routine investigation, implementation, verification, and data analysis | Default delegated worker |
| Sol `high` | cross-file debugging, integration, difficult implementation, substantive review | Use when medium risks missing interactions |
| Sol `xhigh` | hard architecture, security, underspecified reasoning, or taste-sensitive work | Keep top-level judgment with the primary; `max` is exceptional |
| Luna `max` via `sonic` | exact, reversible, menial collection or transformation | Never design, debug, review, secure, or own ambiguous/multi-file changes |

Rules:

- Delegate when the transcript would dwarf the answer: broad file reads, long build or verification output, browser sessions, independent implementation slices, and bulk data work. Keep work inline when it is ambiguous, judgment-heavy, a shared prerequisite, or cheaper to do than to specify.
- Prefer native OMP Task subagents. Match Sol effort to difficulty; use Eval's `agent()` only when an exact model/effort override or structured output is required. Luna is a narrow menial worker, not a general cheaper default.
- Scope before spawning. Fan out independent slices together; never spawn one agent and wait idle. Check what context the subagent inherits; explicitly supply any missing context, scope, constraints, and acceptance criteria.
- For Codex CLI fallback, use automatic approval with the workspace sandbox: `codex -a never -s workspace-write exec ...`. Never use `--dangerously-bypass-approvals-and-sandbox` or `danger-full-access` as an automatic retry; use a narrow `--add-dir` when another writable path is required.
- Review delegated changes and verify their claims before accepting them. If a usage limit fails fast, do not retry-loop; switch route, continue inline, or report the reset time.
