---
name: gauntlet-loop
description: Run adversarial builder–critic refinement against a concrete external quality bar. Use when the user asks for a Gauntlet Loop, independent critics, blind comparison, iterative improvement until a reference is matched, or a high-quality artifact developed by multiple agents. Suitable for visual work, code, performance, writing, research, and other outputs that can be inspected or measured.
---

# Gauntlet Loop

Produce an artifact through repeated, externally grounded builder–critic cycles. The invariant is:

> concrete bar → real artifact → independent judgment → largest gap → repair → repeat

This is an orchestration skill, not permission to create an undirected agent swarm. The primary agent owns the goal, decomposition, shared contracts, integration, and final verdict.

## Non-negotiable invariants

1. **Use an inspectable external bar.** References, tests, benchmarks, examples, or measurable constraints—not “excellent,” “production-ready,” or the builder's opinion.
2. **Judge the real artifact.** Critics inspect pixels, the running product, test behavior, measurements, finished prose, or source evidence. They never grade a builder-written summary.
3. **Separate builder and critic.** A critic starts in fresh context without the builder's rationale or history.
4. **Return the largest evidenced gap.** One root problem and an observable acceptance condition beat a long unranked issue list.
5. **Parallelize only independent work.** Coupled concerns get one owner or a sequential integration pass.
6. **Do not predeclare success.** Report `met`, `partial`, or `missed` from evidence.
7. **Keep looping while the evaluation is valid and meaningful improvement is possible.** Do not use an arbitrary number of polish rounds.

## Intake

Extract or establish:

- **Goal:** the artifact or behavior to produce.
- **Bar:** the reference, test, benchmark, or comparison target.
- **Constraints:** technology, compatibility, safety, ownership, style, and non-goals.
- **Evaluation adapter:** how a fresh critic can inspect and compare the real output.
- **Progress artifact:** optional ledger, report, screenshots, benchmark history, or preview page.

If the user supplies no bar, choose the strongest obvious one from existing project evidence. Ask only when plausible bars have materially different tradeoffs. If no valid bar exists, first create or source one; do not begin cosmetic iteration against a vague standard.

### Suitability gate

Use a Gauntlet Loop when quality is observable and repeated comparison can improve it. Do not create agent overhead for a tiny deterministic edit. For a small task, execute normally and run one independent verification pass.

## Phase 1 — Ground the bar and evaluation

Before delegating builders:

1. Inspect the existing artifact, project conventions, and available references.
2. Define comparison conditions: inputs, viewport, seed, environment, dataset, workload, or rubric.
3. Make evaluation reproducible where the modality permits it.
4. Capture the existing baseline when modifying an existing artifact.
5. Record the bar and pass condition in one concise contract.

A score is supporting data, not the verdict. Evidence, winner, largest gap, and acceptance condition matter more.

### Evaluation adapters

Choose the adapter that inspects the actual outcome:

- **Visual/UI:** drive the real application; capture consistent screenshots or video; compare at the same viewport/state; use blind A/B when practical.
- **Correctness/API:** reproduce behavior; use existing tests plus the real invocation path; compare contract outcomes and failure behavior.
- **Performance:** exercise a representative moving workload; report distributions and worst cases, not only averages; distinguish cold and warm behavior when relevant.
- **Writing:** compare finished passages against reference material for clarity, structure, density, factuality, and audience fit.
- **Research:** compare claims against primary sources, coverage requirements, counterevidence, and reproducibility of the search path.
- **Security/reliability:** use a threat or failure model, adversarial cases, recovery checks, and observable invariants.

If the evaluation itself drifts or produces inconsistent results, stop the improvement loop and repair determinism first.

## Phase 2 — Decompose by independence and coupling

The primary agent—not a planning subagent—maps the work into the smallest pieces that can be built and judged independently.

For every slice, define:

- Exact owner and artifact boundaries.
- Shared interfaces and invariants.
- Inputs and dependencies.
- The slice-specific bar.
- The critic's inspection method.
- Observable acceptance criteria.

Classify each relationship:

- **Independent:** safe for one batched fan-out.
- **Ordered:** downstream work requires an upstream contract or artifact.
- **Coupled:** changes interact strongly; assign one owner or handle sequentially.

Do not use directory boundaries as proof of independence. Rendering, lighting, state, data models, public APIs, and shared prose voice often cross file boundaries.

## Phase 3 — Build

This skill explicitly requires subagents for non-trivial builder–critic separation.

- Scope and contracts come first; then dispatch all genuinely independent builders in one Task batch.
- Give each builder complete context, exact ownership, the bar, and acceptance criteria.
- Builders investigate and implement their slice in one pass when practical.
- Preserve one builder owner per slice across repair rounds when that agent remains available.
- Shared prerequisites and cross-cutting integration remain with the primary agent or one designated owner.
- Delegated builders skip project-wide formatting, linting, and test suites; the primary performs integration verification once the wave lands.

For visual creation, use a design-capable builder. For routine code, use the normal implementation agent. Match the agent to the artifact; do not use a read-only scout as a builder.

## Phase 4 — Fresh adversarial critique

After builders produce inspectable artifacts, dispatch fresh critics. A critic must not be the builder and must not receive the builder's rationale.

Use a reviewer for code, correctness, security, or substantive quality review; use a designer for visual comparison. Give the critic:

- Goal and constraints.
- External bar and comparison conditions.
- Location of the real artifact.
- Slice boundary or whole-artifact scope.
- Required structured verdict.

Require this report shape:

```yaml
winner: reference | ours | tie
status: met | partial | missed
score: 0-10            # optional; secondary to evidence
evidence:
  - concrete observable difference
largest_gap: one highest-leverage root problem
acceptance_condition: observable condition for the next round
confidence: low | medium | high
```

Critics must:

- Inspect or run the artifact themselves.
- Prefer measurements and visible behavior over labels.
- Distinguish symptoms from root causes.
- Avoid broad redesign when one gap dominates.
- State uncertainty when the comparison is weak.

## Phase 5 — Repair loop

For every slice that loses:

1. Give the owning builder only the critic's evidence, largest gap, and acceptance condition.
2. Have the builder diagnose the mechanism before changing the artifact.
3. Apply the smallest root-cause repair that can close the gap.
4. Re-run the slice's real evaluation.
5. Send the result to a new fresh critic.

Do not let the builder argue with the verdict in place of changing or measuring the artifact.

If the same gap survives repeated rounds, do not stack cosmetic patches. Pause that slice and do one of:

- Measure the underlying mechanism.
- Split the gap into smaller independently testable causes.
- Reclassify supposedly independent work as coupled.
- Assign one sequential owner across the coupled concern.
- Repair or replace an invalid evaluation method.

Continue once the root cause or evaluation is grounded.

## Phase 6 — Integration and smoothing

After a major parallel wave, one owner inspects the complete artifact.

The integration pass:

- Resolves conflicts between locally successful changes.
- Checks shared interfaces and global invariants.
- Smooths visual, behavioral, or prose inconsistency without redesigning successful parts.
- Re-runs the whole-artifact comparison under the original conditions.
- Routes newly exposed slice gaps back through fresh critics when needed.

Never have multiple independent agents simultaneously tune one tightly coupled global concern.

## Phase 7 — Final verification

Completion requires end-to-end evidence:

1. Run the real artifact or scenario.
2. Reproduce the final comparison under controlled conditions.
3. Confirm every requested acceptance criterion.
4. Check that integration did not regress previously winning slices.
5. Record the final honest verdict: `met`, `partial`, or `missed`.

Do not convert `partial` into `met` because the result is impressive, expensive, or much improved.

## Progress tracking

For long runs, maintain a compact ledger or live artifact containing:

- Goal and bar.
- Decomposition and owners.
- Baseline evidence.
- Each round's winner, largest gap, and change.
- Current whole-artifact verdict.

Update it from observed results, not agent status prose. Keep it readable without interrupting builders for narrative reports.

## Stop conditions

Stop when one of these is true:

- The final fresh critic says our artifact wins or the measurable bar is satisfied, and end-to-end verification agrees.
- The user stops the run.
- A required external prerequisite is unavailable after all reachable sources and tools are exhausted.
- Further looping cannot be evaluated meaningfully; report the invalid bar or harness instead of inventing progress.

A hard reference may remain unbeaten. In that case, ship only if the user's requested deliverable is otherwise complete, label the quality target `partial` or `missed`, and name the largest remaining gaps.

## Final response

Lead with the verdict. Include:

- Goal and bar used.
- What was built or changed.
- Builder/critic rounds only at the level needed to explain decisive changes.
- Final observed evidence and verification.
- `met`, `partial`, or `missed`.
- Largest remaining gaps if not met.
- Paths or links to artifacts and progress records.

## Provenance

Inspired by Matt Shumer's Claude of Duty process and his retrospective description of the Gauntlet Loop:

- https://somethingbig.ai/gauntlet-loop
- https://github.com/mshumer/Claude-of-Duty
- https://github.com/mshumer/Claude-of-Duty/blob/main/prompt.md
- https://github.com/mshumer/Claude-of-Duty/blob/main/ARCHITECTURE.md

The published game prompt is a seed prompt, not a complete execution transcript. Do not imply that downstream agent prompts, system instructions, or the full run history are available.
