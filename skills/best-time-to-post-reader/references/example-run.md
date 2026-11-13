# example-run.md

> **SYNTHETIC.** Maya Torres is a fictional creator. Every post, number, and date below is invented. Primary source file: `../../_shared/synthetic-data/profile-maya-torres.csv`. Appendix source file: `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv`. Nothing here describes a real person or a real Facebook account.

This is the rubric in `rubric.md` executed start to finish on both fixtures, with every number computed from the source files rather than estimated. Anyone can re-run the parse and check. If a number here disagrees with a recomputation from the CSVs, this file is wrong and gets fixed.

**This file's Part 1 is the working record and the source of truth.** `references/bucket-evidence-worksheet.md` mirrors every bucket computed below, including the ones too small to rank, organized for audit rather than narrative. The two files must agree; if they ever do not, this file wins and the worksheet gets corrected.

Version 1.0 | 2026-08-04

---

# RUN 1: the full 60-post capture, timezone confirmed

# PART 1: THE WORK

Everything in Part 1 is the analyst's working, shown so the method is auditable. Part 2 is what the user actually receives.

---

## Step 1: Parse and validate

```
rows parsed                60
date range                 2026-03-21 to 2026-07-28
span                       130 days
midnight_share             0 of 60 (0.0 percent)
precision                  full time-of-day on every row
row order in file          newest first, sorted by parsed Posted before bucketing
lite mode                  OFF (60 posts >= 40, 130 days >= 60)
corpus median engagement   458.5
corpus mean engagement     639.7
```

No date-only degrade needed. Full two-layer method runs.

---

## Step 2: The timezone question

Asked at the start of this run. **For this worked example, the user answered: "Pacific time, America/Los_Angeles."** Every clock time in Part 2 of this run uses that confirmation and names it. (Run 2, the free-tier appendix, demonstrates the opposite case: unconfirmed, relative-language-only output.)

---

## Step 3: Bucketing, both layers

**Day-of-week counts:**

| Day | n |
|---|---|
| Monday | 9 |
| Tuesday | 12 |
| Wednesday | 1 |
| Thursday | 17 |
| Friday | 1 |
| Saturday | 19 |
| Sunday | 1 |

4 of 7 days clear the 5-post floor: Monday, Tuesday, Thursday, Saturday. Wednesday, Friday, and Sunday do not (1 post each), and are each a single post that happened to land on a day Maya rarely uses, not a measurement of that day.

**Day x time-band grid, full 60-post capture. Cell format is `n` for cells under the 5-post floor, `n: median` for cells that clear it.**

| Day | Morning (5-11am) | Midday (11am-5pm) | Evening (5-9pm) | Night (9pm-5am) |
|---|---|---|---|---|
| Monday | 3 | 3 | 2 | 1 |
| Tuesday | 3 | 1 | **6: 712.0** | 2 |
| Wednesday | 0 | 0 | 1 | 0 |
| Thursday | 4 | **7: 355** | **6: 612.5** | 0 |
| Friday | 1 | 0 | 0 | 0 |
| Saturday | **10: 335.5** | **6: 384.0** | 3 | 0 |
| Sunday | 0 | 1 | 0 | 0 |

**5 of 28 possible cells clear the floor:** Tuesday-Evening (6), Thursday-Midday (7), Thursday-Evening (6), Saturday-Morning (10), Saturday-Midday (6). The other 23 range from 0 to 4 posts.

---

## Step 4: Concentration check on every rankable bucket

**Day-of-week layer:**

| Day | n | median | mean | top post | median after removing top | change | top share | mean/median | Flags |
|---|---|---|---|---|---|---|---|---|---|
| Monday | 9 | 341 | 451.9 | 1,402 | 323.0 | -5.3% | 34.5% | 1.33 | none |
| Tuesday | 12 | 521.0 | 602.6 | 1,188 | 520 | -0.2% | 16.4% | 1.16 | none |
| Thursday | 17 | 540 | 752.4 | 4,118 | 514.0 | -4.8% | 32.2% | 1.39 | none |
| Saturday | 19 | 388 | 672.6 | 3,402 | 377.0 | -2.8% | 26.6% | 1.73 | **divergence** |

Saturday's mean is carried by the 3,402-engagement post from 2026-06-06 (the "4 rules that keep my pantry alive" post). The median, 388, is the number that describes a normal Saturday post.

**Day x band layer:**

| Cell | n | median | mean | top post | median after removing top | change | top share | mean/median | Flags |
|---|---|---|---|---|---|---|---|---|---|
| Tuesday-Evening | 6 | 712.0 | 742.8 | 1,188 | 522 | -26.7% | 26.7% | 1.04 | **median-shift** |
| Thursday-Evening | 6 | 612.5 | 1,175.7 | 4,118 | 610 | -0.4% | 58.4% | 1.92 | **top-share, divergence** |
| Saturday-Midday | 6 | 384.0 | 525.7 | 1,206 | 366 | -4.7% | 38.2% | 1.37 | none |
| Thursday-Midday | 7 | 355 | 441.6 | 826 | 336.5 | -5.2% | 26.7% | 1.24 | none |
| Saturday-Morning | 10 | 335.5 | 357.6 | 702 | 327 | -2.5% | 19.6% | 1.07 | none |

**Thursday-Evening carries two flags and is excluded from ranking.** It is carried by the single 4,118-engagement post from 2026-05-07, the pantry client story, which is 58.4 percent of the bucket's total engagement on its own. It becomes "one post did something worth studying," not a recommended window. Notice this is the same post that also lifts the Thursday day-of-week median, but at 17 posts wide that layer does not trip its own flags, which is exactly why this skill runs two layers instead of one.

Tuesday-Evening carries one flag (median-shift, -26.7 percent after removing its top post, the 1,188-engagement link post from 2026-06-23). One flag does not exclude a bucket from ranking; it goes inline next to the number.

---

## Step 5: Format-confound check on every rankable bucket in both layers

Per-Type medians, whole capture, n=60, corpus median 458.5:

| Type | n | median | ratio to corpus median |
|---|---|---|---|
| link | 4 | 795 | 1.73 |
| video | 14 | 585 | 1.28 |
| album | 8 | 393 | 0.86 |
| photo | 17 | 388 | 0.85 |
| text | 17 | 388 | 0.85 |

Every rankable bucket in both layers gets this check, not just the winner, and every ranked row in Part 2 carries the result. Three states only: a named confound, "checked, no confound", or "not checked". The confound result never reads "none". (The Flags column in the Step 4 tables above is the concentration check, a different check, and "none" there is unambiguous because those tables list only rankable buckets and all three parts ran on every row.)

**Day-of-week layer, all 4 rankable days:**

| Day | Highest rep_ratio | Its median ratio | Result |
|---|---|---|---|
| Thursday (rank 1, 540, n=17) | album 3/17, 1.32 | 0.86 | **checked, no confound.** Nothing clears 1.5. Text is 6/17 at 1.25, video 4/17 at 1.01, photo 4/17 at 0.83. Thursday's number is not a format effect. |
| Tuesday (rank 2, 521.0, n=12) | photo 5/12, 1.47 | 0.85 | **checked, no confound.** Photo comes closest and still misses the first condition, and would fail the second anyway. Link is 1/12 at 1.25. |
| Saturday (rank 3, 388, n=19) | link 2/19, **1.58** | **1.73** | **CONFOUND flagged.** 10.5 percent of Saturday against a 6.7 percent corpus share, and link is Maya's strongest format. |
| Monday (rank 4, 341, n=9) | link 1/9, **1.67** | **1.73** | **CONFOUND flagged.** `(1/9) / (4/60) = 1.67`. That single link post is also Monday's top post, 1,402 engagements on 2026-07-20, so this is the flag with the most bite in the file. |

**Day x band layer, all 4 ranked cells:**

| Cell | Highest rep_ratio | Its median ratio | Result |
|---|---|---|---|
| Tuesday-Evening (rank 1, 712.0, n=6) | link 1/6, **2.500** | **1.73** | **CONFOUND flagged.** `(1/6) / (4/60) = 0.167 / 0.067 = 2.500`. The link post, 1,188 engagements on 2026-06-23, is also the bucket's top post and the same post that fired the median-shift flag in Step 4. One post, two checks. |
| Saturday-Midday (rank 2, 384.0, n=6) | link 1/6, **2.500** | **1.73** | **CONFOUND flagged.** Same ratio as Tuesday-Evening, different post: the 402-engagement link from 2026-05-16, which sits essentially at this bucket's median of 384. Over-represented without lifting the window. |
| Thursday-Midday (rank 3, 355, n=7) | text 3/7, 1.51 | 0.85 | **checked, no confound.** Text clears the first condition and fails the second. The only ranked window in this file that comes through clean. |
| Saturday-Morning (rank 4, 335.5, n=10) | link 1/10, **1.500** | **1.73** | **CONFOUND flagged.** `(1/10) / (4/60) = 0.100 / 0.0667 = 1.500`, and the rule is `>= 1.5`, so it fires on the boundary. Text is over-represented harder at 1.76 but its median ratio is 0.85, so text does not fire. |

**The Saturday-Morning boundary case is the one worth reading twice.** It lands on exactly 1.500 against a `>= 1.5` rule. An earlier version of this worked example recorded it as 1.49 and cleared it, which turned a fired flag into a clean row in the shipped table. The value is `(1/10) / (4/60)`, which is `0.1 / 0.0666...`, which is exactly `1.5`. It fires.

**Also worth stating: this flag measures representation, not direction.** Saturday-Morning's link post is the 244-engagement post from 2026-04-11, second-lowest of the 10 posts in that window. Link is over-represented there and is pulling the median slightly down, not up. The flag is still true and still gets reported, and the caveat sentence names where the post sits so the user is not told the window is inflated when it is not.

**Thursday-Evening, excluded from ranking on two concentration flags, checked anyway for the record:** video is 3 of 6, `rep_ratio` 2.14, `type_median_ratio` 1.28. Both clear, so it is format-heavy on top of being outlier-driven. That earns one clause in the excluded-window note, not a paragraph.

---

## Step 6: Ranking

**Day-of-week, rankable buckets only:**

Median order: Thursday (540) > Tuesday (521.0) > Saturday (388) > Monday (341).
Mean order: Thursday (752.4) > Saturday (672.6) > Tuesday (602.6) > Monday (451.9).

**Top 3 disagree.** Saturday and Tuesday swap places. The 3,402-engagement post on 2026-06-06 is the entire difference; removing it drops Saturday below Tuesday on mean too. The median ranking, Thursday then Tuesday then Saturday, is the one shipped.

**Day x band, rankable buckets only (Thursday-Evening excluded per Step 4):**

Median order: Tuesday-Evening (712.0) > Saturday-Midday (384.0) > Thursday-Midday (355) > Saturday-Morning (335.5).
Mean order over the same four: Tuesday-Evening (742.8) > Saturday-Midday (525.7) > Thursday-Midday (441.6) > Saturday-Morning (357.6).

Same order both ways. No disagreement to report at this layer.

---

## Step 7: The schedule gap

Posting share by rankable day: Saturday 19/60 (31.7 percent), Thursday 17/60 (28.3 percent), Tuesday 12/60 (20.0 percent), Monday 9/60 (15.0 percent).

`most_posted` = Saturday. `best_median` = Thursday. **They differ.**

Thursday's median (540) is 39.2 percent higher than Saturday's (388). Saturday is Maya's most-used day and its second-lowest median among the four rankable days. Monday is lower still (341), but Monday is also her least-used of the four, so the actionable gap is Saturday: high volume, middling return.

Day x band layer: the finer-grained winner is Tuesday-Evening, which is only 6 of 60 posts (10.0 percent), and no single day x band cell dominates Maya's posting habit the way Saturday does at the day level (Saturday-Morning is the largest single cell at 10/60, 16.7 percent, and it is not the winner). The day x band layer is too spread out to name one dominant slot to shift away from; the day-of-week gap above is the one to act on first.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable for Run 1. Part 1 was the working.

---

# Best time to post: Maya Torres

60 posts, 2026-03-21 to 2026-07-28, 130 days. Times below are in America/Los_Angeles, which you confirmed.

Engagement here means reactions plus comments plus shares. Corpus median: 458.5.

---

## Your weekly heat grid

Each cell shows post count and median engagement. Cells below the 5-post floor show the count only and are not ranked.

| Day | Morning (5-11am) | Midday (11am-5pm) | Evening (5-9pm) | Night (9pm-5am) |
|---|---|---|---|---|
| Monday | 3 | 3 | 2 | 1 |
| Tuesday | 3 | 1 | **6: 712** | 2 |
| Wednesday | 0 | 0 | 1 | 0 |
| Thursday | 4 | **7: 355** | **6: 613** | 0 |
| Friday | 1 | 0 | 0 | 0 |
| Saturday | **10: 336** | **6: 384** | 3 | 0 |
| Sunday | 0 | 1 | 0 | 0 |

5 of 28 possible day-by-time windows clear the 5-post floor. The rest are shown with their count only, because a 1 to 4 post median is not a measurement.

---

## Your best days

| Rank | Day | Posts | Median engagement | Flags |
|---|---|---|---|---|
| 1 | Thursday | 17 | 540 | Concentration checked, clean. Format checked, no confound. |
| 2 | Tuesday | 12 | 521 | Concentration checked, clean. Format checked, no confound. |
| 3 | Saturday | 19 | 388 | Mean/median 1.73, carried partly by your 3,402-engagement post from June 6. Format: link posts are 2 of these 19, 1.58 times their normal share of your account, and links are your strongest format at 795 median against your 458.5. |
| 4 | Monday | 9 | 341 | Format: 1 of these 9 is a link post, 1.67 times a link post's normal share, and that post is also Monday's best at 1,402. Take Monday's number as 8 ordinary posts plus one strong link post, not as a Monday effect. |

**Too small to rank:** Wednesday (1 post, 566), Friday (1 post, 388), Sunday (1 post, 560). Each is one post on a day you rarely use, not a finding about that day.

**Ranked by average instead, Saturday would be second and Tuesday third.** Your 3,402-engagement post on June 6 is the entire difference. The ranking above is by median, because it describes what a normal post on that day earns, and that is the ranking that survives a week where you did not post anything extraordinary.

---

## Your best windows (day and time)

| Rank | Window | Posts | Median engagement | Flags |
|---|---|---|---|---|
| 1 | Tuesday, Evening (5-9pm) | 6 | 712 | Your median here shifts 26.7 percent, down to 522, if your best post in this window is removed. That same post is a link post, 2.5 times a link post's normal share of your account, and links are your strongest format overall at 795 median against your 458.5 corpus median. One post, both caveats. Test the window and the format separately before you commit to either. |
| 2 | Saturday, Midday (11am-5pm) | 6 | 384 | Format: 1 of these 6 is a link post, 2.5 times a link post's normal share. That post earned 402, right at this window's median, so the format is over-represented here without doing much to the number. |
| 3 | Thursday, Midday (11am-5pm) | 7 | 355 | Concentration checked, clean. Format checked, no confound. The only window in this table that came through both checks clean. |
| 4 | Saturday, Morning (5-11am) | 10 | 336 | Format: 1 of these 10 is a link post, exactly 1.5 times a link post's normal share, which is where the flag fires. That post earned 244, second-lowest in the window, so link is over-represented here while pulling the number down, not up. |

**Read the flags column, not just the medians.** Three of your four ranked windows lean on the same thin category: you have 4 link posts in 60, and they land in a way that over-represents them in three separate windows. None of these is a reason to ignore the window. All three are a reason to test the format on purpose, in a window you already trust, before you decide the clock is what moved the number.

**Not shown as a recommendation, named because it is the single most striking post in your file:** Thursday, Evening (5-9pm), 6 posts, median 613. One of those 6, your May 7 pantry client story, pulled 4,118 engagements, 58.4 percent of the whole window's total. Two concentration flags fired on this window, which means it does not get ranked. It is also format-heavy, video 3 of 6. The post is worth studying on its own; the window is not yet worth trusting.

---

## Where you post versus where you win

You post most often on Saturdays, 19 of your 60 posts, 31.7 percent of everything you write. Your best median day is Thursday, at 540 across 17 posts, 39.2 percent higher than Saturday's 388. Saturday is not your worst rankable day (Monday is, at 341), but it is your most-used day and your second-lowest median. Moving some Saturday volume to Thursday is the cheapest change available here: it does not require a new format or a new hook, only a different day.

At the finer day-by-time layer, your top window (Tuesday evening) is only 6 of 60 posts, 10.0 percent, and no single day-by-time slot dominates your schedule the way Saturday does at the day level. That layer is too spread out yet to name one slot to move away from. The day-level gap above is the one to act on first.

---

## What this analysis is standing on

Analyzed 60 posts captured 2026-03-21 to 2026-07-28, 130 days. Rankings use median engagement, which is reactions plus comments plus shares, unweighted. Buckets under 5 posts are listed but not ranked, in both layers. The format-confound check was run on all 8 ranked buckets across the two layers and fired on 5 of them: Saturday and Monday at the day level, Tuesday-Evening, Saturday-Midday, and Saturday-Morning at the window level. Every one of those 5 is a link-post flag, off a total of 4 link posts in the whole capture. Saturday's day-of-week median also carries a divergence flag (mean 1.73 times the median), driven by one post. Tuesday-Evening carries a median-shift flag and a format-confound flag, both tied to the same single link post. Thursday-Evening was excluded from ranking entirely for carrying two concentration flags, and it is format-heavy as well. Times are shown in America/Los_Angeles, the timezone you confirmed. A timezone offset can still shift a late-night post into the next calendar day, which affects day-of-week counts by at most one slot.

Not in your export, so not in this analysis: sponsored or paid-partnership flags, so a boosted post's timing looks identical to an organic one here. Reach or impressions, so a strong window means people who saw it engaged more, not that more people saw it.

PostSnag captures what you scrolled, so this is a sample of your account, not its full history.

Analysis based on 60 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=best-time-to-post-reader

---
---

# RUN 2: the free-tier slice, timezone NOT confirmed

# PART 1: THE WORK

Source: `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv`, the most recent 30 rows of the same account. This run demonstrates both honesty rules at once: an unconfirmed timezone (relative-window language only) and a free-tier capture (most buckets fail the floor).

---

## Step 1: Parse and validate

```
rows parsed                30
date range                 2026-05-30 to 2026-07-28
span                       60 days
midnight_share             0 of 30 (0.0 percent)
lite mode                  ON (30 posts < 40)
corpus median engagement   530.0
corpus mean engagement     712.2
```

## Step 2: The timezone question

Asked at the start of this run. **The user did not answer.** Per the rule, every window below is described in relative terms only. No clock time, and no parenthetical hour range, appears anywhere in Part 2 of this run. Band names (Morning, Midday, Evening, Night) still group the data, because the grouping itself does not depend on knowing the timezone, only the advice to act on a specific clock hour does.

---

## Step 3: Bucketing, both layers

**Day-of-week counts:**

| Day | n |
|---|---|
| Monday | 3 |
| Tuesday | 8 |
| Wednesday | 1 |
| Thursday | 7 |
| Friday | 1 |
| Saturday | 9 |
| Sunday | 1 |

**3 of 7 days clear the floor**, down from 4 of 7 on the full file: Tuesday, Thursday, Saturday. Monday drops out here (3 posts, was 9 on the full file, because the free slice is the most recent 30 posts and most of Maya's Monday posts fall outside that window).

**Day x band grid, free-tier 30-post slice:**

| Day | Morning | Midday | Evening | Night |
|---|---|---|---|---|
| Monday | 1 | 1 | 1 | 0 |
| Tuesday | 3 | 0 | 4 | 1 |
| Wednesday | 0 | 0 | 1 | 0 |
| Thursday | 1 | **5: 540** | 1 | 0 |
| Friday | 1 | 0 | 0 | 0 |
| Saturday | 4 | 2 | 3 | 0 |
| Sunday | 0 | 1 | 0 | 0 |

**1 of 28 possible cells clears the floor: Thursday-Midday, exactly at the line with n=5.** Every other cell has 4 or fewer posts. This is the sharpest single number in this appendix: the free export goes from 5 usable day-by-time cells to 1.

---

## Step 4: Concentration check

**Day-of-week layer:**

| Day | n | median | mean | top post | median after removing top | change | top share | mean/median | Flags |
|---|---|---|---|---|---|---|---|---|---|
| Tuesday | 8 | 677.5 | 702.5 | 1,188 | 655 | -3.3% | 21.1% | 1.04 | none |
| Thursday | 7 | 466 | 462.7 | 826 | 410.5 | -11.9% | 25.5% | 0.99 | none |
| Saturday | 9 | 398 | 1,008.8 | 3,402 | 393.0 | -1.3% | 37.5% | 2.53 | **divergence** |

**Day x band layer:**

| Cell | n | median | mean | top post | median after removing top | change | top share | mean/median | Flags |
|---|---|---|---|---|---|---|---|---|---|
| Thursday-Midday | 5 | 540 | 483.6 | 826 | 403.0 | -25.4% | 34.2% | 0.90 | **median-shift** |

Only one bucket clears the floor at this layer, and it carries a caveat. One flag does not exclude a bucket, so the cell survives, but in lite mode it is reported as a single labeled early signal rather than as a ranked window. See Step 6.

---

## Step 5: Format-confound check

Per-Type medians, free slice, n=30, corpus median 530.0:

| Type | n | median | ratio to corpus median |
|---|---|---|---|
| link | 2 | 1,295.0 | 2.44 |
| video | 7 | 604 | 1.14 |
| photo | 8 | 597.5 | 1.13 |
| text | 8 | 396.5 | 0.75 |
| album | 5 | 355 | 0.67 |

**Tuesday (day-of-week rank 1, median 677.5, n=8).** Types: photo 4/8 (50.0 percent, corpus share 26.7 percent, ratio 1.88, but photo's median ratio is only 1.13, under 1.2, so photo does not clear the second condition). link 1/8 (12.5 percent, corpus share 6.7 percent, ratio 1.88, and link's median ratio is 2.44, well over 1.2). **Confound flagged on link.** One link post out of 8 is doing outsized work in Maya's top rankable window here too, the same dynamic as the full file's Tuesday-Evening bucket.

**Thursday-Midday (the one day x band cell that clears, median 540, n=5).** Types: text 2/5 (40 percent, corpus share 26.7 percent, ratio 1.50, median ratio 0.75, fails the second condition), video 1/5 (ratio 0.86), album 1/5 (ratio 1.20, median ratio 0.67, fails), photo 1/5 (ratio 0.75). **Checked, no confound.** This cell is clean of a format effect, though it still carries the median-shift caveat from Step 4.

**Thursday (day-of-week rank 2, median 466, n=7).** Album 2/7 (ratio 1.714, median ratio 0.67, fails the second condition), text 3/7 (1.607, median ratio 0.75, fails), video 1/7 (0.61), photo 1/7 (0.54). **Checked, no confound.**

**Saturday (day-of-week rank 3, median 398, n=9).** Video 3/9 (ratio 1.429, under 1.5), album 2/9 (1.333), text 2/9 (0.83), photo 2/9 (0.83). Nothing clears the first condition. **Checked, no confound.** Saturday's problem in this slice is the divergence flag from Step 4, not its format mix.

---

## Step 6: Ranking

Median order (day-of-week): Tuesday (677.5) > Thursday (466) > Saturday (398).
Mean order: Saturday (1,008.8) > Tuesday (702.5) > Thursday (462.7).

**Top 3 disagree, same as the full file.** Saturday's 3,402-engagement post from June 6 is the reason, and it survived into this slice because it falls inside the most recent 30 posts. The median ranking, Tuesday first, is the one shipped.

Day x band layer: only one bucket clears the floor, so there is no ranking to compute. Per the lite-mode carve-out in `references/foundations.md` section 5 (condensed; full version in the bundle), that single cell is reported as one labeled **early signal**, outside the best-windows table, never as a ranked window. Lite mode does not report time-of-day windows; the carve-out exists so a cell that genuinely cleared the floor is not deleted, and the "one labeled cell, never a ranked table" limit exists so a single surviving cell is not dressed up as a grid that was actually compared.

---

## Step 7: The schedule gap

Posting share: Saturday 9/30 (30.0 percent), Tuesday 8/30 (26.7 percent), Thursday 7/30 (23.3 percent).

`most_posted` = Saturday. `best_median` = Tuesday. **They differ, the same direction as the full file.** Tuesday's median (677.5) is 70.2 percent higher than Saturday's (398). This slice is only 60 days, but it already shows the same gap the full 130-day file shows: Maya posts most where she wins least, among her rankable days.

---

# PART 2: WHAT THE USER RECEIVES

---

> **Lite mode.** This capture has 30 posts across 60 days. Below 40 posts or 60 days this analysis runs shallow on purpose. Your day-of-week floor clears on 3 of your 7 days. Your day-by-time floor clears on 1 of 28 possible windows. To get a time-of-day answer worth trusting, capture about 60 posts across at least 60 days, so a thin weekday still lands 5 posts in one of four time bands.

# Best time to post: Maya Torres

30 posts, 2026-05-30 to 2026-07-28, 60 days. Times below are relative only. No timezone was confirmed this run, so no clock time appears anywhere in this output. Time bands are named (Morning, Midday, Evening, Night) as groupings, not as advice to post at a specific hour.

Engagement here means reactions plus comments plus shares. Corpus median: 530.0.

---

## Your weekly heat grid

| Day | Morning | Midday | Evening | Night |
|---|---|---|---|---|
| Monday | 1 | 1 | 1 | 0 |
| Tuesday | 3 | 0 | 4 | 1 |
| Wednesday | 0 | 0 | 1 | 0 |
| Thursday | 1 | **5: 540** | 1 | 0 |
| Friday | 1 | 0 | 0 | 0 |
| Saturday | 4 | 2 | 3 | 0 |
| Sunday | 0 | 1 | 0 | 0 |

Only 1 of 28 possible day-by-time windows clears the 5-post floor in this capture. That window is Thursday's midday band, and it clears by exactly one post.

---

## Your best days

| Rank | Day | Posts | Median engagement | Flags |
|---|---|---|---|---|
| 1 | Tuesday | 8 | 677.5 | Format: 1 of these 8 posts is a link post, 1.88 times a link post's normal share of your account, and links are your strongest format at 1,295 median against your 530 corpus median. |
| 2 | Thursday | 7 | 466 | Concentration checked, clean. Format checked, no confound. |
| 3 | Saturday | 9 | 398 | Mean/median 2.53, carried by your 3,402-engagement post from June 6, which is inside this 30-post slice. Format checked, no confound. |

**Too small to rank:** Monday (3 posts, 305), Wednesday (1 post, 566), Friday (1 post, 388), Sunday (1 post, 560).

**Ranked by average instead, Saturday would be first and Tuesday second.** The June 6 post is the entire difference. The ranking above is by median.

---

## Your best windows (day and time)

**No best-windows table this run.** Lite mode does not produce one. 1 of your 28 possible day-by-time windows cleared the 5-post floor, so there is no grid to rank, and a one-row table with a rank number on it would imply 27 comparisons that never happened.

## Early signal (one window, not a ranking)

**Thursday, midday band. 5 posts, median 540.** This is the only day-by-time cell in your capture that reaches the 5-post floor, and it clears it by exactly one post.

It is reported here, on its own, because a cell that cleared the floor is real evidence and deleting it to honor lite mode would throw away the most specific thing in this run. It is **not** a rank, not a "best window", and not comparable to anything, because the other 27 cells never produced enough posts to be compared against.

Two caveats travel with it. Its median shifts 25.4 percent, down to 403, if its single best post is removed. Its format check ran and came back clean. Treat it as one thing worth testing on purpose next month, not as an answer.

---

## Where you post versus where you win

You post most often on Saturdays, 9 of your 30 posts, 30.0 percent. Your best median day, of the 3 that clear the floor, is Tuesday, at 677.5, which is 70.2 percent higher than Saturday's 398. This is the same direction the fuller capture shows: your busiest day is not your best one.

---

## What this analysis is standing on

Analyzed 30 posts captured 2026-05-30 to 2026-07-28, 60 days. Rankings use median engagement, unweighted. Buckets under 5 posts are listed but not ranked. Saturday's median carries a divergence flag, driven by one post. The format-confound check ran on all 3 ranked days and fired on 1: Tuesday, tied to a single link post. No timezone was confirmed this run, so every time-of-day finding above is relative, not a clock time. This run is in lite mode, so it ships no best-windows table; the one day-by-time cell that cleared the floor is reported as a single labeled early signal instead.

This capture clears the day-of-week floor on 3 of your 7 days and the day-by-time floor on 1 of 28 possible windows. Day-of-week findings above are real. Time-of-day is not usable yet. To get a time-of-day answer worth trusting, capture about 60 posts across at least 60 days.

Not in your export, so not in this analysis: sponsored or paid-partnership flags. Reach or impressions.

PostSnag captures what you scrolled, so this is a sample of your account, not its full history.

Analysis based on 30 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=best-time-to-post-reader
