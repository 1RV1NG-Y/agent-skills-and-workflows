---
name: distill
description: Extract the useful information and the alpha from any piece of content — YouTube videos (via yt-dlp transcripts), articles, posts, PDFs, screenshots, podcasts, talks. Use whenever the user wants what's worth knowing from content without consuming it all — "distill this", "extract the useful info from this video", "what does this post actually say", "pull the insights out of this" — or drops a link/file asking what matters in it. Produces condensed keep-worthy notes plus promoted Practical alpha and Alpha sections of the actionable and edge-giving insights. For triaging many sources where only alpha matters, use alpha-extraction instead.
---

# Distill

Turn content into the notes worth keeping: useful information, with the alpha promoted out of it.

## Arguments

The invocation is free text, not a schema. It usually names the target — URL, file, folder, playlist — and may carry modifiers: what the user already knows, an alpha-only focus, a save destination, a language. Read all of it as instructions; a folder means every readable source inside it.

## Get the content

Whatever yields clean text is fine — the extraction below is input-agnostic.

- **YouTube / video platforms**: `yt-dlp --skip-download --write-subs --write-auto-subs --sub-langs "<lang>.*" --convert-subs srt -o "<tmpdir>/sub" "<url>"` — match the language to the video, and prefer human captions over auto-subs when both come down. Auto-subs repeat rolling lines; dedupe before reading.
- **X / Twitter**: x.com blocks anonymous fetching — swap the domain to `https://api.fxtwitter.com/<user>/status/<id>` for the full post as JSON, quoted posts included. Read the JSON directly, not through a summarizing fetcher, so the text stays verbatim.
- **Images / screenshots**: read them directly; `tesseract` only for bulk OCR.
- **Web posts / articles**: fetch the page.
- **Local files**: read them.

If extraction came back partial or noisy, say so up front — the reader should know which notes stand on shaky transcription.

## Extract, then promote

Read all of it first. Collect the useful information, then promote upward:

**Useful information.** The notes a person would actually keep: claims, techniques, numbers, named tools and resources, arguments, concrete examples. Grouped by topic, not chronological. This is not a summary — filler, ads, self-promo, motivational padding, and restatements of earlier points don't make the cut. The bar: would this line earn a place in a permanent note?

**Practical alpha.** Promoted from useful information: items that are actionable and easy to miss, even if not secret or time-sensitive — workflow moves, tool usage, process details, settings, heuristics. The working knowledge a reader could apply tomorrow but would probably skim past.

**Alpha.** The scarce end: non-obvious, hard-won, edge-giving — what wouldn't appear in top search results or a beginner tutorial on the topic. Alpha's value comes from asymmetry: if everyone in the field already says it, it isn't alpha, however true or well said.

Every promoted item carries a one-line justification of why it clears its bar, noting when it rests on the source's unverified claim. Promoting from the collected pool rather than hunting alpha directly is deliberate: committing to items first and judging them second keeps borderline material from being silently dropped, and keeps the promoted sections auditable against the pool they came from.

## Calibration

- Baseline reader is an intelligent generalist, not a domain expert. When unsure whether something is too obvious, include it — a misjudgment should demote an item one grade, never delete it. If the user states what they already know, raise the bars to match.
- Most content contains little or no alpha. Empty promoted sections are correct, expected results. Never pad them to seem thorough.

## Output

Write in plain language: short sentences, everyday words. Simplify the wording, never the claim — if a nuance dies when shortened, keep the nuance. Strongest material first. Default shape:

```markdown
<one or two sentences: what this is, whether it was worth the time, any context needed for the notes to land>

## Alpha
- <insight> — <why it clears the bar>

## Practical alpha
- <insight> — <how to use it / why it's easy to miss>

## Useful information
### <topic>
- <note>

## Worth verifying
- <claim> — <what to check>
```

Omit empty sections. Reply inline, then offer to save the result as `<source-name>-useful.md` in the working folder — skip the question and just write the file when the user already chose a destination or the run spans several sources.

## Many sources

- Two passes: collect candidates per source, then dedupe and rank across the whole set.
- Keep a source anchor (URL/ID plus timestamp or section) on every promoted item.
- When independent sources converge on the same point, say so — convergence is itself a signal and raises confidence.
- For dataset-scale runs where only alpha matters, switch to `alpha-extraction`.
