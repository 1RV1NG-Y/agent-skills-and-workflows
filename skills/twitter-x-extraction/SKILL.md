---
name: twitter-x-extraction
description: Extract clean, source-faithful text and metadata from X/Twitter posts, quote tweets, threads, and screenshots or URLs. Use when the user provides an x.com/twitter.com/fxtwitter URL, asks to recover a tweet/post, wants quoted-post context, needs source text for alpha/useful-info extraction, or X blocks anonymous browser access.
---

# Twitter/X Extraction

## Goal

Recover the actual post text, metadata, and quoted context before analyzing or summarizing. Prefer raw structured data over rendered pages or summarizing fetchers.

## URL Intake

Normalize common forms:

- `https://x.com/<user>/status/<id>`
- `https://twitter.com/<user>/status/<id>`
- `https://fxtwitter.com/<user>/status/<id>`
- URLs with query strings, media suffixes, or mobile domains

Extract `<user>` and `<id>`. Keep the original URL in the output.

## Preferred Fetch Path

Try fxtwitter's API first:

```bash
curl -s 'https://api.fxtwitter.com/<user>/status/<id>'
```

Read these fields when present:

- `tweet.text` or `tweet.raw_text.text`
- `tweet.author.name`, `tweet.author.screen_name`, `tweet.author.url`
- `tweet.created_at`, `tweet.created_timestamp`, `tweet.lang`
- `tweet.url`, `tweet.id`
- `tweet.likes`, `tweet.replies`, `tweet.retweets`, `tweet.quotes`, `tweet.bookmarks`, `tweet.views`
- `tweet.quote.text` or `tweet.quote.raw_text.text`
- `tweet.quote.author.*`, `tweet.quote.created_at`, `tweet.quote.url`
- `tweet.media`, `tweet.twitter_card`, or provider/card fields when relevant

If a fetcher returns prose instead of raw JSON, treat it as suspect and fetch the API directly.

## Fallbacks

If fxtwitter fails or omits needed context:

- Try `https://publish.twitter.com/oembed?url=<original-url>` for embedded post HTML and author/date metadata.
- Fetch the raw X/Twitter page and search for `articleBody`, `NoteTweet`, `full_text`, `raw_text`, or the post ID. Use binary-safe search such as `rg -a` if needed.
- Use a browser/session or screenshot OCR only when structured fetches fail.
- For screenshots, OCR first, then preserve visible handles, timestamps, reply/quote relationships, and media captions.

## Threads And Quote Tweets

- Include quoted posts by default when the API returns `tweet.quote`.
- For replies, preserve `replying_to` and `replying_to_status` if present.
- For threads, recover adjacent posts only when the source asks for the thread, the post is clearly incomplete without them, or the API/page exposes thread context.
- Label what was fetched: single post, quote tweet plus quoted post, partial thread, screenshot-only, or failed/partial extraction.

## Fidelity Rules

- Quote or paraphrase the source faithfully. Simplify wording, not claims.
- Do not turn a quoted post, reply target, satire, contrast, or disagreement into the author's recommendation.
- Distinguish `Source says` from `Inference`.
- Preserve uncertainty and hype as source claims, not facts.
- If the source may affect current decisions, verify outside X before presenting it as true.

## Output

For extraction-only tasks:

```markdown
**Source**
- URL:
- Fetched via:
- Extraction limits:

**Post**
- Author:
- Date:
- Text:

**Quoted / Thread Context**
- ...

**Metadata**
- Likes/replies/reposts/views, media, cards, language, or other relevant fields.
```

For analysis tasks, pass the recovered text and context into the relevant downstream skill, such as `$extract-useful-info` or `$extract-alpha`, and keep extraction limits visible.
