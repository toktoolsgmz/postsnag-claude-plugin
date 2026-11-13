Condensed reference. The full version lives in the complete-bundle download.

# csv-parse.md

How to read a PostSnag export without silently corrupting it.

Version 1.0 | 2026-08-05

---

## 1. Parse with a real CSV parser, and match columns by header NAME

**Never split on commas or newlines.** `Content` holds Facebook captions verbatim, which means embedded commas, doubled quotation marks, emoji, and **line breaks**. Physical lines are not rows: a 60-post export is 61 logical rows and can be 245 physical lines. An agent that reads it line by line sees 245 records, most of them caption fragments, and it will happily compute a median over them. Use `csv.DictReader(open(path, newline="", encoding="utf-8"))` or your runtime's equivalent. With no runtime, parse by CSV rules in your context: a field opening with `"` runs to the next unescaped `"`, newlines inside it are content, `""` is a literal quote. **Say the parsed row count out loud in your working notes.** If it is close to the file's physical line count, you parsed it wrong. Go back.

**Address every field by header name, never by position.** The two export types spell the same idea differently (`Post_URL` versus `Post URL`), and column order is an implementation detail that can change in a release. If an expected column is missing, do not guess and do not substitute a lookalike: name the column, name the section that depends on it, then skip that section or ask for a re-export.

## 2. The exact columns

**Profile export, 12 columns:** `Posted` (ISO timestamp), `Type` (one of `text`, `photo`, `video`, `link`, `album`; `video` includes reels; **there is no poll type**), `Reactions` (total only), `Comments` (counts only, no text), `Shares`, `Views` (video rows only), `Duration_Sec` (video rows only), `Content` (caption, embedded newlines, may be empty), `Post_URL`, `Media_URLs` (expiring CDN links), `Link_Title`, `Link_URL`.

**Group export, 9 columns:** `Author`, `Username`, `Posted`, `Type`, `Reactions`, `Comments`, `Shares`, `Content`, `Post URL` (**space, not underscore**). The group export has **no media columns at all**: no `Views`, no `Duration_Sec`, no `Media_URLs`, no `Link_Title`, no `Link_URL`. Group analysis is text and engagement only, and the skill says so rather than leaving the user wondering where the visual section went.

## 3. Empty is absent, not zero

Empty `Views` or `Duration_Sec` means the post type does not carry that metric, not zero views: exclude those rows from view-based math and report the denominator you used ("computed across the 14 video posts"). Empty `Content` is a visual-only post: exclude it from hook, caption, topic, and length analysis, **keep it in the engagement corpus**, and report both counts ("60 posts analyzed for engagement, 57 for text"). Empty `Media_URLs` does not prove there was no media, so infer text-only from `Type` and never from that field. A zero in `Reactions`, `Comments`, or `Shares` is a real zero. Keep it.

## 4. Timestamps, order, span, timezone

Parse `Posted` as a timestamp (`2026-06-06T19:30:12`). Do not string-slice. The date part is reliable; the time part depends on what the extension resolved, and older posts can come back date-only as `T00:00:00`.

```
midnight_share = count(rows where time == 00:00:00) / total rows
if midnight_share > 0.5:  treat the capture as DATE-ONLY, produce no time-of-day analysis,
                          degrade to day-of-week, and say so in one plain sentence
```

When the capture is mixed, report the precise-row count and run time-of-day on those rows only, subject to the 5-post floor. **Row order:** exports are in capture order, typically newest first, so sort by parsed `Posted` before anything sequence-dependent. **Span:** `span_days = (max date minus min date) + 1`, from the parsed values, never from the window the user named.

**The timezone of `Posted` is not stated in the export and must not be assumed.** Either ask once up front ("These timestamps have no timezone attached. Are they in your local time, and which timezone? I need this before I can tell you what hour to post."), then name the confirmed zone in the output, or use relative-window language and never absolute clock advice. "Your evening posts beat your morning posts by 1.6x on median engagement" is true regardless of timezone. "Post at 7pm" is not. Day-of-week carries the same caveat in one clause: an offset can move a late-evening post into the next day.

## 5. Media_URLs: never fetch, ever

Signed, expiring Facebook CDN links. Never issue a network request to one, not to check it, not to describe it. Treat the field as a presence flag at most. **Any visual analysis requires the user to supply the images**, as pasted screenshots or the media zip. When they have not, omit the visual section entirely and say one line about why. Never describe an image you were not shown; a fabricated visual detail invalidates a true finding sitting next to it.

## 6. Reading the Markdown export (defensive, because the structure is unverified)

Same posts, plus a point-in-time follower count and the bio. Parse structurally, not by matching a remembered string. Read top to bottom; the profile block comes before the posts. Find the repeating unit: the heading level occurring many times with post-shaped content under it is one post per block. Inside a block, read labeled values by their label (a line containing "Reactions" and an integer yields Reactions), and take the prose body as the caption. **Count the blocks and tell the user the number before analyzing** ("I read 42 posts out of your Markdown export"). **If the structure does not match, STOP and ask for the CSV:** say what you saw and what you expected, and do not half-parse and analyze whatever came out. The CSV always exists on the free tier, so asking costs one click.

The follower count is a single point-in-time number: one sentence of context, no growth claim, no per-follower rate. The bio is topic context, not evidence about post performance.

## 7. The pasted-posts fallback

Minimum for anything quantitative: 5 posts, each with engagement numbers. Below that, run a qualitative read and say it is an opinion, not a measurement.

Normalize each pasted post into the shape of a CSV row first. Caption text is required. If reactions, comments, and shares are all missing there is no ranking, only a qualitative read. A single combined engagement number is usable as `engagement`, with the comment and share ratios noted as unavailable. A missing date means every date-based section is omitted rather than estimated. A missing type is inferred from what the user said and marked inferred.

Three honesty rules. Say the count ("Read across the 7 posts you pasted."). Apply the same thresholds, because pasted data gets no discount on the rules. And name the selection bias once, plainly, without lecturing: "You picked these 7, so they are not a random sample of your account, and this read describes them rather than your posting overall." One sentence, then get on with it.
