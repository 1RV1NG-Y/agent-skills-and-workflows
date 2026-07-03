---
name: extract-alpha
description: Extract only alpha/edge: non-obvious, actionable, leverage-producing information and optional Markdown alpha notes from videos, transcripts, posts, articles, PDFs, screenshots/OCR text, folders, notes, or large source sets. Use when the user asks for alpha, edge, signal, hidden gems, asymmetric takeaways, high-signal extraction, saved .md alpha output, or efficient scanning across many sources.
---

# Extract Alpha

## Goal

Return only findings that plausibly give the user an edge. Optimize for precision over recall. Do not summarize the source, and do not include generic useful information unless it becomes genuine alpha.

## Definition

Alpha is non-obvious, actionable information that can create an advantage. It usually has at least three of these properties:

- **Actionable**: The user can do something concrete with it.
- **Non-obvious**: A normal informed reader would likely miss or underweight it.
- **Leverage-producing**: It can save time, money, effort, risk, or unlock a new workflow.
- **Specific**: It names tools, steps, numbers, people, URLs, commands, products, settings, or constraints.
- **Under-discussed**: It is not merely the main thesis or obvious headline.
- **Timely**: Acting sooner may matter.

Practical alpha is allowed when the edge is a workflow, tool, process, setup, command, or heuristic that is actionable and easy to miss. Useful but obvious information is not alpha. If there is no alpha, say so.

## Source Intake

Use the lightest reliable path that yields clean source material:

- Treat the user's prompt as the input arguments: source URL/path/folder/query, desired strictness, batch mode, output count if any, and any `.md` destination preference.
- For a folder or batch of sources, enumerate reasonable source files, preserve source IDs, and scan for alpha candidates. Keep batch misses cheap.
- For YouTube/video URLs, use `yt-dlp --skip-download --write-subs --write-auto-subs` first. Prefer human captions when present. Strip duplicated caption fragments before judging.
- For X/Twitter URLs, prefer `$twitter-x-extraction` when available. Use `https://api.fxtwitter.com/<user>/status/<id>` for clean JSON before browser, oEmbed, or raw-page fallbacks; include quoted posts and thread context when returned.
- For posts, articles, PDFs, screenshots, or images, use available browsing, extraction, OCR, or local file tools.
- For provided text, analyze directly.
- For large datasets, scan quickly for candidate alpha, then dedupe and rank. Preserve source IDs, links, titles, timestamps, or filenames when available.
- If extraction is partial or noisy, keep only high-confidence alpha and state the limitation.
- Attribute source claims. Mark inferences as inferences. Add verification targets for factual, current, risky, or surprising claims.
- Preserve source stance. Simplify wording, not claims; do not turn contrast, satire, quoted disagreement, or a reply's target into alpha unless the source clearly endorses it.

## Rejection Rules

Reject candidates that are:

- The source's obvious headline or thesis.
- Generic productivity, business, or technical advice.
- Interesting but not actionable.
- Promotional claims without concrete implementation detail.
- Unsupported speculation unless labeled as a low-confidence hypothesis.
- Merely a tool name without a reason it creates edge.

## Workflow

1. Extract or read the source.
2. List candidate alpha claims, workflows, tools, constraints, or examples.
3. Deduplicate repeated candidates.
4. Keep only candidates with actionability, non-obviousness, leverage, specificity, and adequate source support.
5. Separate source claims from inference.
6. Return none if nothing passes. Do not satisfy an implied quota by padding.

## Output Format

Use a terse structure:

```markdown
**Alpha**
- ...  
  Why this is alpha: ...  
  Source says / Inference: ...

**Patterns Across Sources**
- ...

**Worth Verifying**
- ...
```

If no candidates pass:

```markdown
No alpha found.

Best near-misses:
- ...
```

Include near-misses only for a single source when they help calibrate the bar. Omit near-misses in batch mode or when the user asks for strict alpha-only output. For batch mode, collapse misses to one line per source and expand only hits.

Write plainly. Keep the claim faithful even when compressing it.

## Markdown Output

Default to replying inline in chat.

- If the user asks to save, export, write, create a note, or produce a `.md`, write the alpha output to a Markdown file without asking first.
- If the user did not ask for a file but the alpha found is substantial or worth keeping, end with a concise question offering to save it, such as: `Want me to save this as <slug>-alpha.md?`
- Name files from the source title, URL slug, filename, or folder name. Use lowercase hyphenated names when practical.
- Use `<source>-alpha.md` for single-source alpha. For batch/folder output, use `<batch-or-folder>-alpha.md` unless the user asks for one note per source.
- Save in the current working directory or the user-specified destination. For source folders, save alongside the folder only if the user asked or it is clearly the intended workspace.
- Do not ask to save `no alpha` results, trivial near-misses, failed extractions, or outputs the user explicitly wanted only in chat.
