> Copy of `~/.claude/CLAUDE.md` (the live one is the source of truth). Companion mechanics: `skills by claude/codex-delegation/`. Written 2026-07-03.

# Model routing — delegate the legwork

Fable is the smartest model available and the quickest to hit limits. Spend it on judgment: understanding intent, design, review. Push token-heavy legwork to cheaper agents and have them report back. Mechanics live in the codex-delegation skill.

| agent | use for | keep in mind |
|---|---|---|
| gpt-5.5 via `codex exec` (xhigh) | codebase-wide investigation, bulk implementation from a clear spec, computer use, verification runs, data analysis | Literal and robotic: does exactly what the prompt says and nothing more — but does it correctly given a detailed spec. Handles whole-codebase context well. Much higher limits than Claude models. |
| opus 4.8 subagent | creative or taste-heavy work; tasks where what's left unsaid matters | Not reliable at gathering its own context — package what it needs into the prompt. |
| sonnet subagent | disposable plumbing only, e.g. babysitting parallel codex runs | Never for thinking. |
| fable subagent | subproblems that genuinely need the smartest model | Effort high, not xhigh. |

Rules:

- Delegate when the work's transcript would dwarf its answer: lots of file reads, long build or test output, browser sessions. Keep it inline when the task is ambiguous, judgment-heavy, or small enough that writing the spec costs more than the work.
- Run codex with all permissions (`--dangerously-bypass-approvals-and-sandbox`), always. When caution is wanted, get it by prompting (e.g. "investigate and propose, change nothing yet"), never by sandbox flags.
- Review delegated work before accepting it. Reading a diff is cheap; writing it is what was offloaded.
- If codex answers with a usage-limit error, don't retry-loop: do the work inline or tell the user when the window resets.
