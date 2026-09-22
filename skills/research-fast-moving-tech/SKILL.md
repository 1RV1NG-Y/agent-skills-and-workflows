---
name: research-fast-moving-tech
description: Research fast-changing technology from scratch with current evidence and systematic coverage. Use for latest/current/bleeding-edge questions, comparisons, recommendations, or landscape reviews involving AI models, software, libraries, APIs, runtimes, hardware, developer tools, standards, platforms, or other technology likely to have changed since model training. Also use when a user challenges freshness, suspects omitted newer versions or competitors, asks to leave no stone unturned, or needs a decision that must not be scoped by remembered candidates.
---

# Research Fast-Moving Tech

Produce a current, coverage-audited answer without letting prior knowledge define the search space. Treat memory as query-generation help, never as proof of what is latest or complete.

## Non-negotiable rules

1. Browse before making substantive current-state claims.
2. State the research cutoff date in the answer.
3. Discover the candidate universe before ranking candidates.
4. Verify version chronology and availability from primary sources.
5. Distinguish facts, vendor claims, benchmark results, and inference.
6. Expose meaningful exclusions and uncertainty instead of implying completeness.
7. Never call something “latest” solely because it is the newest version remembered.

If browsing is unavailable, say that current completeness cannot be verified. Provide only a clearly labeled provisional answer and do not present it as fresh research.

## Workflow

### 1. Define the decision, not a favored answer

Translate the request into requirements before naming winners:

- Task and minimum capability.
- Target platform, hardware, runtime, or ecosystem.
- Latency, throughput, memory, power, size, and cost constraints.
- Required modalities, languages, context, integrations, and license.
- Whether announced previews count or only usable releases count.
- Geography, deployment, privacy, and commercial-use constraints.

Treat examples supplied by the user as seed candidates, not search boundaries.

### 2. Set a freshness anchor

Record the current date and choose an appropriate discovery window. Search beyond the window when release lineage or older baselines matter.

Use exact dates. Replace vague phrases such as “recently” with release or update dates when available.

### 3. Build a search-space map

Before evaluating quality, list the categories that could contain an answer. Adapt these axes to the topic:

- Established vendors and newer entrants.
- Major product or model families.
- Current stable releases, previews, release candidates, and announced successors.
- Open-weight/open-source, source-available, and proprietary options.
- General-purpose and task-specific alternatives.
- Different architectures or implementation approaches.
- Native platform options and third-party runtimes.
- Relevant size, price, power, or capability tiers.

Do not fill this map exclusively from memory. Populate it through broad discovery searches, official catalogs, organization pages, release indexes, repositories, registries, and documentation hubs.

### 4. Run discovery searches before comparison searches

Use multiple query forms so one vendor's terminology does not control the results. Include combinations of:

- Topic + latest releases + current year.
- Topic + new model/product/tool + current and previous year.
- Topic + release notes, changelog, roadmap, preview, successor, or deprecation.
- Task + on-device/edge/cloud/open-source or other relevant deployment terms.
- Alternatives to each initially named candidate.
- Site-restricted queries for authoritative organizations and repositories.

Search at least one level broader than the user's examples. When the request begins with “Gemma or anything,” search the category, not only Gemma competitors already known by name.

### 5. Verify every important family’s chronology

For each serious family or vendor:

1. Locate its current official catalog, releases page, documentation, repository, or model organization.
2. Identify the newest stable, preview, and announced versions relevant to the task.
3. Search explicitly for a successor using likely next names and generic terms such as “next generation.”
4. Check publication date, artifact update date, documentation status, and deprecation notices.
5. Confirm whether weights, binaries, API access, SDK support, and licenses are actually available.

Do not infer that a numbered successor exists. Do not infer that it does not exist because the first search missed it.

### 6. Create an evidence ledger

Track serious candidates while researching:

| Candidate | Release/status | Availability | Relevant evidence | Constraints | Confidence |
|---|---|---|---|---|---|

For each decisive claim, prefer:

1. Official release notes, documentation, model cards, repositories, papers, specifications, or registry entries.
2. Original benchmark publications or reproducible benchmark artifacts.
3. High-quality secondary reporting only for discovery or context when primary evidence is unavailable.

Open sources rather than treating search-result snippets as final evidence. For mutable repository content, inspect dates, releases, tags, and commit history when relevant.

### 7. Normalize comparisons

Compare like with like:

- Stable versus stable; label previews separately.
- Same task, dataset, prompt, quantization, hardware, runtime, batch size, and context where possible.
- Total parameters versus active parameters.
- Model-only size versus end-to-end memory.
- Prefill versus decode speed; cold start versus warm latency.
- Vendor-reported measurements versus independent or reproduced measurements.
- Announced support versus working, downloadable support.

Do not turn incomparable benchmark numbers into a precise ranking. State when a recommendation is an inference from imperfect evidence.

### 8. Search for disconfirming evidence

Before finalizing a winner, try to invalidate it:

- Search for a newer successor or refreshed checkpoint.
- Search for platform/runtime incompatibilities.
- Check license restrictions and commercial-use terms.
- Check whether claimed speed depends on special kernels or unreleased hardware.
- Look for regressions, unresolved issues, removed artifacts, or misleading parameter labels.
- Search whether a smaller task-specific system can outperform the favored general solution.

Treat failed disconfirmation as increased confidence, not proof.

### 9. Perform a coverage audit

Do not stop merely because a plausible answer appeared. Stop when all applicable conditions hold:

- The search-space map’s major categories were checked.
- Each major relevant family has a verified current release or an explicit uncertainty.
- Initially named candidates and newly discovered credible candidates were examined.
- At least two differently phrased discovery routes produced no important uninvestigated candidate.
- Successor, preview, availability, runtime, and license checks are complete for finalists.
- Contradictory dates or claims are resolved or disclosed.
- Excluded serious candidates have short, evidence-based reasons.

Never promise literal exhaustiveness. Say “no additional material candidates surfaced under this scope as of DATE” and state the scope.

### 10. Write the answer for auditability

Lead with the conclusion, then include only the structure the decision needs:

- **As-of date and scope.**
- **Recommendation or current landscape.**
- **Latest-version verification.** Clarify stable, preview, announced, and available states.
- **Candidate comparison.** Use normalized criteria.
- **Important exclusions.** Explain why plausible candidates did not qualify.
- **Confidence and gaps.** Identify vendor-only claims or missing apples-to-apples data.
- **Sources.** Cite primary pages next to the claims they support.

If correcting an earlier answer, say exactly what assumption narrowed the earlier search and what the fresh search changed.

## Failure patterns to prevent

- Starting with a remembered shortlist and searching only within it.
- Treating the user’s examples as the complete category.
- Assuming a familiar family’s remembered version is current.
- Searching “best X” before discovering what X currently exists.
- Confusing announcement date, release date, artifact update date, and general availability.
- Calling a model or product faster based only on size or marketing.
- Ignoring task-specific alternatives because general-purpose products are more visible.
- Omitting license, runtime, hardware, language, region, or deployment constraints.
- Citing a search snippet, aggregator, or stale comparison table when a primary source exists.
- Hiding uncertainty behind a clean ranking.

## Compact operating checklist

Before answering, confirm:

- [ ] Browsed from a date-anchored, category-wide starting point.
- [ ] Built the candidate universe before ranking.
- [ ] Checked current catalogs and explicit successors.
- [ ] Verified stable/preview/announced/available status.
- [ ] Opened primary evidence for decisive claims.
- [ ] Normalized performance comparisons.
- [ ] Searched for disconfirming evidence and task-specific alternatives.
- [ ] Audited coverage and documented important exclusions.
- [ ] Stated the as-of date, scope, confidence, and remaining gaps.
