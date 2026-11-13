# example-run.md

> **SYNTHETIC.** Maya Torres is a fictional creator. Every post, number, and date below is invented. Source files: `../../_shared/synthetic-data/profile-maya-torres.csv` (full run) and `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv` (shallow run). Nothing here describes a real person or a real Facebook account. "Today" for every age and gate calculation below is 2026-08-04, the date this pack was built.

This is the rubric in `rubric.md` executed start to finish, with every number computed from the source files rather than estimated. Anyone can re-run the parse and check. If a number here disagrees with a recomputation from the CSV, this file is wrong and gets fixed.

Version 1.0 | 2026-08-04

---

# PART 1: THE WORK (full run, `profile-maya-torres.csv`)

Everything in Part 1 is the analyst's working, shown so the method is auditable. Part 2 is what the user actually receives.

---

## Step 1: Parse and validate

```
rows parsed                60
date range                 2026-03-21 to 2026-07-28
span                       130 days
today (reference date)     2026-08-04
corpus median engagement   458.5    (matches facebook-hook-analyzer's own worked number on this same file, cross-checked)
era-adjustment preconditions:
  N >= 21                  60, yes
  span_days >= 90          130, yes
  lite mode                OFF (60 >= 40 posts, 130 >= 60 days)
  -> ALL THREE HOLD. Era-adjusted scoring is active for this run.
```

---

## Step 2: Era-adjusted score, every post

Full method and the edge-case rule: `rubric.md` section 1. Three posts worked in full there, including both edges of the file (index 0 and index 59) and the file's highest score (index 20). Not repeated here; the summary below is the same computation run across all 60 posts.

**Full table.** `idx` is the position after sorting ascending by `Posted` (0 to 59). `safe` is whether the post already clears the 90-day reuse-safety gate as of 2026-08-04. `class` is the evergreen classification from Step 3. `floor` is whether the era score clears the 1.5x repost-worthy floor.

| idx | Date | Type | Engagement | Era score | Age (days) | Reuse-safe | Class | Clears 1.5x floor |
|---|---|---|---|---|---|---|---|---|
| 0 | 2026-03-21 | photo | 246 | 0.75 | 136 | Y | CLEAN EVERGREEN | N |
| 1 | 2026-03-23 | text | 388 | 1.26 | 134 | Y | CLEAN EVERGREEN | N |
| 2 | 2026-03-26 | video | 312 | 0.97 | 131 | Y | CLEAN EVERGREEN | N |
| 3 | 2026-03-28 | photo | 302 | 0.92 | 129 | Y | CLEAN EVERGREEN | N |
| 4 | 2026-03-30 | text | 291 | 0.89 | 127 | Y | CLEAN EVERGREEN | N |
| 5 | 2026-04-02 | album | 488 | 1.59 | 124 | Y | CLEAN EVERGREEN | **Y** |
| 6 | 2026-04-04 | video | 688 | 2.11 | 122 | Y | CLEAN EVERGREEN | **Y** |
| 7 | 2026-04-06 | photo | 341 | 1.11 | 120 | Y | CLEAN EVERGREEN | N |
| 8 | 2026-04-09 | text | 610 | 1.89 | 117 | Y | CLEAN EVERGREEN | **Y** |
| 9 | 2026-04-11 | link | 244 | 0.60 | 115 | Y | CLEAN EVERGREEN | N |
| 10 | 2026-04-13 | photo | 268 | 0.58 | 113 | Y | CLEAN EVERGREEN | N |
| 11 | 2026-04-16 | video | 1,044 | 2.76 | 110 | Y | CLEAN EVERGREEN | **Y** |
| 12 | 2026-04-18 | text | 305 | 0.71 | 108 | Y | CLEAN EVERGREEN | N |
| 13 | 2026-04-20 | album | 462 | 1.22 | 106 | Y | CLEAN EVERGREEN | N |
| 14 | 2026-04-23 | photo | 355 | 1.00 | 103 | Y | CLEAN EVERGREEN | N |
| 15 | 2026-04-25 | text | 470 | 1.24 | 101 | Y | CLEAN EVERGREEN | N |
| 16 | 2026-04-27 | video | 402 | 0.86 | 99 | Y | CLEAN EVERGREEN | N |
| 17 | 2026-04-30 | photo | 615 | 1.50 | 96 | Y | CLEAN EVERGREEN | N, raw 1.4964 |
| 18 | 2026-05-02 | text | 152 | 0.33 | 94 | Y | CLEAN EVERGREEN | N |
| 19 | 2026-05-05 | photo | 214 | 0.48 | 91 | Y | CLEAN EVERGREEN | N |
| 20 | 2026-05-07 | video | 4,118 | 9.41 | 89 | N | CLEAN EVERGREEN | **Y** |
| 21 | 2026-05-09 | text | 702 | 1.60 | 87 | N | CLEAN EVERGREEN | **Y** |
| 22 | 2026-05-12 | album | 420 | 0.79 | 84 | N | CLEAN EVERGREEN | N |
| 23 | 2026-05-14 | photo | 980 | 2.24 | 82 | N | CLEAN EVERGREEN | **Y** |
| 24 | 2026-05-16 | link | 402 | 0.82 | 80 | N | CLEAN EVERGREEN | N |
| 25 | 2026-05-19 | video | 455 | 0.97 | 77 | N | CLEAN EVERGREEN | N |
| 26 | 2026-05-21 | text | 712 | 1.63 | 75 | N | CLEAN EVERGREEN | **Y** |
| 27 | 2026-05-23 | photo | 190 | 0.43 | 73 | N | **DATED-HOOK-ONLY** | N |
| 28 | 2026-05-26 | video | 522 | 1.22 | 70 | N | CLEAN EVERGREEN | N |
| 29 | 2026-05-28 | text | 318 | 0.65 | 68 | N | CLEAN EVERGREEN | N |
| 30 | 2026-05-30 | album | 344 | 0.70 | 66 | N | CLEAN EVERGREEN | N |
| 31 | 2026-06-02 | photo | 905 | 2.18 | 63 | N | CLEAN EVERGREEN | **Y** |
| 32 | 2026-06-04 | text | 182 | 0.37 | 61 | N | CLEAN EVERGREEN | N |
| 33 | 2026-06-06 | video | 3,402 | 6.90 | 59 | N | CLEAN EVERGREEN | **Y** |
| 34 | 2026-06-09 | photo | 655 | 1.53 | 56 | N | CLEAN EVERGREEN | **Y** |
| 35 | 2026-06-11 | text | 466 | 0.79 | 54 | N | CLEAN EVERGREEN | N |
| 36 | 2026-06-13 | album | 366 | 0.58 | 52 | N | CLEAN EVERGREEN | N |
| 37 | 2026-06-16 | video | 520 | 0.97 | 49 | N | CLEAN EVERGREEN | N |
| 38 | 2026-06-18 | text | 826 | 1.47 | 47 | N | CLEAN EVERGREEN | N |
| 39 | 2026-06-20 | photo | 388 | 0.69 | 45 | N | CLEAN EVERGREEN | N |
| 40 | 2026-06-23 | link | 1,188 | 2.41 | 42 | N | CLEAN EVERGREEN | **Y** |
| 41 | 2026-06-25 | video | 604 | 1.17 | 40 | N | CLEAN EVERGREEN | N |
| 42 | 2026-06-27 | text | 327 | 0.57 | 38 | N | CLEAN EVERGREEN | N |
| 43 | 2026-06-30 | photo | 700 | 1.22 | 35 | N | CLEAN EVERGREEN | N |
| 44 | 2026-07-02 | album | 266 | 0.47 | 33 | N | CLEAN EVERGREEN | N |
| 45 | 2026-07-04 | video | 744 | 1.41 | 31 | N | CLEAN EVERGREEN | N |
| 46 | 2026-07-07 | text | 512 | 1.09 | 28 | N | CLEAN EVERGREEN | N |
| 47 | 2026-07-09 | photo | 540 | 1.19 | 26 | N | CLEAN EVERGREEN | N |
| 48 | 2026-07-11 | video | 1,904 | 3.62 | 24 | N | CLEAN EVERGREEN | **Y** |
| 49 | 2026-07-13 | text | 305 | 0.58 | 22 | N | CLEAN EVERGREEN | N |
| 50 | 2026-07-16 | album | 355 | 0.64 | 19 | N | **DATED-HOOK-ONLY** | N |
| 51 | 2026-07-18 | photo | 398 | 0.72 | 17 | N | CLEAN EVERGREEN | N |
| 52 | 2026-07-20 | link | 1,402 | 2.99 | 15 | N | CLEAN EVERGREEN | **Y** |
| 53 | 2026-07-22 | video | 566 | 1.44 | 13 | N | CLEAN EVERGREEN | N |
| 54 | 2026-07-24 | photo | 388 | 0.81 | 11 | N | CLEAN EVERGREEN | N |
| 55 | 2026-07-25 | text | 1,206 | 3.07 | 10 | N | CLEAN EVERGREEN | **Y** |
| 56 | 2026-07-26 | album | 560 | 1.42 | 9 | N | CLEAN EVERGREEN | N |
| 57 | 2026-07-27 | video | 208 | 0.43 | 8 | N | CLEAN EVERGREEN | N |
| 58 | 2026-07-28 | text | 238 | 0.50 | 7 | N | CLEAN EVERGREEN | N |
| 59 | 2026-07-28 | photo | 902 | 2.30 | 7 | N | CLEAN EVERGREEN | **Y** |

**Idx 17's raw-value check, worked, because it is the only row in this file that this comparator changes.** `era_score = 615 / 411.0 = 1.496350...`, which rounds to the displayed 1.50. Per R1, every comparator in this catalog applies to the raw value, never the rounded display value: `1.496350... >= 1.5` is FALSE, so idx 17 does not clear the floor. Displaying "1.50" and then comparing "1.50 >= 1.5" would have let a rounding artifact promote a post that, unrounded, misses the floor by 0.0037.

---

## Step 3: The evergreen filter, applied

**58 of 60 posts are CLEAN EVERGREEN. 2 are DATED-HOOK-ONLY. 0 are SEASONAL EVERGREEN. 0 are DATED-BODY (excluded).**

**The two DATED-HOOK-ONLY calls, with the section 2.1 test applied to each:**

- **idx 50 (2026-07-16):** `2 shelves, 6 categories, zero rearranging since March.` The hook itself is the currency claim: "since March" is only true because of how much time has passed since the post's own publish date. Reposted later, the arithmetic is wrong or misleading. The body ("Shelf one: daily, weekly. Shelf two: monthly, seasonal, backstock, outbound. The categories are frequency, not type.") carries no dated language, so this is DATED-HOOK-ONLY, not DATED-BODY.
- **idx 27 (2026-05-23):** `If you work from the kitchen table, read this before Sunday.` "Before Sunday" is a deadline aimed at the reader's calendar, tied to the week the post went out. The body ("Sunday dinner should not require relocating your job") uses "Sunday" as a recurring weekly concept, not a specific deadline, and passes the test clean, so this is also DATED-HOOK-ONLY.

**18 posts in the file contain a time-flavored word at all** (a weekday, a month, a year, "this week," "version," "right now," "since"), printed here in full so the count is reproducible against the CSV rather than taken on faith:

| idx | Date | Time-flavored word(s) matched |
|---|---|---|
| 0 | 2026-03-21 | Saturday |
| 6 | 2026-04-04 | Tuesday, May |
| 7 | 2026-04-06 | Tuesday (x3) |
| 12 | 2026-04-18 | Thursday |
| 17 | 2026-04-30 | this week |
| 20 | 2026-05-07 | Monday, 2019 |
| 21 | 2026-05-09 | Wednesday, Saturday |
| 27 | 2026-05-23 | Sunday |
| 29 | 2026-05-28 | this week |
| 38 | 2026-06-18 | Friday |
| 40 | 2026-06-23 | Tuesday |
| 43 | 2026-06-30 | right now |
| 48 | 2026-07-11 | version |
| 50 | 2026-07-16 | March, since |
| 56 | 2026-07-26 | Saturday, version |
| 57 | 2026-07-27 | 2011 |
| 58 | 2026-07-28 | Right now |
| 59 | 2026-07-28 | 2019, since |

**idx 14 ("New parents, your entryway needs a bench and nothing else.") is deliberately not on this list.** "New" is a match for a time-flavored word on its own, but `rubric.md` section 2.2's own marker list only makes "new" count for anything when it is paired with a bare calendar year ("this year's new X"), Category B. Idx 14's "New" has no year attached to it, so the rubric's own marker list does not treat it as time-flavored language at all, and this count follows that list rather than a looser reading. Include idx 14 and the count is 19, not 18; the marker list, not a vibe check, is what decides it, and it says 18.

16 of these 18 pass the section 2.1 test as narrative anchors or reader-facing generic labels, not currency claims. Two worked examples showing the test firing in both directions on similar-looking language, side by side:

| Post | Time word | Test result | Why |
|---|---|---|---|
| idx 6, `I opened a client's coat closet last Tuesday and a sled fell on me... In May.` | "last Tuesday," "In May" | NOT a marker | Describes when a scene happened. Reposted in November, this sentence is exactly as true as it was in April. |
| idx 50, `zero rearranging since March.` | "since March" | **A marker** | True only because of elapsed time since publish. Reposted unchanged, the reader has no way to know if it still holds. |

**No post in this file is SEASONAL EVERGREEN.** Zero of the 60 posts have a season or holiday as their subject; the closest near-miss is idx 16's "falls apart," which is a false positive on the substring "fall," not a seasonal reference. The class is defined in `rubric.md` section 2.2 with a hypothetical example, because this dataset does not happen to exercise it. That is stated here plainly rather than manufacturing a seasonal post that is not in the file.

---

## Step 4: The reuse-safety age gate, applied

**20 of the 58 evergreen posts are already 90 days old or more.** The other 38 evergreen posts, plus both DATED-HOOK-ONLY posts, are not old enough yet, regardless of score.

**The flagship boundary case.** The single highest-scoring post in the entire file, idx 20, `A client cried in her own pantry on Monday, and it was not about food.` (era score 9.41, more than twice the next-highest score in the file), is 89 days old against the 2026-08-04 reference date. It needs **exactly one more day**. It clears the gate on **2026-08-05**. This is not on the shortlist below for that single reason, and it is the clearest proof in this whole run that the gate is a real constraint, not a decorative one: the best post in the file, by a wide margin, is withheld.

---

## Step 5: Building the shortlist

**The funnel, stated as counts at each gate, so the bottleneck is visible:**

```
60 posts in this export
58 clear the evergreen filter (not dated)
20 of those are reuse-safe (90 days old or more)
 4 of those 20 also clear the 1.5x score floor, checked on the raw value (R1)
-> 4 posts make the shortlist
 1 more (idx 17) is reuse-safe and rounds to 1.50 on display, but its raw
   score, 1.4964, misses the floor by 0.0037 -> named as a near-miss below,
   not shortlisted and not watch-listed (it is already reuse-safe, so it is
   not "not yet reuse-safe" either; it simply does not qualify for anything)
12 more clear the evergreen filter and the 1.5x score floor, but are not
   reuse-safe yet -> the watch list, step 8
```

**The 4 shortlist posts, ranked by era score, descending:**

| Rank | idx | Date | Type | Engagement | Era score (10-post neighborhood median) | Age |
|---|---|---|---|---|---|---|
| 1 | 11 | 2026-04-16 | video | 1,044 | 2.76 (median 378.5) | 110 days |
| 2 | 6 | 2026-04-04 | video | 688 | 2.11 (median 326.5) | 122 days |
| 3 | 8 | 2026-04-09 | text | 610 | 1.89 (median 323.0) | 117 days |
| 4 | 5 | 2026-04-02 | album | 488 | 1.59 (median 307.0) | 124 days |

No ties. No exclusions needed at this step.

**Near-miss, named rather than dropped: idx 17 (2026-04-30, photo, 615 engagements, 96 days old).** `615 / 411.0 = 1.49635`, which rounds to a displayed 1.50 but is below the 1.5 raw-value floor per R1. It clears the evergreen filter (CLEAN EVERGREEN) and the age gate (96 >= 90) cleanly; the score floor is the only gate it misses, and it misses by 0.0037. It is not on the watch list either, because the watch list is for posts that are not yet reuse-safe, and this one already is. It simply does not qualify for either list this run. Recapture will not change this one, only genuine engagement would.

---

## Step 6: The repost-as-is versus remake decision rule, applied to each of the 4

**Rankable type medians for the whole corpus, needed for trigger B:** video 585 (n=14), album 393 (n=8), photo 388 (n=17), text 388 (n=17). `link` (n=4) is below the 5-post floor and excluded from this comparison. Video is the best rankable type.

**idx 11**, `Labels do not organize anything. Limits do.` Type video, already the best rankable type. No format gap. Its own Type bucket has n=14, well above the concentration trigger's n<5 requirement, so trigger C does not apply. No dated language. **No trigger fires. REPOST AS-IS.**

**idx 6**, `I opened a client's coat closet last Tuesday and a sled fell on me.` Same reasoning as idx 11: video, best rankable type, n=14 in its type bucket. **No trigger fires. REPOST AS-IS.**

**idx 8**, `Do you actually use the top shelf, or do you just store guilt there?` Type text, corpus median 388. `type_gap = 585 / 388 = 1.51`, at or above the 1.3x threshold. **Trigger B fires: format-upgrade.**

**idx 5**, `5 things I removed from my kitchen counter that I have not missed once.` Type album, corpus median 393. `type_gap = 585 / 393 = 1.49`, at or above 1.3. **Trigger B fires: format-upgrade.**

**Result: 2 REPOST AS-IS, 2 REMAKE, both remakes triggered by format-upgrade alone.**

---

## Step 6b: the reuse-safety checklist, walked on idx 11 (the top shortlist entry)

`references/reuse-safety-checklist.md` is the by-hand companion to this rubric: a 24-item, 6-category sheet for sanity-checking one specific post. Walked here, category by category, on idx 11 (`Labels do not organize anything. Limits do.`, video, 2026-04-16, 1,044 engagements, era score 2.76, 110 days old, REPOST AS-IS), so the checklist and the automated rubric are shown agreeing on the same post rather than living as two disconnected files.

**A. Dated-language checks (items 1-5).** Already resolved by Step 3's evergreen-filter classification: idx 11 is CLEAN EVERGREEN, meaning no Category A/B/C marker anywhere in the hook or body per the section 2.1 test. Items 1-4: No. Item 5, the control question: no time word appears in the post at all, which passes either way.

**B. Factual-claim aging (items 6-10).** No price, cumulative count, named product, policy, or competitor comparison appears in the hook, and the body is not reproduced in this file to check further. Items 6-10: **not checked** against the body, per the checklist's own rule that anything outside the visible export text is "not checked" until the user confirms it, never assumed safe.

**C. Seasonal windows (items 11-13).** The post's subject, labels versus limits as an organizing-systems argument, is not a season or a holiday. Item 11: No. Items 12 and 13 do not apply.

**D. Audience-shift checks (items 14-17).** Nothing in the hook names a life stage, a business-capacity claim, a platform UI step, or a follower count. Items 14-17: No, based on the hook; the body is not reproduced here to check further, so this is a hook-level pass, not a full-body clearance.

**E. Link-rot check (items 18-20).** `Type` is `video`, not `link`, and `Link_URL` is empty on this row per the format table in Step 6. Items 18-20 do not apply.

**F. Media dependency (items 21-24).** `Type` is `video`, so `Media_URLs` and `Duration_Sec` are expected to be populated, per `references/csv-parse.md` section 2. Item 21: yes, media is present, and this skill has never fetched it and never will, treating it strictly as a presence flag. Item 22: the hook and the REPOST AS-IS call do not depend on describing an unseen image; this is a spoken argument, not a "look at this" post, so it stands without the video file being re-verified here. Item 23: `Duration_Sec` is populated per the export schema; the user still needs to confirm the source video file itself still exists before reposting, which this skill cannot check from a CSV. Item 24: no stat graphic or price list is implied by the hook.

**Reading the sheet, per the checklist's own rule:** zero risk-flagging "yes" answers among the items this skill can check from the export, a passed age gate (110 days, well clear of 90), and a score at or above 1.5x (2.76x). That is exactly what the checklist calls REPOST AS-IS, the same call Step 6 already reached mechanically. The two "not checked" categories (B, and the body-dependent half of D) are not silent: they are named here as exactly what a user should personally verify before reposting, which is what the checklist exists for on top of the automated rubric.

---

## Step 7: Drafting the refreshed versions

Method: `rubric.md` section 5. Current voice profile drawn from `facebook-caption-writer`'s own 9-mechanic system, condensed here to the two mechanics that matter for a format-upgrade remake: line-break structure and sentence rhythm. Maya's existing winning video posts (idx 11, idx 6, both already in this shortlist) share one structure: hook line, blank line, then a two-line body, each line short. That structure is the model for both remakes below, because it is the pattern her OWN video posts already use, not an invented template.

**idx 8, format-upgrade to video. Trigger: B (text median 388 vs video median 585, 1.51x gap).**

Original, posted 2026-04-09:
> Do you actually use the top shelf, or do you just store guilt there?
>
> Go look. I will wait.
> Most top shelves hold three things: seasonal items, sentimental items, and evidence of a purchase you regret.

Refreshed:
> Do you actually use the top shelf, or do you just store guilt there?
>
> Go check right now, on camera, while I wait.
> Three things live up there in every home I have organized: seasonal stuff, sentimental stuff, and one purchase nobody wants to admit to.

**What changed and why:** Hook kept word for word, it is not dated and it already earned its 1.89x score. The body was trimmed to the two-line structure Maya's existing video posts use (idx 11, idx 6), because a video can show the top-shelf check happening instead of describing it in text, which is the whole point of the format-upgrade: the text version had to explain what the video version can just show.

**idx 5, format-upgrade to video. Trigger: B (album median 393 vs video median 585, 1.49x gap).**

Original, posted 2026-04-02:
> 5 things I removed from my kitchen counter that I have not missed once.
>
> The knife block, the fruit bowl, the mail tray, the second cutting board, and the paper towel stand.
> All five had a home eighteen inches away. All five were on the counter out of habit, not need.

Refreshed:
> 5 things I removed from my kitchen counter that I have not missed once.
>
> Watch what was actually still sitting there before I touched a single thing.
> Every one of them had a home eighteen inches away. They were out of habit, not need.

**What changed and why:** Hook kept word for word. The itemized list is exactly what a video shows better than a caption lists, so the refreshed caption points at the reveal instead of naming all five items, and the closing line, the actual argument of the post, is kept almost unchanged because it is the part video cannot do on its own.

**idx 11 and idx 6: no refresh drafted. They are REPOST AS-IS.** Posting the exact original text again is the recommendation.

**idx 17 is not drafted here.** It cleared the evergreen filter and the age gate but missed the raw-value 1.5x score floor by 0.0037 (Step 5), so it is a near-miss, not a shortlist member, and this skill does not draft refreshes for posts that are not on the shortlist.

---

## Step 8: The watch list

**12 posts clear the evergreen filter and the 1.5x score floor but are not yet 90 days old**, ranked by how soon each one clears the gate:

| Date | Type | Engagement | Era score | Age | Clears on |
|---|---|---|---|---|---|
| 2026-05-07 | video | 4,118 | 9.41 | 89 days | **2026-08-05** |
| 2026-05-09 | text | 702 | 1.60 | 87 days | 2026-08-07 |
| 2026-05-14 | photo | 980 | 2.24 | 82 days | 2026-08-12 |
| 2026-05-21 | text | 712 | 1.63 | 75 days | 2026-08-19 |
| 2026-06-02 | photo | 905 | 2.18 | 63 days | 2026-08-31 |
| 2026-06-06 | video | 3,402 | 6.90 | 59 days | 2026-09-04 |
| 2026-06-09 | photo | 655 | 1.53 | 56 days | 2026-09-07 |
| 2026-06-23 | link | 1,188 | 2.41 | 42 days | 2026-09-21 |
| 2026-07-11 | video | 1,904 | 3.62 | 24 days | 2026-10-09 |
| 2026-07-20 | link | 1,402 | 2.99 | 15 days | 2026-10-18 |
| 2026-07-25 | text | 1,206 | 3.07 | 10 days | 2026-10-23 |
| 2026-07-28 | photo | 902 | 2.30 | 7 days | 2026-10-26 |

**The two illustration-only posts from `rubric.md` sections 4.1 and 4.3 are on this list too**, and are not treated as recommendations here for the same reason: idx 50 (the dated-hook illustration) does not even clear the 1.5x floor, so it is correctly absent from this table entirely; idx 52, `You do not need more storage. You need fewer decisions.` (2026-07-20, the concentration-trigger illustration, `link` type, 43.3 percent of the link bucket's total engagement), does appear here, at 15 days old, clearing on 2026-10-18. When it clears the gate, the concentration trigger will fire on it and it will ship as a remake, not a straight repost, exactly as `rubric.md` section 4.3 describes.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable. Part 1 was the working.

---

# Evergreen repost finder: Maya Torres

60 posts, 2026-03-21 to 2026-07-28, 130 days. This capture clears the 90-day span era-adjusted scoring needs, so every score below is era-adjusted: each post measured against the median of its own 10 nearest neighbors by publish order, per this skill's rubric.

Of these 60 posts: 58 clear the evergreen filter (not dated). Of those, 20 are reuse-safe, 90 days old or more. Of those, 4 also clear the 1.5x score floor, checked on the raw value, never the rounded display value. **4 posts make the shortlist.** One more, "3 bins, 20 minutes, one entryway that finally works," rounds to a displayed 1.50 but is 1.4964 unrounded, 0.0037 under the floor; it is named below as a near-miss rather than shortlisted. 12 more clear the score floor and are not old enough yet, listed on the watch list below.

---

## Your evergreen shortlist

| Post, verbatim (truncated) | Score (denominator named) | Age | Evergreen class | Repost or remake | Why |
|---|---|---|---|---|---|
| "Labels do not organize anything. Limits do." | 2.76x era-adjusted, its 10-post neighborhood median was 378.5 | 110 days | CLEAN EVERGREEN | REPOST AS-IS | video, already your best-performing rankable format, no dated language |
| "I opened a client's coat closet last Tuesday and a sled fell on me." | 2.11x era-adjusted, neighborhood median 326.5 | 122 days | CLEAN EVERGREEN | REPOST AS-IS | video, "last Tuesday" and "In May" are the scene, not a claim, so nothing to update |
| "Do you actually use the top shelf, or do you just store guilt there?" | 1.89x era-adjusted, neighborhood median 323.0 | 117 days | CLEAN EVERGREEN | REMAKE | format-upgrade: text median 388 is 1.51x below video median 585 |
| "5 things I removed from my kitchen counter that I have not missed once." | 1.59x era-adjusted, neighborhood median 307.0 | 124 days | CLEAN EVERGREEN | REMAKE | format-upgrade: album median 393 is 1.49x below video median 585 |

No posts were excluded as DATED-BODY on this run. 2 posts (2026-05-23 and 2026-07-16) classified DATED-HOOK-ONLY; neither clears the 1.5x score floor, so neither appears above, and both are named here rather than silently dropped.

**One near-miss, named rather than dropped:** "3 bins, 20 minutes, one entryway that finally works." (2026-04-30, photo, 96 days old) clears the evergreen filter and the age gate cleanly. Its score displays as 1.50x, but the unrounded value is 1.4964x, 0.0037 under this skill's 1.5x floor. It is not on the shortlist and not on the watch list either, since the watch list is for posts that are not yet reuse-safe and this one already is. It is simply short on evidence, not on time; a stronger performance on a future post would be what moves it, not the calendar.

---

## The refreshed drafts

**1. 1.89x | CLEAN EVERGREEN | trigger: format-upgrade (text to video, 1.51x)**

Original, posted 2026-04-09:
> Do you actually use the top shelf, or do you just store guilt there?
>
> Go look. I will wait.
> Most top shelves hold three things: seasonal items, sentimental items, and evidence of a purchase you regret.

Refreshed:
> Do you actually use the top shelf, or do you just store guilt there?
>
> Go check right now, on camera, while I wait.
> Three things live up there in every home I have organized: seasonal stuff, sentimental stuff, and one purchase nobody wants to admit to.

**What changed and why:** hook kept exactly as written, it earned its score and it is not dated. Body trimmed to your video posts' own two-line pattern, because a video can show the check instead of describing it.

**2. 1.59x | CLEAN EVERGREEN | trigger: format-upgrade (album to video, 1.49x)**

Original, posted 2026-04-02:
> 5 things I removed from my kitchen counter that I have not missed once.
>
> The knife block, the fruit bowl, the mail tray, the second cutting board, and the paper towel stand.
> All five had a home eighteen inches away. All five were on the counter out of habit, not need.

Refreshed:
> 5 things I removed from my kitchen counter that I have not missed once.
>
> Watch what was actually still sitting there before I touched a single thing.
> Every one of them had a home eighteen inches away. They were out of habit, not need.

**What changed and why:** hook kept exactly as written. The item list is what the video shows; the caption points at the reveal instead of naming all five, keeping the closing argument almost untouched because that is the line video cannot deliver on its own.

**"Labels do not organize anything. Limits do." (110 days) and "I opened a client's coat closet last Tuesday and a sled fell on me." (122 days): no refresh needed. Repost these two exactly as they are.**

**No draft for "3 bins, 20 minutes, one entryway that finally works."** It is a near-miss, not a shortlist member: it clears the evergreen filter and the age gate, but its raw score, 1.4964x, is 0.0037 under the 1.5x floor even though it displays as 1.50x. This skill does not draft refreshes for posts that did not clear the shortlist.

---

## Watch list: high scores that are not reuse-safe yet

| Post, verbatim (truncated) | Score | Age | Clears on |
|---|---|---|---|
| "A client cried in her own pantry on Monday, and it was not about food." | 9.41x | 89 days | 2026-08-05 |
| "Want to know why your system keeps failing by week three?" | 1.60x | 87 days | 2026-08-07 |
| "You are storing three sizes of clothes for three versions of yourself." | 2.24x | 82 days | 2026-08-12 |
| "There is one shelf in every kitchen that predicts the whole house." | 1.63x | 75 days | 2026-08-19 |
| "The container store is the last stop, not the first." | 2.18x | 63 days | 2026-08-31 |
| "4 rules that keep my pantry alive past week three." | 6.90x | 59 days | 2026-09-04 |
| "Ever wonder why the drop zone is always by the door?" | 1.53x | 56 days | 2026-09-07 |
| "Most organizing systems fail because they were designed on a good day." | 2.41x | 42 days | 2026-09-21 |
| "I have a closet in my own house I do not film." | 3.62x | 24 days | 2026-10-09 |
| "You do not need more storage. You need fewer decisions." | 2.99x | 15 days | 2026-10-18 |
| "The cheapest thing in my organizing kit does the most work, and it is not what you think." | 3.07x | 10 days | 2026-10-23 |
| "What is the one drawer you would not let a guest open?" | 2.30x | 7 days | 2026-10-26 |

Your single highest-scoring post in this file, at 9.41x, is 89 days old and needs 1 more day. It is not on the shortlist above for exactly that reason, and it is the sharpest proof that the 90-day gate here is a real constraint, not a formality.

---

## What this analysis is standing on

Analyzed 60 posts captured 2026-03-21 to 2026-07-28, 130 days. Scores are era-adjusted, each post against the median of its own 10 nearest neighbors by publish order, per this skill's rubric, because this capture clears the 90-day span and 21-post minimum the method needs. Every comparator against the 1.5x floor is checked on the raw score, never the rounded display value. The reuse-safety age gate is 90 days, a working number, not a platform fact. 0 posts excluded as dated in the body, not just the hook. 2 posts classified dated in the hook only, neither of which cleared the score floor. 1 post, already reuse-safe, missed the raw-value score floor by 0.0037 and is named above as a near-miss rather than shortlisted. 12 posts score high enough for the shortlist but are not old enough yet, listed above with the exact date each one clears the gate.

Not in your export, so not in this analysis: sponsored or paid-partnership flags, so this cannot tell you if a recommended post was originally boosted. Per-emoji reactions. Reach or impressions. Follower history, so era adjustment reduces but does not remove the confound between an old audience size and a new one.

PostSnag captures what you scrolled, so this is a sample of the account, not its full history.

Analysis based on 60 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=evergreen-repost-finder

---

# APPENDIX: the same analysis on a free-tier export

Run against `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv`, the most recent 30 rows of the same file. This is what a free-tier user gets, and it is included so nobody has to guess how honest the degradation actually is.

```
posts                30
date range            2026-05-30 to 2026-07-28
span                  60 days
lite mode             ON (30 posts < 40)
corpus median         530.0
era-adjustment        NOT ACTIVE: span 60 days is under the 90-day precondition,
                       and lite mode is on. Every score below is a multiple of
                       the corpus median (530.0), never called an era score.
```

**The reuse-safety gate is where this run actually dies, and it is worth stating exactly why.** The oldest post in this free-tier slice is 66 days old (2026-05-30). The gate is 90 days. Every post in this export is at least 24 days short, because the free tier is always your most recent 30 posts, a recency window by definition. **0 of 30 posts can be reuse-safe on this export, not because the data is thin, but because the export structurally cannot contain a post old enough.**

**8 posts clear the 1.5x score floor. 0 of them are reuse-safe.** All 8 go straight to the watch list, none to the shortlist:

| Post, verbatim (truncated) | Score (corpus-median multiple) | Age | Clears on |
|---|---|---|---|
| "4 rules that keep my pantry alive past week three." | 6.42x of 530.0 | 59 days | 2026-09-04 |
| "I have a closet in my own house I do not film." | 3.59x of 530.0 | 24 days | 2026-10-09 |
| "You do not need more storage. You need fewer decisions." | 2.65x of 530.0 | 15 days | 2026-10-18 |
| "The cheapest thing in my organizing kit does the most work, and it is not what you think." | 2.28x of 530.0 | 10 days | 2026-10-23 |
| "Most organizing systems fail because they were designed on a good day." | 2.24x of 530.0 | 42 days | 2026-09-21 |
| "The container store is the last stop, not the first." | 1.71x of 530.0 | 63 days | 2026-08-31 |
| "What is the one drawer you would not let a guest open?" | 1.70x of 530.0 | 7 days | 2026-10-26 |
| "What would you keep if you had to move on Friday?" | 1.56x of 530.0 | 47 days | 2026-09-16 |

**What survives:** the funnel-count sentence, the watch list itself with real dates, and the fact that this skill can tell the user precisely how much deeper to capture rather than shrugging.

**What does not survive:** every one of the four posts on the full run's shortlist, "Labels do not organize anything," the coat closet story, the top-shelf question, and the five-things list, plus the full run's one named near-miss, the three-bins post, are all from April, outside this 30-post window entirely. A free-tier user never sees any of them, not because they scored badly, but because the free export cannot reach back that far.

**The banner this run opens with:**

> **Depth needed.** This capture spans 60 days. This skill needs posts at least 90 days old before it will recommend reposting them, so it needs a capture spanning at least 90 days, ideally more. The oldest post in this export is 66 days old, 24 days short of the gate. Capture more with PostSnag and widen the window. Nothing below is fabricated to look useful; this is the honest list.

That banner, followed by an 8-row watch list and an empty shortlist, makes the evidence gap explicit: no guessing, no padding, a specific number of days and a specific reason.