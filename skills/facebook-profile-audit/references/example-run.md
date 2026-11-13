# example-run.md

> **SYNTHETIC.** Maya Torres is a fictional creator. Every post, number, and date below is invented. Source files: `../../_shared/synthetic-data/profile-maya-torres.csv` (60 posts, full audit) and `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv` (30 posts, the free-tier appendix). Nothing here describes a real person or a real Facebook account.

This is the rubric in `rubric.md` executed start to finish, with every number computed from the source files rather than estimated, using a real CSV parser and real Python arithmetic. Anyone can re-run the parse and check. If a number here disagrees with a recomputation from the CSVs, this file is wrong and gets fixed.

Version 1.0 | 2026-08-04

---

# PART 1: THE WORK

Everything in Part 1 is the analyst's working, shown so the method is auditable. Part 2 is what the user actually receives.

---

## Step 1: Parse and validate

```
rows parsed                60
date range                 2026-03-21 to 2026-07-28
span                       130 days
empty captions             0
lite mode                  OFF (60 >= 40 posts, 130 >= 60 days)
corpus median engagement   458.5
corpus mean engagement     639.7
top quartile               k = floor(60/4) = 15, cut value 700, no tie at the boundary
```

Sorted by parsed `Posted` before anything sequential, per `references/csv-parse.md` section 4 (condensed; full version in the complete bundle), since the file itself is newest-first.

---

## Step 2: Format distribution

| Type | n | median | mean | median after top removed | change | top post's share | mean / median | flags | rankable |
|---|---|---|---|---|---|---|---|---|---|
| photo | 17 | 388 | 493.4 | 388.0 | 0.0% | 11.7% | 1.27 | none | yes |
| text | 17 | 388 | 471.2 | 357.5 | -7.9% | 15.1% | 1.21 | none | yes |
| video | 14 | 585 | 1106.4 | 566 | -3.2% | 26.6% | **1.89** | **mean/median** | yes |
| album | 8 | 393 | 407.6 | 366 | -6.9% | 17.2% | 1.04 | none | yes |
| link | 4 | 795 | 809 | 402 | not checked | not checked | not checked | not checked | **no, n<5** |

Thresholds from `references/foundations.md` section 4: flag if the median moves more than 20 percent after removing the top post, or the top post is more than 40 percent of the bucket's total, or mean over median is 1.5 or higher.

**Reading it.** Video is the only rankable format that flags, and it flags on one test: mean over median at 1.89. Its top post's share (26.6 percent) and its median-shift (-3.2 percent) both clear. That is a partial carry, not a full one: video's median of 585 is trustworthy, its mean of 1106.4 is not, and the output says exactly that rather than either hiding the flag or throwing the whole format out. Link is not rankable at n=4, and its check columns are marked **not checked**, not `none`, because the concentration check never ran on a bucket this skill will not turn into a ranked claim. Its median of 795 is still the highest of any format in the file, which is why it becomes a "too small to rank, worth testing" finding rather than being silently dropped.

**Composition, top quartile (k=15, cut value 700) against corpus share:**

| Type | share of corpus | share of top 15 |
|---|---|---|
| photo | 28.3% (17 of 60) | 26.7% (4 of 15) |
| text | 28.3% (17 of 60) | 26.7% (4 of 15) |
| video | 23.3% (14 of 60) | **33.3% (5 of 15)** |
| album | 13.3% (8 of 60) | **0.0% (0 of 15)** |
| link | 6.7% (4 of 60) | 13.3% (2 of 15) |

Video over-indexes in the top quartile relative to its volume. Album is the inverse: real volume, zero presence at the top.

**Top-10 versus bottom-10 (N=60 >= 25, both sets valid):**

| Set | Composition |
|---|---|
| Top 10 | video 4, photo 3, link 2, text 1 |
| Bottom 10 | photo 4, text 3, album 1, link 1, video 1 |

Video is 4 of the top 10 on 14 total posts. Album shows up once in the bottom 10 on only 8 total posts, less than its 13.3 percent corpus share would predict, so album's failure is "absent from the top" rather than "concentrated at the bottom." Both are real findings and they are different findings.

---

## Step 3: Topic clustering

**Extraction, run against all 60 captions with the trigger-word procedure in `rubric.md` section 2.1:**

```
distinct candidate heads found          252
discarded as non-topics (verbs, time
  words, generic pronouns)               20   (day, days, week, month, year, night,
                                                monday, tuesday, wednesday, thursday,
                                                friday, saturday, sunday, work, thing,
                                                problem, decision, instead, home, for)
kept after discard                      232
merged into a named topic cluster        15 heads -> 12 named topics
remaining long tail (single or thin,
  not named)                            217
```

**The 217-head long tail is expected, not a failure of the method.** Sixty posts of varied, specific prose (a coat closet, a sled, a wedding gift, a spice rack) produces hundreds of one-off nouns. Naming a topic requires the same object to recur; most nouns in free-form writing do not.

**The named topic clusters, ranked:**

| Topic | n | median | mean | median after top removed | change | top post's share | mean / median | flags | rankable |
|---|---|---|---|---|---|---|---|---|---|
| Closets | 10 | 530.0 | 644.6 | 520 | -1.9% | 29.5% | 1.22 | none | yes |
| Labels & Systems | 7 | 402 | 915.4 | 400 | -0.5% | **53.1%** | **2.28** | **top-share, mean/median** | yes |
| Bins & Containers | 5 | 470 | 531.8 | 381 | -19.0% | **45.4%** | 1.13 | **top-share** | yes |
| Kitchen & Counters | 5 | 462 | 487.6 | 425 | -8.0% | 29.2% | 1.06 | none | yes |
| Shelves | 4 | 429.0 | 446.5 | not checked | not checked | not checked | not checked | not checked | **no, n<5** |
| Drawers | 4 | 412.0 | 491 | not checked | not checked | not checked | not checked | not checked | **no, n<5** |
| Garages | 4 | 460.5 | 666.8 | not checked | not checked | not checked | not checked | not checked | **no, n<5** |
| Paper Piles | 3 | 388 | 456.3 | not checked | not checked | not checked | not checked | not checked | **no, n<5** |
| Pantries | 3 | 712 | 1798.7 | not checked | not checked | not checked | not checked | not checked | **no, n<5** |
| Client Stories | 2 | 383.0 | 383 | not checked | not checked | not checked | not checked | not checked | **no, n<5** |
| Entryways | 1 | 268 | 268 | not checked | not checked | not checked | not checked | not checked | **no, n<5** |
| Kids' Spaces | 1 | 540 | 540 | not checked | not checked | not checked | not checked | not checked | **no, n<5** |

**Closets is the one to slow down on.** Its 10 posts span 208 to 1904, its lowest and highest posts in the entire file both live in this cluster. That range looks like it should flag. It does not: median-after-removing-the-top-post moves 1.9 percent, the top post is 29.5 percent of the bucket, and mean over median is 1.22, all three under threshold. A wide range and a carried median are different things, and only the concentration check tells them apart. 530 is a real center for this topic.

**Labels & Systems flags twice and its median is still below the corpus median (458.5).** Even the 402 it shows is inflated by one post; without the concentration check this would read as "a modest but real topic" instead of "a topic propped up by a single post that still does not clear the corpus median."

**Bins & Containers flags once, on top-share only.** One post at 1402 engagement (the "you do not need more storage" link post, which also appears in Section 2's Garages long-tail mention since it references a garage in its body) is 45.4 percent of the bucket's total. The median of 470 still holds under the other two tests, so it is reported with the caveat glued in, not discarded.

**Topics are additive.** The post about "the pretty closet" that closes with a drawer metaphor tags both Closets and Drawers. Percentages in this section do not sum to 100 across the corpus, unlike the format table above, and the output says so once.

---

## Step 4: Cadence

```
posts per week                 3.23
gap between posts (calendar-date subtraction, not raw timestamp subtraction)
  median                       2 days
  minimum                      0 days  (one true same-day double post)
  maximum                      3 days  (17 occurrences across the capture; first at
                                        2026-03-23 to 2026-03-26)
same-day double post            2026-07-28: text at 07:20:46 (238 engagement),
                                            photo at 18:50:53 (902 engagement)
day-of-week posting counts     Saturday 19, Thursday 17, Tuesday 12, Monday 9,
                                Wednesday 1, Friday 1, Sunday 1
```

**The calendar-date fix matters here, concretely.** A naive `timedelta.days` on the raw timestamps reports three separate 0-day gaps in this file, because two of them are posts roughly 19 to 21 hours apart that cross midnight (for example, 2026-07-25 at 16:00 to 2026-07-26 at 11:05). Only one of the three is an actual same-calendar-day double post. Reporting all three as "same-day doubling" would overstate a pattern that mostly is not there.

**The engagement figure is the sum of Reactions, Comments, and Shares, not the Reactions cell alone.** The evening photo post reads 613 in the Reactions column, but its comments (216) and shares (73) bring true engagement to 902, which sits inside the top 10 posts in the entire capture. That makes this same-day double a real recommendation candidate, not a background cadence note: per findings-pattern-library.md pattern 16, a doubled day that performed this well is worth testing on purpose.

**This is a volume description, not a performance read.** Saturday, Thursday, Tuesday, and Monday carry essentially all of her output; Wednesday, Friday, and Sunday get one post each in 130 days. This audit does not say whether those three quiet days would perform well, because that comparison needs its own sample floors and belongs to Best Time to Post Reader.

---

## Step 5: The video secondary lens

**14 of 14 video posts carry `Views`.**

```
raw engagement across the 14 videos       208 to 4,118      (19.8x spread)
engagement per view across the same 14    1.66% to 2.20%    (1.32x spread)
median engagement per view                2.07%
```

Whatever separates Maya's best video from her worst happened before the view, not after it: her 4,118-engagement video converts at 1.92 percent, actually slightly below her 208-engagement video's 2.17 percent. PostSnag does not capture reach or impressions, so "before the view" is as far as this goes.

**Duration bands:**

| Band | n | median | mean | median after top removed | change | top post's share | mean / median | flags | rankable |
|---|---|---|---|---|---|---|---|---|---|---|
| Short (<=40s) | 4 | 894.0 | 1053.5 | not checked | not checked | not checked | not checked | not checked | **no, n<5** |
| Medium (41-70s) | 5 | 688 | 1824.8 | 604 | -12.2% | **45.1%** | **2.65** | **top-share, mean/median** | yes, but **not shipped as a recommendation** |
| Long (71s+) | 5 | 455 | 430.2 | 402 | -11.7% | 26.3% | 0.95 | none | yes |

**Medium clears the 5-post floor and still does not become advice.** Two of the three concentration tests flag, which per `references/foundations.md` section 4 means this bucket does not turn into a recommendation, it turns into "specific posts worth studying." What is actually driving it: the medium band contains **both** of Maya's two highest-engagement posts in the entire 60-post file, the 4,118-engagement pantry story (47 seconds) and the 3,402-engagement four-rules post (64 seconds). That is a real, worth-testing coincidence, not a validated "medium videos win" claim, and the write-up says exactly that instead of shipping a clean-looking table that is actually carried by two posts.

**Long is the one clean, ranked video-length signal in the file, and it is the lowest of the three.** Zero flags, median 455, below the corpus median of 458.5.

**Short is unrankable at n=4** with the highest median of the three bands (894), the same "too small to rank, worth testing" shape as Link in the format table.

---

## Step 6: Trajectory

**Preconditions checked: span 130 days (>= 90), lite mode OFF, N=60 (>= 40). All three clear. This section runs.**

```
earlier half:  30 posts, 2026-03-21 to 2026-05-28, median 402, mean 567.2
later half:    30 posts, 2026-05-30 to 2026-07-28, median 530, mean 712.2
trajectory_ratio = 530 / 402 = 1.32  ->  RISING (>= 1.15 threshold)

concentration check, earlier half:
  median after top removed 402 (0.0% change), top-share 24.2%, mean/median 1.41  -> no flags
concentration check, later half:
  median after top removed 520 (-1.9% change), top-share 15.9%, mean/median 1.34 -> no flags
```

Both halves clear clean, so the rising read is not an artifact of one post pulling a half's median around.

**PostSnag does not capture follower history.** The Markdown export carries a single point-in-time follower count and nothing else. This trajectory read cannot separate "the content got better" from "the audience got bigger" over these 130 days, and it does not claim to. A rising median is consistent with better content, a bigger audience, or both, and this file cannot tell you which.

**Audit seam worth naming.** The later half above is, by construction, the same 30 rows as the shared free-tier fixture `profile-maya-torres-free-slice.csv` (defined in `_shared/synthetic-data/README.md` as the most recent 30 posts of this same file). Its median of 530 matches this later-half median exactly, which is a live cross-check: the free-tier appendix in this file (below) and this trajectory section should never disagree on that number.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable. Part 1 was the working.

---

# Profile audit: Maya Torres

60 posts, 2026-03-21 to 2026-07-28, 130 days. Format mix: photo 17 (28.3%), text 17 (28.3%), video 14 (23.3%), album 8 (13.3%), link 4 (6.7%). Corpus median engagement: 458.5. Engagement here means reactions plus comments plus shares.

---

## What works

**1. Closets is your most-used topic and it holds up clean.**

Closets, 10 posts, median 530 against your corpus median of 458.5. This cluster spans your lowest post in the file (208) and your highest (1,904), and the concentration check still clears on all three counts: nothing here is a fluke carrying the number. Keep writing closet content at the current rate.

**2. Video earns a real premium, with one number to trust over another.**

Video, 14 posts, median 585 against your corpus median of 458.5, and 33.3 percent of your top 15 posts on 23.3 percent of your volume. The mean (1,106.4) overstates this: mean over median is 1.89, so two videos are doing outsized work. Use the median, 585, as the honest number.

**3. Link posts, untested but the strongest number in the file.**

Link, only 4 posts, median 795, the highest median of any format you use. Four posts is not a measurement, so this is not ranked and not proven. It is the clearest "write three more and find out" in this audit.

---

## What does not work

**1. Album is real volume with nothing at the top.**

Album, 8 posts (13.3 percent of your output), median 393, and zero of your top 15 posts. You are spending real slots on a format that has not once broken into your best work.

**2. Long videos are your one clean, ranked video-length signal, and they are your worst.**

Long videos (71 seconds and over), 5 posts, median 455, no concentration flags. This is the cleanest bucket in the whole video section, and it sits right at your corpus median, below both other duration bands.

**3. Kitchen & Counters is tested and flat.**

Kitchen & Counters, 5 posts, median 462 against a corpus median of 458.5, no flags. This is not a failure, it is a null result: you have enough posts to measure it and the measurement says "no different from average." Worth knowing, not worth chasing.

---

## Format distribution

| Type | Posts | Median | Mean | Share of corpus | Share of top 15 | Median after top removed | Change | Top post's share | Mean / median | Rankable |
|---|---|---|---|---|---|---|---|---|---|---|
| photo | 17 | 388 | 493.4 | 28.3% | 4 of 15 | 388.0 | 0.0% | 11.7% | 1.27 | yes |
| text | 17 | 388 | 471.2 | 28.3% | 4 of 15 | 357.5 | -7.9% | 15.1% | 1.21 | yes |
| video | 14 | 585 | 1106.4 | 23.3% | 5 of 15 | 566 | -3.2% | 26.6% | 1.89 | yes |
| album | 8 | 393 | 407.6 | 13.3% | 0 of 15 | 366 | -6.9% | 17.2% | 1.04 | yes |
| link | 4 | 795 | 809 | 6.7% | 2 of 15 | not checked | not checked | not checked | not checked | **no, n<5** |

Top 10 versus bottom 10 by format: top 10 is video 4, photo 3, link 2, text 1. Bottom 10 is photo 4, text 3, album 1, link 1, video 1.

---

## Topic clusters

Topics are extracted mechanically from `Content` and are additive: a post can belong to more than one cluster, unlike format, which is exactly one value per post. Full extraction method: `references/rubric.md` section 2.

| Topic | Posts | Median | Mean | Median after top removed | Change | Top post's share | Mean / median | Rankable |
|---|---|---|---|---|---|---|---|---|
| Closets | 10 | 530.0 | 644.6 | 520 | -1.9% | 29.5% | 1.22 | yes |
| Labels & Systems | 7 | 402 | 915.4 | 400 | -0.5% | 53.1% | 2.28 | yes |
| Bins & Containers | 5 | 470 | 531.8 | 381 | -19.0% | 45.4% | 1.13 | yes |
| Kitchen & Counters | 5 | 462 | 487.6 | 425 | -8.0% | 29.2% | 1.06 | yes |
| Shelves | 4 | 429.0 | 446.5 | not checked | not checked | not checked | not checked | **no, n<5** |
| Drawers | 4 | 412.0 | 491 | not checked | not checked | not checked | not checked | **no, n<5** |
| Garages | 4 | 460.5 | 666.8 | not checked | not checked | not checked | not checked | **no, n<5** |
| Paper Piles | 3 | 388 | 456.3 | not checked | not checked | not checked | not checked | **no, n<5** |
| Pantries | 3 | 712 | 1798.7 | not checked | not checked | not checked | not checked | **no, n<5** |
| Client Stories | 2 | 383.0 | 383 | not checked | not checked | not checked | not checked | **no, n<5** |
| Entryways | 1 | 268 | 268 | not checked | not checked | not checked | not checked | **no, n<5** |
| Kids' Spaces | 1 | 540 | 540 | not checked | not checked | not checked | not checked | **no, n<5** |

20 candidate topic heads were discarded as non-topics (verbs, time words, generic pronouns) before this table was built. 217 additional heads survived the discard step but were single or near-single mentions that never formed a repeatable topic, so they are not reported individually.

---

## Cadence

60 posts across 130 days, 3.23 posts per week. Gap between posts (calendar-date based): median 2 days, minimum 0 days, maximum 3 days (17 occurrences, the first between 2026-03-23 and 2026-03-26). Same-day doubling: 2026-07-28 carried 2 posts, a text at 238 engagement and a photo at 902 engagement (613 Reactions plus 216 comments plus 73 shares), the photo landing inside your top 10 posts, which makes this pairing worth testing on purpose.

Posting days: Saturday 19, Thursday 17, Tuesday 12, Monday 9, Wednesday 1, Friday 1, Sunday 1. Wednesday, Friday, and Sunday are essentially untested, not proven weak: this audit counts posts, it does not rank days by performance. That read is Best Time to Post Reader's job.

---

## Video: views and duration

14 of your 14 video posts carry `Views`. Raw engagement across them spans 208 to 4,118 (19.8x). Engagement per view spans 1.66% to 2.20% (1.32x). Whatever separates your best video from your worst happened before the view, not after it: your highest-engagement video converts at 1.92 percent, slightly below your lowest-engagement video's 2.17 percent.

| Duration band | Posts | Median | Mean / median | Top post's share | Rankable |
|---|---|---|---|---|---|
| Short (<=40s) | 4 | 894.0 | not checked | not checked | **no, n<5** |
| Medium (41-70s) | 5 | 688 | 2.65 | 45.1% | yes, but not shipped as a recommendation |
| Long (71s+) | 5 | 455 | 0.95 | 26.3% | yes |

Medium flags twice (mean/median and top-share) and does not become a recommendation. What is actually there: your two highest-engagement posts in this entire capture, the 4,118-engagement pantry story and the 3,402-engagement four-rules post, are both medium-length videos (47 and 64 seconds). That is worth testing on purpose, not worth claiming as proven. Long is your one clean, ranked video-length signal, and it is your lowest.

---

## 5 patterns worth stealing

**1. Untested Standout: link posts** (pattern 4, Untested Standout, `findings-pattern-library.md`)

Link, 4 posts, median 795, the highest median of any format in the file, unrankable at n<5. Write 3 more link-style posts this month and see whether the number holds once it clears the floor.

**2. Single Best Post: the pantry story** (pattern 29, Single Best Post, `findings-pattern-library.md`)

Your all-time top post (4,118 engagement, "A client cried in her own pantry on Monday, and it was not about food.") is a first-person client story, medium-length video (47 seconds). Worth a frame-by-frame study of the opening, the pacing, and the closing line on its own, independent of any bucket ranking.

**3. Two-post coincidence: the medium video band** (pattern 22, Two Posts, Not A Trend, `findings-pattern-library.md`)

Your two highest-engagement posts of the entire capture both happen to be medium-length videos (41 to 70 seconds). The bucket itself is not a validated recommendation, but the coincidence is: script and test 3 more videos in that length band, deliberately, and see if a third post lands anywhere near the first two.

**4. Untested Standout: short videos** (pattern 4, Untested Standout, `findings-pattern-library.md`)

Short videos (40 seconds or under), 4 posts, median 894, the highest median of any duration band, unrankable at n<5. One short video away from being measurable.

**5. Thin topic worth testing: Kids' Spaces** (pattern 10, Thin Topic Cluster, `findings-pattern-library.md`)

Kids' Spaces, 1 post, 540 engagement, above your corpus median of 458.5 on a single data point. Write 3 to 4 more and see whether it clears the 5-post floor as a real topic.

---

## Your 30-day list

1. Write 3 more link-style posts. (Traces to: What works, finding 3, and steal-worthy pattern 1.)
2. Script and post one more medium-length video (41 to 70 seconds), structured like the pantry story and the four-rules post: a specific person or number up top, one clean beat, under 70 seconds. (Traces to: steal-worthy pattern 3.)
3. Cut album's share of the rotation for 30 days and reassign that slot to photo or video. (Traces to: What does not work, finding 1.)
4. Cap new long-form videos at 70 seconds. (Traces to: What does not work, finding 2.)
5. Write 3 to 4 more Kids' Spaces posts. (Traces to: steal-worthy pattern 5.)
6. Keep the Closets rate where it is. (Traces to: What works, finding 1.)
7. Test one post on a day you rarely use, Wednesday, Friday, or Sunday, and see whether the audience is there. This audit cannot tell you whether those days perform, only that you have not tested them. (Traces to: Cadence.)

---

## Trajectory

Your earlier half (2026-03-21 to 2026-05-28, 30 posts) sits at a median of 402. Your later half (2026-05-30 to 2026-07-28, 30 posts) sits at 530, a ratio of 1.32, which this audit calls **rising**. Concentration check on both halves clears clean: neither is being carried by a single post.

**PostSnag does not capture follower history.** The Markdown export carries a single point-in-time follower count and nothing else. This trajectory read cannot separate "the content got better" from "the audience got bigger" in the same window, and it does not claim to.

---

## What this audit is standing on

Analyzed 60 posts captured 2026-03-21 to 2026-07-28, 130 days. Format and topic buckets under 5 posts are listed but not ranked. Video's mean/median flags (1.89); the medium duration band flags on two of three checks and was reported as two specific posts rather than a ranked recommendation; Labels & Systems flags on two of three checks; Bins & Containers flags on one.

Not in your export, so not in this audit: sponsored or paid-partnership flags, so a boosted post looks identical to an organic one here. Per-emoji reactions. Reach or impressions. Comment text. Follower history over time.

PostSnag captures what you scrolled, so this is a sample of the account, not its full history.

Analysis based on 60 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-profile-audit

---

# APPENDIX: the same audit on a free-tier export

Run against `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv`, the most recent 30 rows of the same file. This is what a free-tier user gets, included so nobody has to guess how honest the degradation actually is.

```
posts                30
date range            2026-05-30 to 2026-07-28
span                  60 days
lite mode             ON (30 posts < 40)
corpus median         530
corpus mean           712.2
top quartile          k = 7, cut value 902
trajectory section    DOES NOT RUN (span 60 < 90, and lite mode is on regardless)
```

**Format distribution:**

| Type | n | median | share of corpus | share of top 7 | rankable |
|---|---|---|---|---|---|
| photo | 8 | 597.5 | 26.7% | 2 of 7 | yes |
| text | 8 | 396.5 | 26.7% | 1 of 7 | yes |
| video | 7 | 604 | 23.3% | 2 of 7 | yes |
| album | 5 | 355 | 16.7% | 0 of 7 | yes, exactly at the floor |
| link | 2 | 1295 | 6.7% | 2 of 7 | **no, n<5** |

**Topic clusters: only 1 of 10 clears the floor.**

| Topic | n | median | rankable |
|---|---|---|---|
| Closets | 5 | 540 | yes, exactly at the floor |
| Garages | 3 | 466 | no |
| Labels & Systems | 3 | 655 | no |
| Drawers | 3 | 512 | no |
| Paper Piles | 2 | 377.0 | no |
| Kitchen & Counters | 2 | 388.0 | no |
| Bins & Containers | 2 | 873.0 | no |
| Client Stories | 1 | 520 | no |
| Kids' Spaces | 1 | 540 | no |
| Pantries | 1 | 566 | no |

**Cadence:** 30 posts across 60 days, 3.5 posts per week. Gap between posts (calendar-date based): median 2 days, minimum 0 (the same 2026-07-28 same-day double as the full file, since it falls inside this window), maximum 3 days. Posting days: Saturday 9, Tuesday 8, Thursday 7, Monday 3, Wednesday 1, Friday 1, Sunday 1.

**Video:** 7 of 7 videos carry `Views`. Raw engagement spans 208 to 3,402 (16.4x). Engagement per view spans 2.01% to 2.17% (1.08x). Duration bands: short n=2, medium n=2, long n=3, all three below the 5-post floor, so no duration finding ships on a free-tier capture.

**What survives:** the format table (all rankable except link), the Closets topic finding (thinner: n=5 instead of n=10, median 540 instead of 530, exactly at the floor instead of comfortably above it), and the video views-versus-rate finding. What does not survive: 9 of 10 topic clusters, all duration-band findings, and the entire trajectory section.

**The banner this run would open with:**

> **Lite mode.** This capture has 30 posts across 60 days. Below 40 posts or 60 days this analysis runs shallow on purpose. Degraded here: only 1 of 10 topic clusters clears the ranking floor, video duration bands are all below the floor, and there is no trajectory section. To unlock the full topic table and the video duration read, capture about 40 posts across 60 or more days. To unlock trajectory specifically, capture at least 90 days of span.

That banner gives the sample size, date span and sections that more data would support.
