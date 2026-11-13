# rubric.md

The full method for Best Time to Post Reader. Written so an agent with no other context can execute it and reach the same numbers as anyone else running it on the same file.

Version 1.0 | 2026-08-04

---

## Section 0: Two layers, not one

This skill buckets posts two different ways and treats them as two different confidence tiers, not one grid:

1. **Day-of-week alone.** 7 buckets. Coarser, but every post in the capture has enough neighbors to clear the 5-post floor unless a day is genuinely rare in the account's schedule.
2. **Day of week crossed with time band.** Up to 28 buckets (7 days x 4 bands). Finer, more useful if it clears, and much more likely not to. On the shared 60-post synthetic file, only 5 of the 28 possible cells clear the 5-post floor. On the 30-post free-tier slice, exactly 1 does.

**Report both layers, and say which one is doing the work.** A user with a thin capture still gets a real, ranked day-of-week answer. A user with a deep capture gets the finer grid on top of it. Never present the coarse layer as if it were the fine one, and never let a fine-layer finding stand without saying how many cells around it failed to clear.

---

## Section 1: The four time bands, and why these four

A wrong number presented with confidence is worse than no number.

```
Morning   05:00 to 10:59
Midday    11:00 to 16:59
Evening   17:00 to 20:59
Night     21:00 to 04:59
```

**Why four bands and not six or eight.** More bands mean more buckets, and more buckets mean more of them fail the 5-post floor before they say anything. Four bands is the coarsest split that still separates the parts of a day people actually talk about separately: before the workday, the middle of it, after it, and the hours most people are not looking at a feed. Splitting Evening into "early evening" and "late evening" sounds more precise and produces two 3-post buckets instead of one 6-post bucket, which is a worse outcome dressed as more detail.

**Why these boundaries and not clock-round ones.** The bands are built around behavior, not the clock:

- **Morning (5am-10:59am)** covers the pre-work and early-work window, when a check-in is quick and the read is often on a commute or over coffee.
- **Midday (11am-4:59pm)** is the long stretch most people are working or otherwise occupied, with lunch somewhere in the middle of it. It is wide because attention during it is thin and scattered, not concentrated at one point.
- **Evening (5pm-8:59pm)** is dinner through prime scrolling time, the window every "best time to post" article means when it says "evening" without defining it.
- **Night (9pm-4:59am)** is late scrolling through the dead hours. It is the only band that crosses midnight, which is deliberate: a post at 11pm and a post at 1am belong to the same behavioral window even though they are on different calendar dates.

**These bands are a working definition, not a platform fact.** Facebook does not publish engagement windows, and this skill does not claim inside knowledge of the feed algorithm. The bands exist so that two different runs of this skill on two different exports bucket time the same way and produce comparable results, which is the whole point of a fixed definition instead of an ad hoc one each time.

---

## Section 2: The timezone gate, run before step 1 produces any clock-time output

**The rule, restated from `references/csv-parse.md` section 4 (condensed; full version in the bundle), because this skill is the one where it matters most:**

1. Ask, once, up front: "Your `Posted` timestamps have no timezone attached. Are they in your local time, and if so which timezone? I need this before I can tell you what hour to post."
2. **If confirmed:** use it everywhere a clock time appears in the output, and name it every time ("Tuesday, 5pm to 9pm, in the timezone you confirmed, America/Los_Angeles").
3. **If not confirmed:** the entire output switches to relative-window language. Every finding is phrased as a ratio or a comparison, never a clock time. "Your evening posts earn 1.6x your morning posts on median engagement" is true regardless of timezone. "Post at 7pm" is not, and if the timestamps turn out to be UTC, that advice is off by hours in a direction the user cannot guess.

**Day-of-week gets a lighter version of the same caveat, always, confirmed or not.** A timezone offset can move a post logged at 11:47pm into the next calendar day depending on where the boundary falls. State this once, in one clause, in the honesty footer. Do not turn it into a paragraph, and do not let it block day-of-week findings the way an unconfirmed timezone blocks clock-time findings, because a day shifting by at most one slot is a much smaller error than a clock time being off by a full offset.

---

## Section 3: Precision check, run before bucketing

From `references/csv-parse.md` section 4 (condensed; full version in the bundle):

```
midnight_share = count(rows where time-of-day == 00:00:00) / total rows

if midnight_share > 0.5:
    the whole capture is DATE-ONLY precision
    skip every time-of-day section, in both layers
    run day-of-week only, and say so in one plain sentence at the top of the output
```

**When the capture is mixed** (some rows precise, some sitting at exactly `T00:00:00`), run time-of-day analysis on the precise rows only, state that row count out loud, and apply the same 5-post floor to that smaller pool. Day-of-week analysis still runs on the full capture, because a date without a time still tells you which day of the week it was.

On the shared synthetic fixtures, both `profile-maya-torres.csv` and its free-tier slice carry full time-of-day precision on every row (`midnight_share = 0`), so both example runs in this skill exercise the full two-layer method. `competitor-jordan-lee.csv` is the fixture that exercises the mixed-precision path (12 of 40 rows date-only, 30 percent, under the threshold), and is a reference worth reading if you need to see that branch worked through, though it is not a Maya-Torres file and is not this skill's primary example.

---

## Section 4: Bucketing procedure

1. Parse every `Posted` value as a timestamp, sort ascending. (Sorting matters less here than in other skills since no era adjustment happens, but it is still required before reporting a date range or a span, per `references/csv-parse.md` section 4.)
2. For each post, compute `weekday = Posted.weekday_name` and `band = time_band(Posted.hour)` using the table in Section 1.
3. Group into 7 day-of-week buckets and up to 28 day x band buckets. A bucket that never occurs in the data is not reported as `n=0` in the main output; it is folded into the "no posts in this window" note so the grid does not carry 20 empty rows.
4. For every bucket in both layers: `n`, median engagement, mean engagement, the highest post in the bucket and its engagement.
5. Split into rankable (`n >= 5`) and unrankable (`n < 5`) per bucket, in each layer independently. A day can be rankable at the day-of-week layer while every one of its four day x band cells is unrankable. Report both truths; they are not a contradiction.

**Worked counts from `profile-maya-torres.csv` (60 posts, 130 days), computed and re-derivable from the file:**

| Day | n | Rankable (day-of-week) |
|---|---|---|
| Monday | 9 | yes |
| Tuesday | 12 | yes |
| Wednesday | 1 | no |
| Thursday | 17 | yes |
| Friday | 1 | no |
| Saturday | 19 | yes |
| Sunday | 1 | no |

Day x band cells that clear `n >= 5`: Tuesday-Evening (6), Thursday-Evening (6), Thursday-Midday (7), Saturday-Midday (6), Saturday-Morning (10). That is 5 of 28 possible cells. The other 23 cells range from `n=0` to `n=4`.

---

## Section 5: The format-confound check

**The problem this catches.** A creator who happens to post video on Tuesday nights and text posts at lunch will see "Tuesday night wins" in a naive read, and the honest cause might be "video wins, and I happen to post video on Tuesday nights." A time recommendation that is secretly a format recommendation sends the user to test the wrong variable.

**Run this on every rankable bucket in both layers, not only on the winner.** A ranked row the user can read is a row the user can act on, so every ranked row needs the check behind it. The confound result records one of exactly three states per ranked bucket, and **the confound result never reads "none"**:

- the named confound, with both ratios and the post count driving it
- **"checked, no confound"**, which is a result
- **"not checked"**, which is an admission

"None" collapses the second and third into one word and hands the reader a clean-looking column that may contain nothing but unexamined buckets. That is worse than a flag, because a flag at least tells the truth about what was looked at.

```
For the bucket, and for each post Type present in it:

  type_share_bucket  = count(that Type in the bucket) / n_bucket
  type_share_corpus   = count(that Type across the whole capture) / N
  rep_ratio            = type_share_bucket / type_share_corpus

  type_median_corpus   = median engagement of that Type across the WHOLE capture
  corpus_median         = median engagement across the whole capture
  type_median_ratio     = type_median_corpus / corpus_median

  FLAG if rep_ratio >= 1.5  AND  type_median_ratio >= 1.2
```

**Both conditions have to be true.** A format can be over-represented in a window without being a strong format (no confound: the window's advantage is not explained by it). A format can be a strong performer corpus-wide without being over-represented in the window (no confound: the window is not leaning on it more than usual). Only when a format is both concentrated in the window and itself a winner does the window's number need the caveat.

**When it fires:** name the type, both ratios, and the actual post count driving it, glued into the same sentence as the recommendation, not a trailing note. "Tuesday evening's median is 712 across 6 posts, but link posts make up 1 of those 6, which is 2.5 times their normal share of your account, and links are your best-performing format corpus-wide at 795 median against your 458.5 overall. Some of Tuesday evening's number is a link-post number, not a time number."

**Worked check, `profile-maya-torres.csv`, per-Type corpus-wide medians (n=60, corpus median 458.5):**

| Type | n | median | ratio to corpus median |
|---|---|---|---|
| link | 4 | 795 | 1.73 |
| video | 14 | 585 | 1.28 |
| album | 8 | 393 | 0.86 |
| photo | 17 | 388 | 0.85 |
| text | 17 | 388 | 0.85 |

Only `link` and `video` clear the 1.2 median-ratio half of the test. `link` is thin (4 posts total in the whole capture), so any bucket containing even one link post can swing its representation ratio hard.

**Run against all four rankable day-of-week buckets:**

- **Thursday (rank 1, median 540, n=17):** video 4/17 (`rep_ratio` 1.01), album 3/17 (1.32), text 6/17 (1.25), photo 4/17 (0.83). Nothing clears 1.5. **Checked, no confound.** Thursday's number is not explained by an over-represented strong format.
- **Tuesday (rank 2, median 521.0, n=12):** photo 5/12 (1.47), link 1/12 (1.25), video 3/12 (1.07), album 1/12 (0.63), text 2/12 (0.59). The highest is photo at 1.47, under the 1.5 line, and photo's `type_median_ratio` is 0.85 so it would fail the second condition regardless. **Checked, no confound.**
- **Saturday (rank 3, most-posted day, n=19, median 388):** link is 2/19 (10.5 percent) against a corpus share of 6.7 percent, `rep_ratio = 1.58`, and link's `type_median_ratio` is 1.73. **Both clear. Confound flagged**, and it goes on Saturday's row in the shipped table, not only in the worksheet.
- **Monday (rank 4, median 341, n=9):** link is 1/9 (11.1 percent), `rep_ratio = (1/9) / (4/60) = 1.67`, `type_median_ratio = 1.73`. **Both clear. Confound flagged.** The link post here is also Monday's top post, the 1,402-engagement post from 2026-07-20, so this is the case where the caveat bites hardest.

**Run against all four ranked day x band cells:**

- **Tuesday-Evening (rank 1, median 712, n=6):** types are album 1, video 2, photo 2, link 1. Link's `rep_ratio = (1/6) / (4/60) = 0.167 / 0.067 = 2.500`, and link's `type_median_ratio = 1.73`. **Both clear. Confound flagged.** One link post, the 1,188-engagement post from 2026-06-23, is the bucket's top post and is doing outsized work in a 6-post bucket. State it plainly: this window's evidence leans partly on a single strong-format post, not purely on the time slot.
- **Saturday-Midday (rank 2, median 384.0, n=6):** link 1/6, `rep_ratio = 2.500`, `type_median_ratio = 1.73`. **Both clear. Confound flagged.** The link post here is the 402-engagement post from 2026-05-16, sitting essentially at the bucket's median of 384, so the format is over-represented without lifting the window much.
- **Thursday-Midday (rank 3, median 355, n=7):** text 3/7, `rep_ratio = 1.51`, clears the first condition, but text's `type_median_ratio` is 0.85 and fails the second. Album 1.07, photo 1.01, video 0.61. **Checked, no confound.** This is the only ranked window in the file that comes through clean.
- **Saturday-Morning (rank 4, median 335.5, n=10):** link 1/10, `rep_ratio = (1/10) / (4/60) = 0.100 / 0.0667 = 1.500`, `type_median_ratio = 1.73`. The rule is `>= 1.5`, so **it fires. Confound flagged.** Text is also over-represented at 1.76 but its median ratio is 0.85, so text does not fire. The link post here is the 244-engagement post from 2026-04-11, the second-lowest in the bucket, which means link is over-represented while pulling the window's number slightly down rather than up.

**Representation is not direction, and the output says which one it found.** This check answers "is a strong format concentrated in this window", not "did that format lift this window". Three of the four ranked windows above fire on the same thin link category, and the link post sits at the top of the bucket in one of them, at the median in another, and near the bottom in the third. Report the flag every time it fires, and name where the post actually sits, because "your window is inflated by a link post" is a false statement about Saturday-Morning even though the flag is a true one.

**And on the boundary case specifically:** 1.500 against a `>= 1.5` rule fires. It does not "come within a hair". A threshold that gets read as approximate on the one occasion it lands exactly on the line is not a threshold.

**What this check does not do.** It does not remove the bucket from the ranking and it does not downgrade a single flag into an exclusion, the way two concentration-check flags do. A format confound is reported as a caveat glued to the recommendation, always, every time it fires, because a user can still act on "test this window, but also test whether it is the format" and that is more useful than hiding the window entirely.

---

## Section 6: The concentration check, applied here

Full definition and thresholds: `references/foundations.md` section 4 (condensed; full version in the bundle). Run all three parts on every bucket about to become a recommendation, same as any other skill in the catalog: median-after-deleting-the-top-post, the top post's share of the bucket total, mean over median.

**Worked results on the rankable day-of-week buckets, `profile-maya-torres.csv`:**

| Day | n | median | mean | median after deleting top | change | top post's share | mean/median | Flags |
|---|---|---|---|---|---|---|---|---|
| Monday | 9 | 341 | 451.9 | 323.0 | -5.3% | 34.5% | 1.33 | none |
| Tuesday | 12 | 521.0 | 602.6 | 520 | -0.2% | 16.4% | 1.16 | none |
| Thursday | 17 | 540 | 752.4 | 514.0 | -4.8% | 32.2% | 1.39 | none |
| Saturday | 19 | 388 | 672.6 | 377.0 | -2.8% | 26.6% | 1.73 | **divergence** |

Saturday's mean is carried upward by its one 3,402-engagement post (the number-promise pantry post from 2026-06-06). The median, 388, is the honest number for a normal Saturday post, and it is also the lowest of the four rankable days.

**Worked results on the 5 rankable day x band cells, same file:**

| Cell | n | median | mean | median after deleting top | change | top share | mean/median | Flags |
|---|---|---|---|---|---|---|---|---|
| Tuesday-Evening | 6 | 712.0 | 742.8 | 522 | **-26.7%** | 26.7% | 1.04 | **median-shift** |
| Thursday-Evening | 6 | 612.5 | 1,175.7 | 610 | -0.4% | 58.4% | 1.92 | **top-share, divergence** |
| Saturday-Midday | 6 | 384.0 | 525.7 | 366 | -4.7% | 38.2% | 1.37 | none |
| Thursday-Midday | 7 | 355 | 441.6 | 336.5 | -5.2% | 26.7% | 1.24 | none |
| Saturday-Morning | 10 | 335.5 | 357.6 | 327 | -2.5% | 19.6% | 1.07 | none |

**Tuesday-Evening fires the median-shift flag.** Delete its top post, the 1,188-engagement link post from 2026-06-23, and the window's median falls from 712.0 to 522, a 26.7 percent move against a 20 percent threshold. Its other two parts pass: the top post is 26.7 percent of the bucket total, and the mean sits 1.04 times the median. One flag does not exclude a bucket from ranking, so Tuesday-Evening still ranks first in this layer, with the flag written inline next to the number. It also carries a format-confound flag from Section 5, on the same post: that post is the link post. Two different checks, one post, and the output names it once and attributes both caveats to it rather than making it sound like two independent problems.

**Thursday-Evening carries two flags, which per `references/foundations.md` section 4 means it does not become a recommendation.** It is the same 4,118-engagement post (the pantry client story, 2026-05-07) that also drives the standalone Thursday day-of-week median upward without tripping that layer's flags, because at 17 posts the same outlier is a much smaller share of a much bigger bucket. This is the two-layer design paying off directly: the outlier that breaks the fine layer does not break the coarse one, and the output should say exactly that rather than silently dropping Thursday-Evening.

**Reading the combined picture.** Tuesday-Evening is the day x band leader by median (712) carrying one concentration flag and one format-confound flag, both traceable to the same 1,188-engagement link post. Thursday-Evening has the single most dramatic post in the file but fails its own concentration check twice, so it is reported as "one post did something worth studying" and the post is named, not turned into a recommendation. It is also format-heavy (video 3 of 6, `rep_ratio` 2.14), which is worth one clause in the excluded-window note.

---

## Section 7: Ranking

1. Rank each layer's rankable buckets by median engagement, descending. Never by mean.
2. Compute the mean-based ranking too. If the top 3 in a layer disagree between median and mean ranking, say so, name the posts responsible, and confirm the median ranking is the one shipped.

**Day-of-week layer, `profile-maya-torres.csv`:**

Median order: Thursday (540) > Tuesday (521.0) > Saturday (388) > Monday (341).
Mean order: Thursday (752.4) > Saturday (672.6) > Tuesday (602.6) > Monday (451.9).

**The top 3 disagree: Saturday and Tuesday swap places.** The 3,402-engagement post on Saturday 2026-06-06 is the reason. Removing it drops Saturday's mean below Tuesday's. The median ranking, with Tuesday ahead of Saturday, is the one shipped, because it describes what a normal Saturday post does, and the flag already named in Section 6 explains why the mean disagreed.

**Day x band layer**, rankable cells only (Thursday-Evening excluded per Section 6): median order Tuesday-Evening (712.0) > Saturday-Midday (384.0) > Thursday-Midday (355) > Saturday-Morning (335.5). Mean order over the same four: Tuesday-Evening (742.8) > Saturday-Midday (525.7) > Thursday-Midday (441.6) > Saturday-Morning (357.6). **Same order in both.** No disagreement to report in this layer.

---

## Section 8: The schedule gap, "you post at X but win at Y"

**The point of this section is a single, concrete, checkable sentence: is the account's actual posting habit aimed at its best window, or somewhere else.**

1. Compute the actual posting share of every rankable bucket in the day-of-week layer: `posting_share = n_bucket / N_total`.
2. Identify `most_posted` = the rankable bucket with the highest `posting_share`.
3. Identify `best_median` = the rankable bucket with the highest median engagement (the layer's rank 1 from Section 7).
4. **If `most_posted == best_median`:** say so plainly. "You already post most often where you win. Nothing to move here."
5. **If they differ:** state both numbers side by side, with the percentage gap between their medians, and name what would change if posting volume shifted toward the winner.
6. **Repeat at the day x band layer only if that layer has at least one rankable cell**, and label it as the finer, thinner-evidence version of the same question, never as a replacement for the day-of-week answer.

**Worked on `profile-maya-torres.csv`:**

Posting share by rankable day: Saturday 19/60 (31.7%), Thursday 17/60 (28.3%), Tuesday 12/60 (20.0%), Monday 9/60 (15.0%).

`most_posted` = Saturday. `best_median` = Thursday (from Section 7). They differ.

"You post most often on Saturdays, 19 of your 60 posts, 31.7 percent of everything you write. Your best median day is Thursday, at 540 across 17 posts, 39.2 percent higher than Saturday's 388. Saturday is not your worst rankable day, Monday is, but it is your most-used day and your second-lowest median. Moving some Saturday volume to Thursday is the cheapest change available: it does not require a new format or a new hook, only a different day."

**Day x band layer, same file:** `best_median` cell is Tuesday-Evening (712, n=6, format-confound caveat noted). Its posting share within the day x band layer is 6/60 (10.0%). This layer is too thin across the board to identify a single dominant "most posted" cell the way the day-of-week layer can; the most any single day x band cell reaches is Saturday-Morning at 10/60 (16.7%), which is itself a rankable cell but not the winner. State this as "your posting habit is too spread out across 28 possible day x time slots to name one dominant slot at this layer, so the day-of-week gap above is the one to act on first."

---

## Section 9: Free-tier and lite-mode behavior, spelled out

**Trigger, from `references/foundations.md` section 5 (condensed; full version in the bundle):** `posts_analyzed < 40 OR span_days < 60`. On the free tier you see 30 posts per profile, so expect an export around that size, which always trips this. A free export is also the most recent 30 posts, not a random 30, which matters here specifically: a schedule reads differently over 60 recent days than over 130 days spanning a season, and this skill says so rather than letting the user assume the free read is just a smaller version of the same answer.

**What degrades on a free export, worked on `profile-maya-torres-free-slice.csv` (30 posts, 2026-05-30 to 2026-07-28, 60 days):**

| Layer | Full file (60 posts) | Free slice (30 posts) |
|---|---|---|
| Day-of-week cells clearing n>=5 | 4 of 7 | 3 of 7 |
| Day x band cells clearing n>=5 | 5 of 28 | 1 of 28 |

**The honest sentence this skill ships instead of a paywall screen:** "This capture clears the day-of-week floor on 3 of your 7 days and the day-by-time floor on 1 of 28 possible windows. Day-of-week findings below are real. Time-of-day is not usable yet. To get a time-of-day answer worth trusting, you need roughly 60 posts spread across 60 or more days, so that even a thin weekday still has 5 posts landing in one of four time bands. Capture that and rerun this same skill, nothing else changes."

**Explain the evidence gap.** State how many additional posts the analysis needs and why, using the reader’s sample counts.

---

## Section 10: What this rubric refuses to do

- **No clock-time claim without a confirmed timezone.** Not "probably," not "assuming Pacific," nothing. Relative-window language only until the user answers the question in Section 2.
- **No time-of-day claim on a date-only capture.** If more than half the timestamps sit at midnight, the precision is not there, and no amount of clever inference recovers it. Day-of-week only, said once, plainly.
- **No ranked bucket under 5 posts, in either layer.** A 3-post window with a great median is listed as untested, not promoted.
- **No ranked bucket, in either layer, without the format-confound check having been run on it.** A clean check is itself worth stating ("checked, no confound"), not silently skipped, and **the confound result never reads "none"**, because "none" reads as clean whether the check ran or not. The concentration-check column in the Section 6 working tables may read "none", because those tables contain only rankable buckets and the check ran on every row in them; the confound column has no such guarantee, which is exactly why it needs the third state.
- **No claim that this schedule caused the engagement.** The account's audience, the news cycle, and a dozen things this export does not capture also move week to week. This skill reports what happened in the posts you have, not why the platform served them the way it did.
- **No comparison to the account's full posting history.** PostSnag captures what you scrolled. A pattern in your export is a pattern in your export.
