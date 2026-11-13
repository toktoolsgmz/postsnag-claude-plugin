# bucket-evidence-worksheet.md

The worksheet an agent fills while running this skill. Every bucket in both layers gets a row, including the ones with zero or one post, because a worksheet that only shows the winners cannot be checked by anyone else. This is the working document behind `example-run.md`, shown in full so a supervisor can audit every cell, not just the five that made it into the output.

**`example-run.md` Part 1 is the source of truth for the worked example; this worksheet is a mirror of it, organized for audit rather than for narrative.** If a number ever disagrees between the two files, `example-run.md` Part 1 is the one that gets trusted and this file gets corrected to match, because Part 1 is what a builder actually walks step by step and this worksheet exists to make every cell in that walk auditable in one place.

Version 1.0 | 2026-08-04

---

## Part A: the decision tree, raw CSV to final claims

Follow this in order. Do not skip a step because a later one seems more interesting.

```
1. PARSE
   Real CSV parser. Columns by header name. Posted parsed as a timestamp, not sliced as a string.
   Report: row count, date range, span in days.
   -> references/csv-parse.md sections 1, 2, 4 (condensed; full version in the bundle)

2. PRECISION CHECK
   midnight_share = rows at exactly T00:00:00 / total rows
   IF midnight_share > 0.5: whole capture is date-only.
       -> skip to step 4 with TIME-OF-DAY DISABLED. Day-of-week only.
   IF midnight_share is between 0 and 0.5: mixed precision.
       -> time-of-day analysis runs on the precise rows only, state the count.
   IF midnight_share == 0: full precision, both layers proceed normally.
   -> rubric.md section 3

3. TIMEZONE GATE
   Ask the user once: "Are your Posted timestamps in your local time, and which timezone?"
   IF confirmed: every clock-time claim downstream names the timezone.
   IF not confirmed: every clock-time claim downstream is replaced with a ratio or
   a relative comparison. Band names may still be used as group labels, but no
   specific hour range is presented as advice to act on.
   -> rubric.md section 2

4. BUCKET, LAYER 1: DAY OF WEEK
   7 buckets. Compute n for each.
   -> rubric.md section 4

5. BUCKET, LAYER 2: DAY x TIME BAND
   Up to 28 buckets (7 days x 4 bands: Morning 5-11, Midday 11-5, Evening 5-9, Night 9-5).
   Compute n for each. A cell with n=0 is real information, not a gap to hide.
   -> rubric.md sections 1, 4

6. COMPUTE STATS PER BUCKET, BOTH LAYERS
   n, median engagement, mean engagement, top post and its engagement.
   -> references/foundations.md sections 1, 2 (condensed; full version in the bundle)

7. SPLIT RANKABLE / UNRANKABLE
   n >= 5 is rankable. n < 5 is listed with its numbers, never ranked, never deleted.
   -> references/foundations.md section 3

8. CONCENTRATION CHECK, rankable buckets only
   median-after-removing-top-post, top post's share of bucket total, mean/median.
   0 or 1 flag: bucket ranks, flag written inline if 1 fired.
   2 or 3 flags: bucket does NOT rank. Name the post responsible instead.
   -> references/foundations.md section 4, rubric.md section 6

9. FORMAT-CONFOUND CHECK, on EVERY rankable bucket in both layers
   For each Type present: rep_ratio = type_share_in_bucket / type_share_in_corpus
                            type_median_ratio = type_median_corpus / corpus_median
   FLAG if rep_ratio >= 1.5 AND type_median_ratio >= 1.2.
   A flag does not exclude the bucket. It is glued to the recommendation as a caveat.
   Every ranked row records one of three states, never a blank and never "none":
   the named confound, "checked, no confound", or "not checked".
   -> rubric.md section 5

10. RANK
    Median descending, within each layer, rankable buckets only.
    Compute the mean-based ranking too. If the top 3 disagree, say so, name the
    posts responsible, ship the median ranking.
    -> rubric.md section 7

11. SCHEDULE GAP
    most_posted = highest posting_share among rankable day-of-week buckets.
    best_median = rank 1 from step 10, day-of-week layer.
    State both numbers and the percentage gap, or state they match.
    Repeat at the day x band layer only if it has a usable winner.
    -> rubric.md section 8

12. WRITE THE OUTPUT
    Timezone question or confirmation first. Lite-mode / date-only banner next, if
    applicable. Heat grid showing every cell. Best-days table. Best-windows table
    (or the one-line "not usable yet" note). Schedule gap. Honesty footer. Pointer line.
    -> output-template.md
```

---

## Part B: the filled worksheet, `profile-maya-torres.csv` (60 posts, full precision, timezone confirmed for this run)

### Layer 1: day of week, all 7 buckets

| Day | n | Median | Mean | Rankable? | Concentration flags | Confound check | Notes |
|---|---|---|---|---|---|---|---|
| Monday | 9 | 341 | 451.9 | YES | none | **CONFOUND: link, rep_ratio 1.667, type_median_ratio 1.73** | the one link post is also the bucket's top post, 1,402 on 2026-07-20 |
| Tuesday | 12 | 521.0 | 602.6 | YES | none | checked, no confound (highest rep_ratio is photo at 1.471, under 1.5, and photo's median ratio is 0.85 anyway) | |
| Wednesday | 1 | 566 | 566 | NO | not run (n<5) | not run (n<5) | too small to rank, worth testing |
| Thursday | 17 | 540 | 752.4 | YES | none | checked, no confound (highest rep_ratio is album at 1.324) | day-of-week rank 1 |
| Friday | 1 | 388 | 388 | NO | not run (n<5) | not run (n<5) | too small to rank, worth testing |
| Saturday | 19 | 388 | 672.6 | YES | divergence (mean/median 1.73) | **CONFOUND: link, rep_ratio 1.579, type_median_ratio 1.73** | most-posted day; carried partly by the June 6 post |
| Sunday | 1 | 560 | 560 | NO | not run (n<5) | not run (n<5) | too small to rank, worth testing |

**7 of 7 buckets accounted for. 4 rankable, 3 not. All 4 rankable days had the confound check run; 2 of the 4 fired.** No ranked row in this worksheet says "none" for a check that was never executed. "Not run (n<5)" and "checked, no confound" are different facts and the column keeps them different, because a reader cannot otherwise tell a clean bucket from an unexamined one.

### Layer 2: day x time band, all 28 possible cells

| Day | Band | n | Median | Mean | Rankable? | Concentration flags | Confound check |
|---|---|---|---|---|---|---|---|
| Monday | Morning | 3 | 341 | 344.7 | NO | not run | not run |
| Monday | Midday | 3 | 402 | 690.7 | NO | not run | not run |
| Monday | Evening | 2 | 249.5 | 249.5 | NO | not run | not run |
| Monday | Night | 1 | 462 | 462 | NO | not run | not run |
| Tuesday | Morning | 3 | 512 | 468.3 | NO | not run | not run |
| Tuesday | Midday | 1 | 214 | 214 | NO | not run | not run |
| Tuesday | Evening | 6 | 712.0 | 742.8 | YES | median-shift (-26.7% after top post removed) | **CONFOUND: link, rep_ratio 2.500, type_median_ratio 1.73** |
| Tuesday | Night | 2 | 577.5 | 577.5 | NO | not run | not run |
| Wednesday | Morning | 0 | n/a | n/a | NO | n/a | n/a |
| Wednesday | Midday | 0 | n/a | n/a | NO | n/a | n/a |
| Wednesday | Evening | 1 | 566 | 566 | NO | not run | not run |
| Wednesday | Night | 0 | n/a | n/a | NO | n/a | n/a |
| Thursday | Morning | 4 | 600.0 | 661.5 | NO | not run | not run |
| Thursday | Midday | 7 | 355 | 441.6 | YES | none | checked, no confound (text rep_ratio 1.51 clears the first condition, but text's median ratio is 0.85, so the second condition fails) |
| Thursday | Evening | 6 | 612.5 | 1,175.7 | YES, then EXCLUDED | **top-share (58.4%), divergence (1.92)**, 2 flags | run anyway for the record: **CONFOUND: video, rep_ratio 2.143, type_median_ratio 1.28** (video 3 of 6) |
| Thursday | Night | 0 | n/a | n/a | NO | n/a | n/a |
| Friday | Morning | 1 | 388 | 388 | NO | not run | not run |
| Friday | Midday | 0 | n/a | n/a | NO | n/a | n/a |
| Friday | Evening | 0 | n/a | n/a | NO | n/a | n/a |
| Friday | Night | 0 | n/a | n/a | NO | n/a | n/a |
| Saturday | Morning | 10 | 335.5 | 357.6 | YES | none | **CONFOUND: link, rep_ratio 1.500, type_median_ratio 1.73** (fires: the rule is >= 1.5 and this is exactly 1.5) |
| Saturday | Midday | 6 | 384.0 | 525.7 | YES | none | **CONFOUND: link, rep_ratio 2.500, type_median_ratio 1.73** |
| Saturday | Evening | 3 | 1,904 | 2,016.7 | NO | not run | not run |
| Saturday | Night | 0 | n/a | n/a | NO | n/a | n/a |
| Sunday | Morning | 0 | n/a | n/a | NO | n/a | n/a |
| Sunday | Midday | 1 | 560 | 560 | NO | not run | not run |
| Sunday | Evening | 0 | n/a | n/a | NO | n/a | n/a |
| Sunday | Night | 0 | n/a | n/a | NO | n/a | n/a |

**28 of 28 cells accounted for. 5 rankable before the concentration check, 4 rankable after it (Thursday-Evening excluded for 2 flags). 3 of the 4 surviving rankable cells carry a format-confound flag: Tuesday-Evening (link, 2.500), Saturday-Midday (link, 2.500), and Saturday-Morning (link, 1.500 exactly). Only Thursday-Midday came through clean, and it was checked, not assumed.**

**Saturday-Morning fires at exactly 1.500 and the rule is `>= 1.5`, so it fires.** `(1/10) / (4/60) = 0.100 / 0.0667 = 1.500`. A threshold written as "greater than or equal to" resolves the boundary case one way and one way only, and the earlier version of this worksheet had it recorded as 1.49 and cleared, which is the exact failure mode a hard threshold exists to prevent.

**Direction is not the same thing as representation, and the worksheet says which is which.** The confound check measures whether a format is over-represented in a window, not whether it lifted that window. On Saturday-Morning the single link post is the 244-engagement post from 2026-04-11, the second-lowest post in a 10-post bucket, so link is over-represented there while dragging the median slightly down. On Saturday-Midday the link post is 402, effectively at the bucket median of 384. On Monday and on Tuesday-Evening the link post is the bucket's top post, which is where the caveat actually bites. All four are reported as fired flags because the rule fired; where the post sits in the bucket is stated next to it so the user is not told a window is inflated when it is not.

**Every one of these flags reaches the user-facing output**, attached to its own row in the best-windows table. An earlier version of this skill glued the confound sentence only to the rank 1 window and left the rest of the column reading "none", which told the reader that three checked-and-flagged windows were clean. The column now carries one of three states per ranked row: a named confound, "checked, no confound", or "not checked". It never says "none".

---

## Part C: the filled worksheet, `profile-maya-torres-free-slice.csv` (30 posts, full precision, timezone NOT confirmed for this run)

### Layer 1: day of week, all 7 buckets

| Day | n | Median | Mean | Rankable? | Concentration flags | Confound check | Notes |
|---|---|---|---|---|---|---|---|
| Monday | 3 | 305 | 638.3 | NO | not run | not run (n<5) | too small to rank; was 9 posts and rankable on the full file, dropped out here because the free slice is a recency window |
| Tuesday | 8 | 677.5 | 702.5 | YES | none | **CONFOUND: link, rep_ratio 1.875, type_median_ratio 2.44** | day-of-week rank 1; photo also hits rep_ratio 1.875 but its median ratio is 1.13, under 1.2, so photo does not fire |
| Wednesday | 1 | 566 | 566 | NO | not run | not run (n<5) | too small to rank |
| Thursday | 7 | 466 | 462.7 | YES | none | checked, no confound (highest rep_ratio is album at 1.714, median ratio 0.67, second condition fails) | |
| Friday | 1 | 388 | 388 | NO | not run | not run (n<5) | too small to rank |
| Saturday | 9 | 398 | 1,008.8 | YES | divergence (mean/median 2.53) | checked, no confound (highest rep_ratio is video at 1.429, under 1.5) | most-posted day; carries the June 6 post |
| Sunday | 1 | 560 | 560 | NO | not run | not run (n<5) | too small to rank |

**7 of 7 buckets accounted for. 3 rankable, 4 not, down from 4 rankable on the full file. All 3 rankable days had the confound check run; 1 fired.**

### Layer 2: day x time band, all 28 possible cells

| Day | Band | n | Median | Mean | Rankable? | Concentration flags | Confound check |
|---|---|---|---|---|---|---|---|
| Monday | Morning | 1 | 305 | 305 | NO | not run | not run |
| Monday | Midday | 1 | 1,402 | 1,402 | NO | not run | not run |
| Monday | Evening | 1 | 208 | 208 | NO | not run | not run |
| Monday | Night | 0 | n/a | n/a | NO | n/a | n/a |
| Tuesday | Morning | 3 | 512 | 468.3 | NO | not run | not run |
| Tuesday | Midday | 0 | n/a | n/a | NO | n/a | n/a |
| Tuesday | Evening | 4 | 903.5 | 878.8 | NO | not run | not run |
| Tuesday | Night | 1 | 700 | 700 | NO | not run | not run |
| Wednesday | Evening | 1 | 566 | 566 | NO | not run | not run |
| Wednesday | (other 3 bands) | 0 | n/a | n/a | NO | n/a | n/a |
| Thursday | Morning | 1 | 466 | 466 | NO | not run | not run |
| Thursday | Midday | 5 | 540 | 483.6 | YES | median-shift (-25.4% after top post removed) | checked, no confound (text rep_ratio 1.500 exactly, which clears the first condition, but text's median ratio is 0.75, so the second condition fails) |
| Thursday | Evening | 1 | 355 | 355 | NO | not run | not run |
| Thursday | Night | 0 | n/a | n/a | NO | n/a | n/a |
| Friday | Morning | 1 | 388 | 388 | NO | not run | not run |
| Friday | (other 3 bands) | 0 | n/a | n/a | NO | n/a | n/a |
| Saturday | Morning | 4 | 366.0 | 364.2 | NO | not run | not run |
| Saturday | Midday | 2 | 786.0 | 786 | NO | not run | not run |
| Saturday | Evening | 3 | 1,904 | 2,016.7 | NO | not run | not run |
| Saturday | Night | 0 | n/a | n/a | NO | n/a | n/a |
| Sunday | Midday | 1 | 560 | 560 | NO | not run | not run |
| Sunday | (other 3 bands) | 0 | n/a | n/a | NO | n/a | n/a |

**28 of 28 cells accounted for. 1 rankable, down from 5 on the full file.** Thursday-Midday clears the floor by exactly one post (n=5) and carries a caveat of its own. There is nothing to compare it against yet in this layer.

---

## Part D: what this worksheet is for

**Every claim in `example-run.md` traces to a row in this worksheet.** If a number in the output does not have a matching row here, it was not computed, it was guessed, and that is a defect to fix before shipping.

**The zero cells matter as much as the winners.** 23 of the 28 possible cells on the full file, and 27 of 28 on the free slice, never reach the 5-post floor. That ratio is the honest headline of this whole skill: day-of-week is a real layer almost immediately, day-by-time is a real layer only on a deep capture, and a worksheet that hides the empty cells hides exactly the fact a free-tier user most needs to see.
