---
name: alpha-extraction
description: Extract only the alpha — the scarce, edge-giving, non-obvious insights — from content of any kind: videos (yt-dlp transcripts), posts, articles, images, feeds, folders of sources. Terse output built for fast triage of many sources; most sources correctly yield "no alpha". Use when the user says "extract the alpha", "any alpha in these?", "triage this playlist/channel/folder", or wants only the rare gems from a batch without general notes. For full notes plus alpha sections from a single piece, use distill instead.
---

# Alpha extraction

Alpha is information that confers an edge. Its value comes from asymmetry: if everyone in the field already says it, it isn't alpha, however true or well said. An alpha item usually has at least three of these properties:

- **Actionable** — the user can do something concrete with it.
- **Non-obvious** — an informed reader would likely miss or underweight it.
- **Leverage-producing** — saves time, money, effort, or risk, or unlocks a new workflow.
- **Specific** — names tools, steps, numbers, people, commands, settings, constraints.
- **Under-discussed** — not the headline or the obvious thesis; not already priced in.
- **Timely** — acting sooner matters.

This is the terse sibling of `distill` — it skips general notes entirely. The point is triage, precision over recall: pass many sources through a high bar cheaply, and expand only the hits.

The invocation is free text, not a schema: the target (URL, file, folder, playlist, channel) plus any modifiers — what the user already knows, a save destination. A folder or playlist means every readable source inside it.

## Reject

- The source's obvious headline or thesis.
- Generic productivity, business, or technical advice.
- Interesting but not actionable.
- Promotional claims without concrete implementation detail.
- Unsupported speculation, unless labeled as a low-confidence hypothesis.
- A bare tool name without the reason it creates an edge.

## Get the content

Whatever yields clean text is fine — the judging below is input-agnostic.

- **YouTube / video platforms**: `yt-dlp --skip-download --write-subs --write-auto-subs --sub-langs "<lang>.*" --convert-subs srt -o "<tmpdir>/sub" "<url>"` — match the language to the video, and prefer human captions over auto-subs when both come down. Auto-subs repeat rolling lines; dedupe before reading. For playlists/channels, yt-dlp handles the enumeration too.
- **X / Twitter**: x.com blocks anonymous fetching — swap the domain to `https://api.fxtwitter.com/<user>/status/<id>` for the full post as JSON, quoted posts included. Read the JSON directly, not through a summarizing fetcher, so the text stays verbatim.
- **Images / screenshots**: read them directly; `tesseract` only for bulk OCR.
- **Web posts / articles**: fetch the page.
- **Local files**: read them.

If extraction is partial or noisy, keep only high-confidence hits and say so.

## Judge

Read the whole source before judging — alpha hides in asides and throwaway remarks more often than in the thesis.

- Baseline reader is an intelligent generalist, not a domain expert. When genuinely unsure whether something is obvious, include it and let the justification show the doubt. If the user states what they already know, raise the bar to match.
- State each item fully enough to act on without going back to the source, plus one line on why it clears the bar — noting when it rests on the source's unverified claim. Plain language: simplify the wording, never the claim.
- Anchor every hit to its source (URL or ID, plus timestamp or section when available) so it can be checked without re-reading the batch.
- "No alpha" is the expected common case. It is a finding, not a failure — never lower the bar or pad to avoid it.

## Output

```markdown
<source> — <URL or ID>
- <alpha item> — <why it clears the bar> (<timestamp/section>)

<source> — no alpha
```

Single source with no hits may add the single best near-miss and why it fell short, so the user can audit where the bar sits; batch misses stay one line, never expanded. After replying, offer to save the results as `<source-name>-alpha.md` (`<batch-name>-alpha.md` for a set) — for large batches skip the question, write the file, and reply with only the hits.
