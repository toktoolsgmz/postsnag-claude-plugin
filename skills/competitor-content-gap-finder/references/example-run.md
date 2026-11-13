# example-run.md

> **SYNTHETIC.** Maya Torres and Jordan Lee are both fictional creators. Every post, number, and date below is invented. Your-side source file: `../../_shared/synthetic-data/profile-maya-torres.csv`. Competitor-side source file: `../../_shared/synthetic-data/competitor-jordan-lee.csv`. Nothing here describes a real person or a real Facebook account.

This is the rubric in `rubric.md` executed start to finish, with every number computed from the two source files rather than estimated. Anyone can re-run the parse and check. If a number here disagrees with a recomputation from the CSVs, this file is wrong and gets fixed. Maya Torres is playing "you." Jordan Lee is playing the competitor, per the shared dataset's design (`_shared/synthetic-data/README.md`: "the topic overlap with Maya is small on purpose, so a gap analysis finds real gaps in both directions").

Version 1.0 | 2026-08-04

---

# PART 1: THE WORK

Everything in Part 1 is the analyst's working, shown so the method is auditable. Part 2 is what the user actually receives.

---

## Step 1: Parse and validate, both files

```
                          Your file (Maya)          Competitor file (Jordan)
rows parsed               60                         40
date range                2026-03-21 to 2026-07-28    2026-03-05 to 2026-06-30
span                       130 days                    118 days
corpus median engagement   458.5                       243.0
corpus mean engagement     639.7                       317.6
lite mode                  OFF (60>=40, 130>=60)       OFF (40>=40, 118>=60)
```

**Both files clear full mode.** Neither lite-mode banner fires in this run. Section 8 of `rubric.md` and the appendix at the bottom of this file show what changes when the "your file" side is a free-tier 30-post slice instead.

**A note on the competitor file's span.** `_shared/synthetic-data/README.md` describes `competitor-jordan-lee.csv` as running "2026-03-05 to 2026-07-30." The file's actual latest `Posted` value, parsed directly, is 2026-06-30, which is where the 118-day span above comes from. This example run uses the parsed value, not the README's prose, per the standing rule that a number here traces to a computation, never to a description. Flagged for whoever maintains the shared fixture; not something this skill folder can fix.

---

## Step 2: Topic inventory, run independently on each file

### 2a. The failure mode, shown live before the fix

Running Section 1 of `topic-inventory-method.md` with the STOPWORD list but with an EMPTY filler list, against the real 60-post Maya file, produces this (unigrams only, `df >= 5`):

```
Every (13)  Closet (10)  Three (10)  Open (9)  Organizing (9)  Needs (9)  Work (9)
Bins (8)    Keep (8)     Nothing (8) Shelf (8) Second (7)      Minutes (7) Year (7)
Week (7)    Stop (7)     Last (7)    About (7) System (7)      Four (6)   Label (6)
Kitchen (6) Built (6)    Anything (6) Things (6) Drawer (5)    House (5)  Never (5)
Pantry (5)  Failing (5)  Storage (5) Decision (5) Container (5) Nobody (5) Door (5)
Everything (5) Client (5) Problem (5)
```

37 candidate clusters clear the floor. Roughly two thirds of them (`Every`, `Three`, `Open`, `Needs`, `Work`, `Keep`, `Nothing`, `Second`, `Year`, `Week`, `Stop`, `Last`, `About`, `Four`, `Built`, `Anything`, `Things`, `Never`, `Failing`, `Decision`, `Nobody`, `Everything`) are grammatical connective tissue or generic verbs, not subjects the posts are about. This is Failure Mode 1 from `topic-inventory-method.md` section 6, live on real data, not a hypothetical.

**The fix.** The FILLER list in `topic-inventory-method.md` Appendix B already absorbs most of the above (`three`, `four`, `second`, `year`, `week`, `last`, `about`, `things`, `never`, `everything`, `anything`, `nothing`, `needs`, `keep`, `every` and its family are already in the base list). What was NOT yet covered, caught on this run, and added to FILLER: `open`, `opens`, `opened`, `work`, `works`, `worked`, `working`, `built`, `build`, `builds`, `building`, `fail`, `fails`, `failed`, `failing`, `nobody`, `somebody`, `decision`, `decisions`. Those seven word families are the last two lines of Appendix B, and they exist because this run found them, not because someone guessed they might show up.

### 2b. Final clusters, both files, `df >= 5`, after the fix

**Your file (Maya), 16 clusters:**

| Topic | n | Median | Mean | Multiple of your median |
|---|---|---|---|---|
| Container | 5 | 905 | 1,260.2 | 1.97x |
| House | 5 | 712 | 871.2 | 1.55x |
| Pantry | 5 | 712 | 1,827.8 | 1.55x |
| System | 7 | 655 | 698.0 | 1.43x |
| Minutes | 7 | 560 | 1,022.1 | 1.22x |
| Closet | 10 | 530 | 644.6 | 1.16x |
| Bins | 8 | 530 | 989.0 | 1.16x |
| Drawer | 5 | 512 | 634.0 | 1.12x |
| Storage | 5 | 466 | 726.0 | 1.02x |
| Door | 5 | 455 | 1,039.6 | 0.99x |
| Shelf | 8 | 429 | 528.0 | 0.94x |
| Kitchen | 6 | 425 | 424.2 | 0.93x |
| Client | 5 | 402 | 1,126.0 | 0.88x |
| Organizing | 9 | 398 | 560.7 | 0.87x |
| Problem | 5 | 388 | 459.6 | 0.85x |
| Label | 6 | 376.5 | 576.2 | 0.82x |

**Competitor file (Jordan), 6 clusters:**

| Topic | n | Median | Mean | Multiple of their median |
|---|---|---|---|---|
| Dollars | 11 | 255 | 299.3 | 1.05x |
| Rental | 7 | 326 | 372.7 | 1.34x |
| Apartment | 7 | 176 | 243.7 | 0.72x |
| Studio | 5 | 246 | 381.2 | 1.01x |
| Square | 5 | 192 | 290.4 | 0.79x |
| Wall | 5 | 176 | 247.8 | 0.72x |

**No bigram cleared the floor on either file.** Both corpora are too small and too phrase-varied for any two-word combination to reach `df >= 5`. The mechanism exists (Section 4 of `topic-inventory-method.md`) and would fire on a larger capture; on these two files, every surviving cluster is a unigram. That is a real result, not a shortcut: it is reported here instead of silently, because a method that would have caught a phrase and did not needs to say so.

**Topic overlap between the two creators' cluster lists: none.** Not one canonical topic name appears on both sides. This matches the shared dataset's design note directly (`_shared/synthetic-data/README.md`): Maya's clusters are organizing-object nouns (closet, pantry, bins, shelf, drawer, container, kitchen, door, storage, label, system), Jordan's are small-space and rental-market nouns (rental, dollars, apartment, studio, square, wall). Zero overlap on a real run is itself worth stating plainly in the output: it means every candidate gap below is a genuine subject-matter gap, not a naming collision between two creators using different words for the same thing.

---

## Step 3: Format inventory, both files

**Competitor file (Jordan):**

| Type | n | Median | Mean | Multiple of their median | Corpus share | Top-quartile share (k=10) |
|---|---|---|---|---|---|---|
| video | 11 | 576.0 | 589.6 | 2.37x | 27.5% (11 of 40) | 100.0% (10 of 10) |
| album | 7 | 289.0 | 279.7 | 1.19x | 17.5% (7 of 40) | 0.0% (0 of 10) |
| photo | 12 | 224.0 | 224.5 | 0.92x | 30.0% (12 of 40) | 0.0% (0 of 10) |
| text | 10 | 156.0 | 156.8 | 0.64x | 25.0% (10 of 40) | 0.0% (0 of 10) |

Jordan has no `link` posts anywhere in her capture. All 10 of her top-quartile posts are video. Nothing else comes close.

**Your file (Maya):**

| Type | n | Median | Mean | Multiple of your median | Corpus share | Top-quartile share (k=15) |
|---|---|---|---|---|---|---|
| link | 4 | 795.0 | 809.0 | 1.73x | 6.7% (4 of 60) | 13.3% (2 of 15) |
| video | 14 | 585.0 | 1,106.4 | 1.28x | 23.3% (14 of 60) | 33.3% (5 of 15) |
| album | 8 | 393.0 | 407.6 | 0.86x | 13.3% (8 of 60) | 0.0% (0 of 15) |
| photo | 17 | 388.0 | 493.4 | 0.85x | 28.3% (17 of 60) | 26.7% (4 of 15) |
| text | 17 | 388.0 | 471.2 | 0.85x | 28.3% (17 of 60) | 26.7% (4 of 15) |

---

## Step 4: The competitor-winner test, applied to every Jordan bucket

Test per `rubric.md` Section 4: `n >= 5`, over-represented in their own top quartile against their own corpus share, concentration check reported.

| Bucket | Type | n>=5? | Over-rep in top-q? | Concentration flags | Winner? |
|---|---|---|---|---|---|
| Rental | topic | yes (7) | 30.0% vs 17.5%, yes | 1 flag (median-after, see below) | **YES** |
| Studio | topic | yes (5) | 20.0% vs 12.5%, yes | 1 flag (divergence, see below) | **YES** |
| Dollars | topic | yes (11) | 10.0% vs 27.5%, **no** | not run, fails composition first | no, most-used topic that does not win, see note below |
| Apartment | topic | yes (7) | 10.0% vs 17.5%, no | not run | no |
| Square | topic | yes (5) | 10.0% vs 12.5%, no | not run | no |
| Wall | topic | yes (5) | 10.0% vs 12.5%, no | not run | no |
| video | format | yes (11) | 100.0% vs 27.5%, yes | 0 flags (see below) | **YES** |
| album | format | yes (7) | 0.0% vs 17.5%, no | not run | no |
| photo | format | yes (12) | 0.0% vs 30.0%, no | not run | no |
| text | format | yes (10) | 0.0% vs 25.0%, no | not run | no |

**Concentration check, Rental** (`references/foundations.md` section 4, n=7, engagements 629/576/503/326/194/192/189, sum 2,609):
```
top_share       = 629 / 2,609        = 24.1%     (floor is 40%, no flag)
median_after    = median of the other 6 = 260     |260-326|/326 = 20.2%   (floor is >20%, FLAGS)
divergence      = mean/median = 372.7/326 = 1.14   (floor is 1.5, no flag)
```
One flag. Rental still qualifies as a winner (fewer than two flags), and the flag rides with the number in Part 2: dropping Jordan's single best rental post moves the bucket's median by just over the 20 percent line, so the size of "1.34x" carries a little more weight from one post than the other six alone would produce.

**Concentration check, Studio** (n=5, engagements 678/565/246/241/176, sum 1,906):
```
top_share       = 678 / 1,906        = 35.6%     (no flag)
median_after    = median of the other 4 = 243.5   |243.5-246|/246 = 1.0%   (no flag)
divergence      = mean/median = 381.2/246 = 1.55   (floor is 1.5, FLAGS)
```
One flag. Studio still qualifies, with the same rule: reported inline.

**Concentration check, video format** (n=11, engagements 787/718/678/651/629/576/565/514/503/486/379, sum 6,486):
```
top_share       = 787 / 6,486        = 12.1%     (no flag)
median_after    = median of the other 10 = 570.5  |570.5-576|/576 = 1.0%   (no flag)
divergence      = mean/median = 589.6/576 = 1.02   (no flag)
```
Zero flags. This is the cleanest winner in the file: Jordan's video format is not being carried by one viral post, all 11 of her videos sit in a tight band, and every one of her top 10 posts is a video.

**Dollars is worth one line even though it does not qualify.** It is Jordan's single most-used topic, 11 of her 40 posts, 27.5 percent of her file, and its median (255) is barely above her corpus median (1.05x). But it makes up only 10 percent of her top quartile against 27.5 percent of her corpus, which means it under-delivers relative to how often she reaches for it. Copying Jordan's most frequent topic would not copy what makes her account work. That is reported below, not recommended.

---

## Step 5: Cross-profile normalization, stated once, applied everywhere below

Maya's file has a median of 458.5. Jordan's has a median of 243.0. Maya's median is nearly double Jordan's. Nothing in either export explains why: no follower counts (the CSV export carries none at all, and the Markdown export's one point-in-time number would not help here since neither file is a Markdown export), no reach, no account age beyond the post dates themselves. Comparing Jordan's 629-engagement rental post against Maya's 458.5 median directly would produce a number ("Jordan's rental post beat Maya's typical post by 1.37x") that looks exactly like a real finding and proves nothing, because it silently assumes the two accounts are the same size, and there is no field in either file that lets you check that assumption.

**So this analysis never does that.** Every claim about Jordan is `their_cluster_median / their_own_corpus_median`, a ratio computed entirely inside her own file. Every claim about Maya's coverage is a raw count of Maya's own posts, never converted into an engagement figure and never set against Jordan's numbers. Rental at "1.34x their own median" is a claim Jordan's file proves on its own terms. "Zero of your posts touch rental" is a claim Maya's file proves on its own terms. The gap is the fact that one of those two true statements has nothing to answer it, not a raw-number scoreboard between two accounts of unknown relative size.

---

## Step 6: Coverage check, your file against each winning bucket's keyword set

Search Maya's 60 posts for the exact stemmed keyword that defines each Jordan winner cluster, using the identical extraction rules from `topic-inventory-method.md`.

| Winning bucket (Jordan) | Keyword searched | Matching posts in your file | Status |
|---|---|---|---|
| Rental | `rental` | 0 | **ABSENT** |
| Studio | `studio` | 0 | **ABSENT** |
| video (format) | `Type == video` | 14 | **covered, not a gap** (n=14, well above the 5-post floor) |

**The video row is the finding worth sitting with.** On its own, "100 percent of your competitor's top 10 posts are video" reads like the single biggest opportunity in this analysis. Checked against your own file, it is not one: you already publish 14 videos, their video runs 2.37x their own median, yours runs 1.28x yours, and your videos already make up a third of your own top quartile. This is validation that video is worth the time it takes, not a format you are missing. The gap test exists specifically to catch this before it becomes bad advice: a format can look like a slam-dunk opportunity and still fail the ABSENT/UNDERWEIGHTED test the moment you check the other file.

**Rental and Studio are both fully absent.** Neither the word `rental` nor the word `studio`, nor any surface form that stems to them, appears anywhere in Maya's 60 captions.

---

## Step 7: Gap-ranking formula, computed

```
gap_score = their_multiple * absence_factor

Rental: their_multiple = 326 / 243.0 = 1.34   absence_factor = 1.0 (ABSENT)   gap_score = 1.34 * 1.0 = 1.34
Studio: their_multiple = 246 / 243.0 = 1.01   absence_factor = 1.0 (ABSENT)   gap_score = 1.01 * 1.0 = 1.01
```

**Both gaps happen to land at `absence_factor = 1.0` in this run**, because Maya has zero coverage of either keyword. That is a property of this particular pair of files, not the formula: `rubric.md` Section 7 shows the formula's behavior when the user has partial coverage (1 to 4 matching posts), using invented numbers, since neither real gap here exercises that branch. Ranked by `gap_score` descending: **1. Rental (1.34), 2. Studio (1.01).**

**Format:** no bucket cleared the ABSENT/UNDERWEIGHTED test (video is covered, and it is the only format winner Jordan has), so the gap list this run is topic-only. The format inventory table still ships in the output, with its honest empty result, per `output-template.md`.

---

## Step 8: Evidence citations

**Rental, best example, verbatim, in full:**

> Closet system for a rental, built entirely from tension rods and hanging shelves. Comes down in fifteen minutes.

629 engagements (487 reactions, 83 comments, 59 shares). Video. Posted 2026-05-18.

**Studio, best example, verbatim, in full:**

> Making a 380 square foot studio work for two people and a dog. Full tour.

678 engagements (523 reactions, 91 comments, 64 shares). Video. Posted 2026-05-30.

---

## Step 9: The 5 drafted ideas, built from Maya's own voice

Maya's own rankable hook archetypes, per `facebook-hook-analyzer/references/example-run.md` (same shared file, already computed there): Question Open ranks first, 11 posts, median 610. Number Promise ranks second, 7 posts, median 560. Both are used here; nothing from Jordan's sentences is reused anywhere below, only her subject matter.

Only 2 gaps cleared the winner bar this run, so the five drafts split 3 for Rental (the stronger gap, score 1.34) and 2 for Studio (score 1.01), weighted toward the stronger evidence rather than split evenly by default.

**1. Fills: Rental, rank 1**
> What is the first thing you would fix in your rental if your landlord could not say no?

Modeled on your own Question Open archetype (11 posts, median 610). Evidence this fills: Jordan's rental closet system post, 629 engagements, 1.34x her own median.

**2. Fills: Rental, rank 1**
> 3 systems that hold a full pantry when you are not allowed to install a single shelf.

Modeled on your own Number Promise archetype (7 posts, median 560). Evidence this fills: same rental cluster, 7 of Jordan's posts, 3 in her top quartile.

**3. Fills: Rental, rank 1**
> If you could never drill another hole in this apartment, what would you finally get organized?

Modeled on your own Question Open archetype, a second angle on the same gap. Evidence this fills: Jordan's rental vertical-garden post, 576 engagements.

**4. Fills: Studio, rank 2**
> If your whole home was one room, what is the first thing you would get rid of?

Modeled on your own Question Open archetype. Evidence this fills: Jordan's studio-for-two-and-a-dog post, 678 engagements, her single highest-engagement post in either winning cluster.

**5. Fills: Studio, rank 2**
> 2 zones I would build first in one room, and neither one needs a wall.

Modeled on your own Number Promise archetype. Evidence this fills: Jordan's studio-layout-walkthrough post, 565 engagements.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable. Part 1 was the working.

---

# Content gap: your export vs the competitor's export

Your file: 60 posts, 2026-03-21 to 2026-07-28, 130 days, median engagement 458.5.
Their file: 40 posts, 2026-03-05 to 2026-06-30, 118 days, median engagement 243.0.

These two numbers are never compared to each other directly. Every claim about their account below is a multiple of their own median. Every count of your coverage is a raw count of your own posts. Your file's median is nearly double theirs, and nothing in either export explains why (no follower counts, no reach, no account age beyond the post dates), so a raw comparison between your numbers and theirs would assume the two accounts are the same size with no way to check it.

---

## What they win with that you do not touch

| Topic or format | Their evidence (multiple of their own median) | Your coverage | Status | Opportunity rank |
|---|---|---|---|---|
| Rental | 1.34x, 7 of their posts, 30.0% of their top quartile vs 17.5% of their corpus. Dropping their single best rental post moves this median by 20.2 percent, so the number leans on one strong post more than the rest of the six. | 0 of your posts | ABSENT | 1, score 1.34 |
| Studio | 1.01x, 5 of their posts, 20.0% of their top quartile vs 12.5% of their corpus. Their mean runs 1.55x their median here, carried partly by one post. | 0 of your posts | ABSENT | 2, score 1.01 |

**Reported, not recommended:** Dollars, their single most-used topic (11 of 40 posts, 27.5 percent of their file), median 1.05x their own corpus median. It makes up only 10 percent of their top quartile against 27.5 percent of their corpus, which means it under-delivers relative to how often they reach for it. Their most-used topic is not their best one. Copying it would copy volume, not results.

---

## Format inventory

| Type | Their n | Multiple of their own median | Your n | Multiple of your own median | Status |
|---|---|---|---|---|---|
| video | 11 | 2.37x | 14 | 1.28x | covered, not a gap |
| album | 7 | 1.19x | 8 | 0.86x | not a competitor winner (0% of their top quartile despite the multiple) |
| photo | 12 | 0.92x | 17 | 0.85x | not a competitor winner |
| text | 10 | 0.64x | 17 | 0.85x | not a competitor winner |

**No format gap.** Video is their strongest format by both tests, all 10 of their top 10 posts, but you already clear the coverage floor on it too, at n=14: their video runs 2.37x their own median, yours runs 1.28x yours. This looked like the biggest finding in the file until the coverage check ran. It checked out as validation instead of a gap.

---

## The 5 drafted ideas

Only 2 gaps cleared the winner bar, so the five below split 3 for Rental and 2 for Studio, weighted toward the stronger gap rather than split evenly by default. **These drafts are unproven ideas filling a proven gap; nothing here predicts performance.**

**1. Fills: Rental, opportunity rank 1**

> What is the first thing you would fix in your rental if your landlord could not say no?

**Modeled on your own:** Question Open, your top rankable hook archetype, 11 posts, median 610. **Evidence this fills:** their rental closet system post, 629 engagements, 1.34x their own median.

**2. Fills: Rental, opportunity rank 1**

> 3 systems that hold a full pantry when you are not allowed to install a single shelf.

**Modeled on your own:** Number Promise, your second-ranked archetype, 7 posts, median 560. **Evidence this fills:** the same rental cluster, 3 of their 7 rental posts sit in their top quartile.

**3. Fills: Rental, opportunity rank 1**

> If you could never drill another hole in this apartment, what would you finally get organized?

**Modeled on your own:** Question Open, a second angle on the same gap. **Evidence this fills:** their rental vertical-garden post, 576 engagements.

**4. Fills: Studio, opportunity rank 2**

> If your whole home was one room, what is the first thing you would get rid of?

**Modeled on your own:** Question Open. **Evidence this fills:** their studio-for-two-and-a-dog post, 678 engagements, the single highest-engagement post in either winning cluster.

**5. Fills: Studio, opportunity rank 2**

> 2 zones I would build first in one room, and neither one needs a wall.

**Modeled on your own:** Number Promise. **Evidence this fills:** their studio-layout-walkthrough post, 565 engagements.

---

## What this analysis is standing on

Your file: 60 posts, 2026-03-21 to 2026-07-28, 130 days. Their file: 40 posts, 2026-03-05 to 2026-06-30, 118 days. 60 plus 40 is 100 posts combined, which is the N in the pointer line below. Topic clusters formed independently on each file using the identical method in `topic-inventory-method.md`, minimum 5 posts per cluster, no bigram cleared the floor on either file this run. Competitor winners require over-representation in their own top quartile against their own corpus share, not just volume; Dollars is Jordan's most-used topic and did not qualify. Rental carries one concentration flag (its median moves 20.2 percent with its top post removed). Studio carries one concentration flag (mean runs 1.55x median). Both still qualify as findings; a bucket needs two or more flags before it is dropped. The video format gap-checked as covered, not absent, once your own file was searched.

Not in either export, so not in this analysis: sponsored or paid-partnership flags on either side, per-emoji reactions, reach or impressions, comment text, follower history.

Neither file's history is complete. PostSnag captures what was scrolled on each account, so this compares two samples, not two full histories.

Analysis based on 100 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=competitor-content-gap-finder

---

# APPENDIX: what changes when your side is a free-tier export

Run with `_shared/synthetic-data/profile-maya-torres-free-slice.csv` (the same 30-post free-tier slice used across the catalog) as "your file," against the same full Jordan competitor file.

```
your file (free slice)   30 posts, 2026-05-30 to 2026-07-28, 60 days, median 530.0
lite mode                ON (30 < 40)
their file               unchanged, full mode, 40 posts, 118 days
```

**Your own cluster count drops from 16 to 2** (`Closet`, `Organizing`, both at exactly `df = 5`). That does not change anything about the gap list below, because gaps are measured by whether you are ABSENT or UNDERWEIGHTED in the COMPETITOR's winning buckets, and that check is a keyword search against your captions, not a requirement that your own clusters have formed.

**Coverage check, free slice:**

| Winning bucket | Keyword | Matches in your free slice | Status |
|---|---|---|---|
| Rental | `rental` | 0 | ABSENT |
| Studio | `studio` | 0 | ABSENT |

**Both gaps survive unchanged on the free slice.** The gap list itself does not shrink here, because Maya's absence from rental and studio content is total in the full file, not a matter of the free slice missing the handful of posts that would have counted; there are no such posts anywhere in her 60. What does change, and what the banner says: on a thinner "your file," an ABSENT reading only proves absence across a smaller, more recent window, so the honest caveat is narrower ("zero in your last 30 posts") rather than wrong.

**The banner this run would open with:**

> **Lite mode, your file.** 30 posts across 60 days. Below 40 posts or 60 days, an ABSENT reading describes your most recent posts, not your full account; a deeper capture would confirm whether the gap is real or just recent.

**What this means in practice:** a free-tier user still gets a working gap list, because the coverage check does not need your own clusters to have formed. What they do not get is the reassurance that a thin gap list on the competitor's side is really thin and not just under-captured; that reassurance needs both sides deeper, which is exactly why this skill needs two captures at minimum by definition.

---

**Version 1.0 | 2026-08-04**
