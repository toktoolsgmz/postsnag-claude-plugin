# scoring-worksheet.md

The complete printable worksheet: every dimension, its weight, its 0-to-3 scale with observable anchors, the total bands, and the gap-fill re-weighting table. This is the depth asset behind Capture Target Builder. `rubric.md` tells you the method; this file is what you fill in per candidate while running it.

**Every weight, anchor, and cut point in this file is a working number**, stated as one, defined here for this skill, not derived from the catalog's shared engagement thresholds. Those numbers rank a user's own captured posts by engagement; this skill scores the outside view of an uncaptured candidate, which is a different kind of measurement and needed its own scale.

Version 1.0 | 2026-08-04

---

## Part A: the qualifying gate (run first, on every search result)

| # | Question | Yes means | No means |
|---|---|---|---|
| 1 | Posted within the last 14 days? | Currently active | Possibly dormant or abandoned |
| 2 | Do the most recent 3 visible posts each show a reaction or comment count above zero? | An audience is visibly present | Either private counts, a new account, or nobody is responding |
| 3 | Do at least half the visible recent posts carry more than one short line of caption? | There is real writing to learn from | Mostly visual-only posts, thinner for caption and hook analysis |
| 4 | Does the account use more than one visible post format? | Format-mix data exists for a future capture | Single-format account, format-mix score will be low |

**2 or more yes: advance to Part B. Fewer than 2: stop, do not record the candidate's name past this point.**

---

## Part B: the 4 base dimensions, full anchors

### 1. Posting recency (weight 3)

| Score | Anchor, in observable terms |
|---|---|
| 0 | Last visible post is 30 or more days old, or there is no visible recent activity at all |
| 1 | Last visible post is 15 to 29 days old |
| 2 | Last visible post is 8 to 14 days old |
| 3 | Last visible post is within the last 7 days, and more than one post falls in that window |

### 2. Visible engagement (weight 3)

| Score | Anchor, in observable terms |
|---|---|
| 0 | The last 3 to 5 visible posts show reaction counts under 5, or comments are absent entirely |
| 1 | Visible posts show reactions roughly in the 5-to-25 range, with occasional comments |
| 2 | Visible posts consistently show reactions roughly in the 25-to-150 range, and most posts carry multiple comments |
| 3 | Visible posts consistently show triple-digit-plus reactions, or a steady stream of 10 or more comments on most recent posts |

### 3. Caption depth (weight 2)

| Score | Anchor, in observable terms |
|---|---|
| 0 | Posts are visual-only or carry a single short line, no real writing |
| 1 | Captions exist but are short and generic (one to two sentences), inconsistent post to post |
| 2 | Most posts carry a few sentences of real writing, some specificity or personality |
| 3 | Captions are consistently substantial (a short paragraph or more), specific, with a clear voice across most visible posts |

### 4. Format mix (weight 1)

| Score | Anchor, in observable terms |
|---|---|
| 0 | Every visible post is the same single format |
| 1 | Two formats visible, but one accounts for roughly 90 percent or more of what's shown |
| 2 | Two to three formats in real rotation, no single format past roughly 80 percent |
| 3 | Three or more formats in active rotation, all appearing within the last 10 to 15 visible posts |

**Base-dimension max.** Each dimension's contribution is `score * weight`, summed across dimensions. Maximum when every dimension scores 3: `(3*3) + (3*3) + (3*2) + (3*1) = 9 + 9 + 6 + 3 = 27`.

**Base bands (no export supplied):**

| Band | Range | Share of max |
|---|---|---|
| Capture now | 18 to 27 | 66.7% and up |
| Watch | 9 to 17 | 33.3% to 63.0% |
| Skip | 0 to 8 | under 33.3% |

---

## Part C: the 5th dimension, gap-fill relevance (weight 3, only when an export is supplied)

Run `rubric.md` Section 5 first to find the gap format from the user's own `Type` column. Then score every candidate against it.

| Score | Anchor, in observable terms |
|---|---|
| 0 | The candidate's visible content is in formats the user's own export already uses heavily; capturing this candidate adds no new evidence |
| 1 | The candidate touches the gap format occasionally, mixed into formats the user already covers well |
| 2 | The candidate uses the gap format regularly, alongside other formats |
| 3 | The candidate's visible content is dominated by the exact format the user's own export shows under the 10 percent gap threshold |

**Full max with the 5th dimension:** `27 + (3*3) = 36`.

**Full bands (export supplied, gap-fill dimension applied):**

| Band | Range | Share of max |
|---|---|---|
| Capture now | 24 to 36 | 66.7% and up |
| Watch | 12 to 23 | 33.3% to 63.9% |
| Skip | 0 to 11 | under 33.3% |

---

## Part D: the re-weighting table, what changes and why

| Without an export | With an export, gap identified |
|---|---|
| 4 dimensions, max 27 | 5 dimensions, max 36 |
| Capture-now floor: 18 | Capture-now floor: 24 |
| A candidate is judged only on their own activity | A candidate is also judged on whether they cover ground the user's own capture history does not |
| A format-mix score of 3 is the highest reward format can contribute (weight 1, max 3 points of 27, about 11%) | Gap-fill can contribute up to 9 of 36 points (25%) on its own, on top of format mix, so a candidate who is otherwise middling can still reach capture-now if they squarely cover the user's blind spot |

**Why gap-fill gets its own dimension instead of folding into format mix.** Format mix (Part B.4) can never swing more than 11 percent of a candidate's score on its own; it is a general health signal, not a strong lever. Gap-fill can swing up to 25 percent, more than double format mix's own ceiling, on a sharper question: does this specific candidate's content sit in the one format the user's own posts are thinnest in. A candidate can score low on general format mix (mostly one format) and still score a perfect 3 on gap-fill, if that one format happens to be exactly what the user needs to see more of. That much swing is exactly why gap-fill earned its own weighted dimension instead of a bonus point folded into format mix, where its influence would have been capped at format mix's own small share.

---

## Part E: printable per-candidate row

Copy this row for every candidate that clears the gate in Part A.

```
Candidate: __________________  (placeholder label only, e.g. "Candidate 1")
Type: profile / group
Niche-map category: __________________
Qualifying gate: __ of 4 yes  ->  PASS (2+) / do not score further

Posting recency        [0 1 2 3] x 3 = ___
Visible engagement     [0 1 2 3] x 3 = ___
Caption depth          [0 1 2 3] x 2 = ___
Format mix             [0 1 2 3] x 1 = ___
Gap-fill relevance     [0 1 2 3] x 3 = ___   (only if export supplied; otherwise skip this row and use the 27-point bands)

TOTAL: ___ / 27 or 36
BAND: Capture now / Watch / Skip
```
