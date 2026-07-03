---
name: extract-useful-info
description: Extract useful information, alpha/edge, actionable takeaways, tools, claims to verify, follow-up actions, and optional Markdown notes from videos, transcripts, articles, posts, PDFs, screenshots/OCR text, folders, notes, or mixed source material. Use when the user asks for useful info, alpha, edge, signals, takeaways, insight extraction, transcript/video analysis, high-signal summaries, or saved .md output.
---

# Extract Useful Info

## Goal

Turn source material into keep-worthy notes, then promote the best subset into alpha. Do not produce an even summary. Keep useful information that a person would actually save, and separately call out strong or practical edge.

## Source Intake

Use any reliable path that yields clean text or readable source material. Do not over-focus on extraction mechanics when the source is already available.

- Treat the user's prompt as the input arguments: source URL/path/folder/query, desired depth, alpha-only/full mode, and any output preference.
- For a folder or batch of sources, enumerate reasonable source files, preserve source IDs, and process as a set. If the set is too large for a useful pass, do an alpha/useful candidate scan first or ask for a narrower scope.
- For YouTube/video URLs, prefer `yt-dlp --skip-download --write-subs --write-auto-subs` to get subtitles/transcripts. Prefer human captions when present. Strip duplicate rolling caption fragments and timestamp noise before analysis.
- For X/Twitter URLs, prefer `$twitter-x-extraction` when available. Use `https://api.fxtwitter.com/<user>/status/<id>` for clean JSON before browser, oEmbed, or raw-page fallbacks; include quoted posts and thread context when returned.
- For articles, posts, webpages, PDFs, screenshots, or images, use available browsing, extraction, OCR, or local file tools. If extraction quality is poor, say so briefly.
- If source material is provided directly in the prompt, analyze it directly unless the user asks to verify or the content is likely stale.
- Attribute claims to the source. Mark inferences as inferences. Do not turn a source's assertion into established fact unless verified.
- Preserve source stance. Simplify wording, not claims; do not turn contrast, satire, quoted disagreement, or a reply's target into advice unless the source clearly endorses it.
- If the user asks for current facts, prices, rules, specs, safety, or recommendations involving meaningful time or money, verify where tools allow.

## Extract Then Promote

First extract useful information. Then promote the subset that clears the alpha bar.

- **Strong alpha**: Scarce, asymmetric, non-obvious information that could create an advantage if acted on.
- **Practical alpha**: Non-obvious practical leverage: workflows, tools, process changes, commands, setups, or heuristics that are actionable and easy to miss. It does not need to be secret, but it must be more than generic useful advice.
- **Useful information**: Keep-worthy notes: claims, techniques, numbers, named tools, resources, arguments, concrete examples, and clarifying details.
- **Context**: Include only when it helps interpret why a useful item matters.

The bar for useful information is: would this line earn a place in a permanent note? The bar for alpha is higher: would this give an intelligent generalist or the user a practical edge they might otherwise miss?

Do not force alpha. "No strong alpha found" is a valid result. Do not let practical alpha become a catch-all for merely useful information.

## Workflow

1. Extract or read the source material.
2. Pull the notes worth keeping, grouped by topic rather than chronology.
3. Promote the strongest edge-giving items into Strong Alpha or Practical Alpha.
4. Add verification targets for factual, current, risky, surprising, or high-impact source claims.
5. Match the requested depth. If the user asks for "brief", return only the top findings. If the user asks for "exhaustive", include lower-level useful notes too.

## Output Format

Use a light structure. Omit empty sections and do not force every alpha item into a rigid six-field template.

```markdown
**Source**
One line on what was analyzed and any extraction limits, if useful.

**Alpha / Edge**
- **Strong:** ...  
  Why this is alpha: ...
- **Practical:** ...  
  Why this is practical alpha: ...

**Useful Information**
- Grouped notes by topic.

**Tools / Names / References**
- Only concrete names, commands, URLs, products, people, repos, papers, or concepts worth retaining.

**Worth Verifying**
- Source says ...; verify because ...

**Source-Grounded Actions**
- Optional. Include only actions directly supported by the source, or label them as inference.
```

For small tasks, answer compactly and plainly. For alpha items, include "Source says" or "Inference" when attribution matters.

## Markdown Output

Default to replying inline in chat.

- If the user asks to save, export, write, create a note, or produce a `.md`, write the output to a Markdown file without asking first.
- If the user did not ask for a file but the extraction is substantial or worth keeping, end with a concise question offering to save it, such as: `Want me to save this as <slug>-useful.md?`
- Name files from the source title, URL slug, filename, or folder name. Use lowercase hyphenated names when practical.
- Use `<source>-useful.md` for full useful-info output. For batch/folder output, use `<batch-or-folder>-useful.md` unless the user asks for one note per source.
- Save in the current working directory or the user-specified destination. For source folders, save alongside the folder only if the user asked or it is clearly the intended workspace.
- Do not ask to save trivially short answers, failed extractions, or outputs the user explicitly wanted only in chat.

## Large Source Sets

When processing many sources or a long transcript:

- Use a two-pass approach: collect useful candidates first, then dedupe, promote, and rank.
- Preserve source IDs, titles, timestamps, or links when available.
- Cluster repeated signals across sources and raise confidence when independent sources converge.
- Prefer alpha-only compression if the user asks for edge, high-signal triage, or dataset-scale processing.
