# example-run.md

> **SYNTHETIC.** Maya Torres is a fictional creator. Every post, number, and date below is invented. Source file: `../../_shared/synthetic-data/profile-maya-torres.csv`. Nothing here describes a real person or a real Facebook account.

This is the rubric in `rubric.md` executed start to finish, with every number computed from the source file rather than estimated. Anyone can re-run the parse and check. If a number here disagrees with a recomputation from the CSV, this file is wrong and gets fixed.

**This run is checkable standalone, without opening the source CSV.** Step 3's table below reproduces all 60 hooks verbatim, each with its full engagement breakdown (reactions, comments, shares) and archetype label, in-file. Every median, bucket count, and ranking in the steps that follow is computed from that reproduced table, so a reader can re-derive every number in this file from this file alone.

Version 1.0 | 2026-08-04

---

# PART 1: THE WORK

Everything in Part 1 is the analyst's working, shown so the method is auditable. Part 2 is what the user actually receives.

---

## Step 1: Parse and validate

Parsed with a real CSV reader, columns addressed by header name.

```
rows parsed                60
physical lines in file     245        <- captions carry embedded newlines
captions with newlines     60 of 60
captions with commas       54 of 60
captions with quote marks   8 of 60
date range                 2026-03-21 to 2026-07-28
span                       130 days
empty captions             0
Views populated            14 rows (all video)
Views empty                46 rows (treated as absent, not zero)
row order in file          newest first, so sorted by parsed Posted before anything sequential
lite mode                  OFF (60 posts >= 40, 130 days >= 60)
corpus median engagement   458.5
corpus mean engagement     639.7
top quartile               k = floor(60/4) = 15, cut value 700, no tie at the boundary
```

**The line-count check matters.** An agent that read this file line by line would see 245 records instead of 60 and compute a median over caption fragments. The row count and the physical line count disagreeing by 4x is normal and expected on Facebook captions.

---

## Step 2: Extract the hook lines

On this capture, the hook is the first line of `Content` in all 60 cases.

```
CTA lines skipped (skip test A)      0
chrome lines skipped (skip test B)   0
leaked labels skipped (skip test C)  0
NO CAPTION                           0
UNCLASSIFIED after classification    0
```

**Worth saying out loud:** zero CTA skips is a finding, not a non-event. Maya never opens with a platform mechanic. Plenty of creators open 19 posts out of 30 with "Follow and comment TOOLS", and on those files the skip count is the first real thing the analysis has to report, because it means their actual hook is buried on a third of their posts.

---

## Step 3: Classify all 60 hooks

Precedence ladder run top to bottom, first match wins.

| # | Engagement | R / C / S | Type | Date | Archetype | Hook, verbatim |
|---|---|---|---|---|---|---|
| 1 | 4,118 | 3130 / 700 / 288 | video | 2026-05-07 | Story Cold Open | A client cried in her own pantry on Monday, and it was not about food. |
| 2 | 3,402 | 2381 / 748 / 273 | video | 2026-06-06 | Number Promise | 4 rules that keep my pantry alive past week three. |
| 3 | 1,904 | 1409 / 362 / 133 | video | 2026-07-11 | Confession | I have a closet in my own house I do not film. |
| 4 | 1,402 | 1066 / 238 / 98 | link | 2026-07-20 | Problem Callout | You do not need more storage. You need fewer decisions. |
| 5 | 1,206 | 796 / 314 / 96 | text | 2026-07-25 | Curiosity Gap | The cheapest thing in my organizing kit does the most work, and it is not what you think. |
| 6 | 1,188 | 879 / 226 / 83 | link | 2026-06-23 | Bold Claim | Most organizing systems fail because they were designed on a good day. |
| 7 | 1,044 | 710 / 251 / 83 | video | 2026-04-16 | Bold Claim | Labels do not organize anything. Limits do. |
| 8 | 980 | 647 / 255 / 78 | photo | 2026-05-14 | Problem Callout | You are storing three sizes of clothes for three versions of yourself. |
| 9 | 905 | 597 / 235 / 73 | photo | 2026-06-02 | Bold Claim | The container store is the last stop, not the first. |
| 10 | 902 | 613 / 216 / 73 | photo | 2026-07-28 | Question Open | What is the one drawer you would not let a guest open? |
| 11 | 826 | 661 / 116 / 49 | text | 2026-06-18 | Question Open | What would you keep if you had to move on Friday? |
| 12 | 744 | 536 / 149 / 59 | video | 2026-07-04 | Question Open | Is it clutter, or is it a decision you have not made yet? |
| 13 | 712 | 555 / 114 / 43 | text | 2026-05-21 | Curiosity Gap | There is one shelf in every kitchen that predicts the whole house. |
| 14 | 702 | 505 / 140 / 57 | text | 2026-05-09 | Question Open | Want to know why your system keeps failing by week three? |
| 15 | 700 | 476 / 168 / 56 | photo | 2026-06-30 | Number Promise | 7 questions that end every "but I might need it" argument. |
| 16 | 688 | 550 / 96 / 42 | video | 2026-04-04 | Story Cold Open | I opened a client's coat closet last Tuesday and a sled fell on me. |
| 17 | 655 | 511 / 105 / 39 | photo | 2026-06-09 | Question Open | Ever wonder why the drop zone is always by the door? |
| 18 | 615 | 430 / 135 / 50 | photo | 2026-04-30 | Number Promise | 3 bins, 20 minutes, one entryway that finally works. |
| 19 | 610 | 451 / 116 / 43 | text | 2026-04-09 | Question Open | Do you actually use the top shelf, or do you just store guilt there? |
| 20 | 604 | 423 / 133 / 48 | video | 2026-06-25 | Direct Address | To the person who reorganized at 11pm last night: I see you. |
| 21 | 566 | 408 / 113 / 45 | video | 2026-07-22 | Question Open | Why does the pantry always fail before the fridge does? |
| 22 | 560 | 414 / 106 / 40 | album | 2026-07-26 | Number Promise | 10 minutes a day beats 6 hours on Saturday. Here is the math. |
| 23 | 540 | 356 / 140 / 44 | photo | 2026-07-09 | Direct Address | If your kid is under five, ignore every closet video you have seen. |
| 24 | 522 | 397 / 89 / 36 | video | 2026-05-26 | Question Open | Which is faster: folding it, or hanging it? |
| 25 | 520 | 374 / 104 / 42 | video | 2026-06-16 | Story Cold Open | The first house I ever organized, I did everything wrong. |
| 26 | 512 | 410 / 72 / 30 | text | 2026-07-07 | Problem Callout | Your bathroom drawer has a graveyard of sample sizes. |
| 27 | 488 | 351 / 98 / 39 | album | 2026-04-02 | Number Promise | 5 things I removed from my kitchen counter that I have not missed once. |
| 28 | 470 | 310 / 122 / 38 | text | 2026-04-25 | Question Open | What if the bin is the reason you cannot find anything? |
| 29 | 466 | 317 / 112 / 37 | text | 2026-06-11 | Direct Address | Anyone with a garage and a car that lives outside, come here. |
| 30 | 462 | 333 / 92 / 37 | album | 2026-04-20 | Story Cold Open | My mother in law reorganized my spice rack while I was at the store. |
| 31 | 455 | 318 / 100 / 37 | video | 2026-05-19 | Problem Callout | The garage is not storage. It is a landfill with a door. |
| 32 | 420 | 336 / 59 / 25 | album | 2026-05-12 | Direct Address | Renters, this one changes nothing about your lease. |
| 33 | 402 | 297 / 76 / 29 | link | 2026-05-16 | Number Promise | The 12 items I tell every client to throw out on day one. |
| 34 | 402 | 297 / 76 / 29 | video | 2026-04-27 | Problem Callout | The playroom resets in forty minutes and falls apart in six. |
| 35 | 398 | 271 / 96 / 31 | photo | 2026-07-18 | Story Cold Open | I threw out my own label maker last month. |
| 36 | 388 | 310 / 54 / 24 | photo | 2026-07-24 | Direct Address | Small kitchen people, the counter is not the enemy. |
| 37 | 388 | 256 / 101 / 31 | photo | 2026-06-20 | Problem Callout | The paper pile on the counter is not paperwork. It is deferred decisions. |
| 38 | 388 | 272 / 85 / 31 | text | 2026-03-23 | Question Open | How many times have you organized this exact shelf? |
| 39 | 366 | 278 / 62 / 26 | album | 2026-06-13 | Problem Callout | Your kids' art is not clutter, but the pile of it is. |
| 40 | 355 | 277 / 57 / 21 | album | 2026-07-16 | Number Promise | 2 shelves, 6 categories, zero rearranging since March. |
| 41 | 355 | 284 / 50 / 21 | photo | 2026-04-23 | Direct Address | New parents, your entryway needs a bench and nothing else. |
| 42 | 344 | 275 / 48 / 21 | album | 2026-05-30 | Story Cold Open | I spent nine hours in a garage in Reno and left with two boxes. |
| 43 | 341 | 225 / 89 / 27 | photo | 2026-04-06 | Problem Callout | Your pantry looks organized in photos and fails on a Tuesday night. |
| 44 | 327 | 255 / 52 / 20 | text | 2026-06-27 | Problem Callout | You reorganize the same shelf every three months. |
| 45 | 318 | 229 / 64 / 25 | text | 2026-05-28 | Problem Callout | Every flat surface in your house is a shelf now. |
| 46 | 312 | 243 / 50 / 19 | video | 2026-03-26 | Problem Callout | The junk drawer is not the problem. The drawer next to it is. |
| 47 | 305 | 214 / 67 / 24 | text | 2026-07-13 | Question Open | How long does it take you to find scissors? |
| 48 | 305 | 232 / 52 / 21 | text | 2026-04-18 | Problem Callout | You clean the kitchen every night and it looks the same by Thursday. |
| 49 | 302 | 205 / 72 / 25 | photo | 2026-03-28 | Direct Address | If you have a bin labeled "misc", this one is for you. |
| 50 | 291 | 221 / 49 / 21 | text | 2026-03-30 | Problem Callout | You keep buying bins. You still cannot find anything. |
| 51 | 268 | 209 / 43 / 16 | photo | 2026-04-13 | Problem Callout | Nothing in your entryway has a home, so everything lives on the floor. |
| 52 | 266 | 202 / 45 / 19 | album | 2026-07-02 | Story Cold Open | She told me the room was "basically fine" and then opened the door. |
| 53 | 246 | 182 / 47 / 17 | photo | 2026-03-21 | Problem Callout | Your closet is not messy. It is over capacity. |
| 54 | 244 | 171 / 54 / 19 | link | 2026-04-11 | Direct Address | To everyone still folding fitted sheets: stop. |
| 55 | 238 | 186 / 38 / 14 | text | 2026-07-28 | Command | Go empty one drawer. Right now. Set a timer for four minutes. |
| 56 | 214 | 146 / 51 / 17 | photo | 2026-05-05 | Problem Callout | Your linen closet is where folded things go to unfold. |
| 57 | 208 | 146 / 46 / 16 | video | 2026-07-27 | Story Cold Open | We found a wedding gift, still boxed, from 2011. |
| 58 | 190 | 129 / 46 / 15 | photo | 2026-05-23 | Direct Address | If you work from the kitchen table, read this before Sunday. |
| 59 | 182 | 135 / 35 / 12 | text | 2026-06-04 | Problem Callout | You have four half-used bottles of the same cleaner under the sink. |
| 60 | 152 | 119 / 24 / 9 | text | 2026-05-02 | Command | Stop labeling. Start counting. |

**Five classification calls worth showing, because they are the ones the ladder exists for:**

| Row | Hook | Naive call | Ladder call | Why |
|---|---|---|---|---|
| 4 | `You do not need more storage. You need fewer decisions.` | Bold Claim (it reads as a flat contrarian assertion) | **Problem Callout** | Both required markers of rule 2.4 fire: second-person subject in the first clause, and a failure attributed to the reader. Problem Callout sits at ladder position 11 and Bold Claim at 12, so the ladder resolves it before the catch-all is reached. Bold Claim's own first marker also excludes it: that archetype requires a general subject, not `you`. |
| 8 | `You are storing three sizes of clothes for three versions of yourself.` | Number Promise (two numbers in it) | **Problem Callout** | The number is not the head of the subject noun phrase and does not count the post's contents. Marker 3 of rule 2.5 fails. |
| 14 | `Want to know why your system keeps failing by week three?` | Curiosity Gap (it withholds) | **Question Open** | Question in form. Form wins over function throughout, so two agents reach the same label. |
| 35 | `I threw out my own label maker last month.` | Confession (admission against interest) | **Story Cold Open** | Past-tense single event with a time anchor. Confession requires a present-tense standing state. |
| 54 | `To everyone still folding fitted sheets: stop.` | Command (ends in an imperative) | **Direct Address** | Command requires the imperative to be the first word. First word is `To`, and the address filters readers before the instruction. |

---

## Step 4: Bucket math and the concentration check

| Archetype | n | median | mean | top post | median after deleting top | change | top post's share of bucket | mean / median | Flags |
|---|---|---|---|---|---|---|---|---|---|
| Confession | 1 | 1,904 | 1,904 | 1,904 | n/a | n/a | 100.0% | 1.00 | n=1 |
| Bold Claim | 3 | 1,044 | 1,046 | 1,188 | 974.5 | -6.7% | 37.9% | 1.00 | **none** |
| Curiosity Gap | 2 | 959 | 959 | 1,206 | 712 | -25.8% | 62.9% | 1.00 | 2 flags |
| Question Open | 11 | 610 | 608 | 902 | 588 | -3.6% | 13.5% | 1.00 | none |
| Number Promise | 7 | 560 | 932 | 3,402 | 524 | -6.4% | 52.2% | 1.66 | 2 flags |
| Story Cold Open | 8 | 430 | 876 | 4,118 | 398 | -7.4% | 58.8% | 2.04 | 2 flags |
| Direct Address | 9 | 388 | 390 | 604 | 372 | -4.3% | 17.2% | 1.00 | none |
| Problem Callout | 17 | 327 | 430 | 1,402 | 322.5 | -1.4% | 19.2% | 1.31 | none |
| Command | 2 | 195 | 195 | 238 | 152 | -22.1% | 61.0% | 1.00 | 2 flags |

Thresholds from `references/foundations.md` section 4 (condensed; full version in the bundle): flag if the median moves more than 20 percent, or the top post is more than 40 percent of the bucket total, or mean over median is 1.5 or higher.

**Reading it:**

- Story Cold Open and Number Promise each fire two flags. Both are being carried by a single post. Neither becomes a recommendation; instead the analysis names the post.
- **Bold Claim is the only bucket in the file with a small n and zero flags.** Three posts, tight spread, top post 38 percent of the bucket total, mean and median within 2 points of each other. All three did it, not one. That is the most useful line in this table and it belongs to a bucket the 5-post floor correctly refuses to rank. Note how close the top-post share now sits to the 40 percent threshold: at n=3 a bucket is one good post away from flagging, which is the floor earning its keep rather than the flag failing.
- Curiosity Gap and Command both flag, and both are n=2, where flagging is close to automatic. Reported, not interpreted.

---

## Step 5: The ranking

**Rankable buckets, n at or above 5, ranked by median engagement:**

1. Question Open, 610 across 11 posts
2. Number Promise, 560 across 7 posts
3. Story Cold Open, 430 across 8 posts
4. Direct Address, 388 across 9 posts
5. Problem Callout, 327 across 17 posts

**The same buckets ranked by mean instead:**

1. Number Promise, 932
2. Story Cold Open, 876
3. Question Open, 608
4. Problem Callout, 430
5. Direct Address, 390

**The top 3 disagree, so this gets said in the output, not buried here.** Three posts create the entire difference: the 4,118 story open on 2026-05-07, the 3,402 number promise on 2026-06-06, and the 1,402 problem callout on 2026-07-20. Delete those three and the two rankings match position for position. Leave any one of them in and they do not: the 1,402 post alone lifts Problem Callout's mean from 369 to 430 while moving its median 4.5 points, which is the whole argument for medians in one line. The median ranking is the one shipped, because it describes what happens when Maya writes a normal post, and next week's post will be a normal post.

No tie-breaks were needed at the archetype level.

---

## Step 6: Composition

**Top quartile is the top 15 posts, cut value 700.** Composition of those 15 against composition of all 60:

| Archetype | Share of the 60 posts | Share of the top 15 | Direction |
|---|---|---|---|
| Bold Claim | 5.0% (3 of 60) | 20.0% (3 of 15) | **4x over-represented** |
| Curiosity Gap | 3.3% (2 of 60) | 13.3% (2 of 15) | 4x over-represented |
| Question Open | 18.3% (11 of 60) | 26.7% (4 of 15) | over-represented |
| Confession | 1.7% (1 of 60) | 6.7% (1 of 15) | over-represented, n=1 |
| Number Promise | 11.7% (7 of 60) | 13.3% (2 of 15) | roughly even |
| Story Cold Open | 13.3% (8 of 60) | 6.7% (1 of 15) | under-represented |
| **Problem Callout** | **28.3% (17 of 60)** | **13.3% (2 of 15)** | **2x under-represented** |
| Direct Address | 15.0% (9 of 60) | 0% (0 of 15) | absent from the top quartile |
| Command | 3.3% (2 of 60) | 0% (0 of 15) | absent, n=2 |

**Top 10 versus bottom 10:**

| Set | Composition |
|---|---|
| Top 10 | Bold Claim 3, Problem Callout 2, then one each of Story Cold Open, Number Promise, Confession, Curiosity Gap, Question Open |
| Bottom 10 | Problem Callout 4, Story Cold Open 2, Direct Address 2, Command 2 |

Bold Claim: 3 of the top 10, 0 of the bottom 10, on 3 total posts. Problem Callout: 2 of the top 10, 4 of the bottom 10, on 17 total posts.

---

## Step 7: The structural read

| Feature | Bucket | Posts | Median | Ranked? |
|---|---|---|---|---|
| Hook length | 0-50 chars | 13 | 327 | yes |
| Hook length | 51-75 chars | 46 | 464 | yes |
| Hook length | 76-100 chars | 1 | 1,206 | no, n below 5 |
| Hook length | 101+ chars | 0 | n/a | no posts |
| Caption length | 0-250 chars | 39 | 388 | yes |
| Caption length | 251-400 chars | 21 | 700 | yes |
| Caption length | 401+ chars | 0 | n/a | no posts |
| Question mark in hook | yes | 11 | 610 | see the confound note |
| Question mark in hook | no | 49 | 402 | see the confound note |

**Confound note, and this is the kind of thing that separates an analysis from a table.** The 11 posts with a question mark in the hook are **the same 11 posts** as the Question Open archetype. Identical set, identical median. Reporting "question marks earn 1.5x" as a separate finding would be counting one piece of evidence twice and presenting it as two. It gets one line in the output, cross-referenced, not its own headline.

**Caption length, checked for the same problem.** Longer captions carry a 700 median against 388, which is 1.80x, and the two buckets are 21 and 39 posts, so both clear the floor. Is it just archetype mix? Partly: 5 of the 7 number promises and 4 of the 8 story opens are long captions. So the effect was checked **within** archetypes:

- Question Open: 7 short captions median 522, 4 long captions median 764
- Problem Callout: 13 short captions median 318, 4 long captions median 684

The direction holds inside both archetypes. Both long-caption sub-buckets are under the 5-post floor, so this is reported as **directional and consistent**, not as a measured effect. That phrasing is doing real work: the corpus-level number is solid, the causal read is not, and the output says exactly that much and no more.

**No-variance line.** Every caption in this capture uses the same paragraph structure, one hook line then one body block, so there is no signal to read on paragraphing. Said out loud, because a reader told nothing about it cannot tell whether it was checked.

**Hooks over 120 characters: 0.** Nothing in this capture is at risk of needing a second rendered line. No character limit is asserted anywhere, because Facebook's truncation point varies by surface and changes without notice.

---

## Step 8: The video secondary lens

14 video rows carry `Views`. The other 46 rows have `Views` empty, which means absent, not zero, so they are excluded from every calculation in this section and the denominator is stated: 14.

```
raw engagement across the 14 videos      208 to 4,118     (a 19.8x spread)
engagement per view across the same 14   1.66% to 2.20%   (a 1.32x spread)
median engagement per view               2.07%
```

**Whatever separates Maya's best video from her worst happened before the view, not after it.** Her 208-engagement video converts views to engagement at 2.17 percent. Her 4,118-engagement video converts at 1.92 percent, slightly worse. The 20x difference between them is entirely a difference in how many views each one got.

That is as far as the data goes. PostSnag does not capture reach or impressions, so "before the view" cannot be broken down further, and this analysis does not speculate about why one video was served more than another.

---

## Step 9: Visual hooks

**Omitted.** No screenshots and no media zip were supplied with this run. The export carries `Media_URLs` on 39 rows, and those are expiring Facebook links that this skill never fetches. Nothing about Maya's images appears anywhere in the output.

---

## Step 10: The gap list

**Tier 2, used 1 to 4 times with a median above the corpus median of 458.5**, ordered by median descending:

| Archetype | n | median | vs corpus median |
|---|---|---|---|
| Confession | 1 | 1,904 | 4.15x |
| Bold Claim | 3 | 1,044 | 2.28x |
| Curiosity Gap | 2 | 959 | 2.09x |

**Tier 3, used 1 to 4 times with a median below the corpus median.** Reported, not recommended: Command, 2 posts, median 195, which is 0.43x the corpus median. Tried twice, landed below her median both times, on too few posts to conclude anything.

**Tier 1, never used as an opening line.** Three archetypes: Contrarian Take, Myth Bust, Permission Grant. Ordered by the latent-fit test, which searches the **bodies** of her posts for each archetype's recognition markers:

| Archetype | Marker hits in hooks | Marker hits in bodies | Order |
|---|---|---|---|
| Permission Grant | 0 | **2** | 1st |
| Contrarian Take | 0 | 0 | 2nd, on topic fit |
| Myth Bust | 0 | 0 | 3rd, on topic fit |

The two Permission Grant body hits, verbatim:

- `You are allowed to make a temporary place work for you.` (line 3 of the post at 420 engagements, 2026-05-12)
- `Nobody has ever opened a linen closet and graded your corners.` (line 3 of the post at 244 engagements, 2026-04-11)

**She already writes this archetype. She has buried it in line 3 both times and has never once led with it.** That is the highest-confidence gap the analysis produced, and it came out of a mechanical grep rather than a hunch.

**The five, filled:** Confession, Bold Claim, Curiosity Gap (all Tier 2), then Permission Grant and Contrarian Take (Tier 1).

**Every drafted hook is pulled from `hook-template-library.md` and filled with Maya's own subject matter, per rubric section 6 and Method step 9.** Two of the five are traceable to a specific numbered template in the write-up below: the Permission Grant draft is template 43, and the Contrarian Take draft is template 27. Naming the template number is what turns "drafted for you" into a checkable claim instead of a black box.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable. Part 1 was the working.

---

# Hook analysis: Maya Torres

60 posts, 2026-03-21 to 2026-07-28, 130 days. All 60 had captions and were classified. No posts opened with a call-to-action line, so every hook below is the creator's real first sentence.

Median engagement across the whole capture: 458.5. Engagement here means reactions plus comments plus shares.

---

## Your hook patterns

| Archetype | Posts | Median engagement | Share of your top 15 | Best example, verbatim |
|---|---|---|---|---|
| Question Open | 11 | 610 | 4 of 15 | "What is the one drawer you would not let a guest open?" (902) |
| Number Promise | 7 | 560 | 2 of 15 | "4 rules that keep my pantry alive past week three." (3,402) |
| Story Cold Open | 8 | 430 | 1 of 15 | "A client cried in her own pantry on Monday, and it was not about food." (4,118) |
| Direct Address | 9 | 388 | 0 of 15 | "To the person who reorganized at 11pm last night: I see you." (604) |
| Problem Callout | 17 | 327 | 2 of 15 | "You do not need more storage. You need fewer decisions." (1,402) |

**Ranked by median engagement.** Ranked by average instead, Number Promise would be first and Question Open third. Three posts are the entire difference: the pantry story at 4,118, the four rules at 3,402, and the storage-versus-decisions post at 1,402. The median ranking is the one above, because it describes what happens when you write a normal post, and next week's post will be a normal post.

**Too small to rank, listed because they matter:** Bold Claim (3 posts, median 1,044), Curiosity Gap (2 posts, median 959), Command (2 posts, median 195), Confession (1 post, 1,904).

**Read that Bold Claim line again.** Three posts, a median of 1,044, which is 2.3 times your overall median, and three of your top ten posts. It gets no rank number because three posts is not a measurement. It is also the cleanest signal in this file, and it is the first thing on your test list below.

**Two archetypes are carried by one post each, so their averages are noise:** Story Cold Open sits at a median of 430 across 8 posts, but the pantry story alone accounts for 59 percent of the archetype's total engagement. Number Promise sits at 560 across 7 posts with the four-rules post accounting for 52 percent. Use the medians. Ignore the averages on those two.

---

## What you over-invest in and what you under-invest in

| Archetype | Share of your posts | Share of your top 15 |
|---|---|---|
| Bold Claim | 5.0% (3 of 60) | 20.0% (3 of 15) |
| Curiosity Gap | 3.3% (2 of 60) | 13.3% (2 of 15) |
| Question Open | 18.3% (11 of 60) | 26.7% (4 of 15) |
| Problem Callout | 28.3% (17 of 60) | 13.3% (2 of 15) |
| Direct Address | 15.0% (9 of 60) | 0% (0 of 15) |

**Problem callouts are 28 percent of everything you write and 13 percent of what works.** They are also 4 of your bottom 10 posts, against 2 in your top 10. Bold claims are 5 percent of what you write and 20 percent of what works, and 3 of your top 10, with zero in the bottom 10. Bold claim earns four times its share of your best posts on a fifth of the volume, and problem callout returns half its share. Swapping some of the second for some of the first is the single highest-value change available to you.

Direct address is the quieter problem: 9 posts, none of them in your top 15, none in your bottom 10 either. It is not failing. It is just not doing anything, and it is 15 percent of your output.

**Top 10 versus bottom 10:** your top 10 is 3 bold claims, 2 problem callouts, and one each of five other archetypes. Your bottom 10 is 4 problem callouts, 2 story opens, 2 direct addresses, and both of your commands.

---

## The structural read

| Feature | Bucket | Posts | Median engagement |
|---|---|---|---|
| Hook length | 0-50 characters | 13 | 327 |
| Hook length | 51-75 characters | 46 | 464 |
| Hook length | 76-100 characters | 1 | 1,206 (not ranked, one post) |
| Caption length | 0-250 characters | 39 | 388 |
| Caption length | 251-400 characters | 21 | 700 |

**Your short hooks underperform.** Under 50 characters, median 327. Between 51 and 75, median 464, on 46 posts. Your instinct to be punchy is costing you: at 40 characters you can name a problem, and at 65 you can name it and turn it.

**Your longer captions do 1.8x.** 700 against 388. That effect survives a check inside your two biggest archetypes, though the sub-groups there are too small to call it measured rather than directional. Both of your longest-caption posts are also two of your best.

Question marks in hooks show a 610 median against 402. **That is not a separate finding.** All 11 of your question-mark hooks are the same 11 posts as your Question Open archetype, so it is the archetype result restated, not additional evidence.

Every caption in this capture uses the same paragraph structure, so there is nothing to read on paragraphing. No hook here runs over 120 characters, so none are at risk of needing a second rendered line.

**Videos:** across your 14 videos, raw engagement spans 20x but engagement per view spans 1.32x, from 1.66 to 2.20 percent. Your 208-engagement video converts views to engagement slightly better than your 4,118 one does. Whatever separated them happened before the view, not after it. Your export does not carry reach or impressions, so that is as far as this goes.

---

## Visual hooks

Not analyzed. Your export carries `Media_URLs`, but those are expiring Facebook links and this skill never fetches them. Paste screenshots or supply the media zip from your capture and rerun to get this section.

---

## Your top 10 hooks, as templates

**1. 4,118 engagements | Story Cold Open**

> A client cried in her own pantry on Monday, and it was not about food.

**Template:** `A {person} {emotional verb} in their own {mundane place} on {weekday}, and it was not about {the obvious subject}.`
**Use it for:** a client story where the real subject is not the room.

**2. 3,402 engagements | Number Promise**

> 4 rules that keep my pantry alive past week three.

**Template:** `{N} rules that keep my {system} alive past week {N}.`
**Use it for:** a system post where the failure point is a known interval.

**3. 1,904 engagements | Confession**

> I have a closet in my own house I do not film.

**Template:** `I have a {area} in my own {domain} I do not {show}.`
**Use it for:** the post that costs you authority and buys you trust.

**4. 1,402 engagements | Problem Callout**

> You do not need more storage. You need fewer decisions.

**Template:** `You do not need more {resource}. You need fewer {decisions}.`
**Use it for:** reframing what the reader thinks they came for. This is your best post that is not a story, a number, or a confession, and it is a problem callout, which is the archetype you otherwise under-perform with. The difference is that it names the fix in the same breath as the failure.

**5. 1,206 engagements | Curiosity Gap**

> The cheapest thing in my organizing kit does the most work, and it is not what you think.

**Template:** `The cheapest thing in my {kit} does the most work, and it is not what you think.`
**Use it for:** a reveal post. Only when the answer is genuinely surprising.

**6. 1,188 engagements | Bold Claim**

> Most organizing systems fail because they were designed on a good day.

**Template:** `Most {systems} fail because they were designed on a good day.`
**Use it for:** explaining a failure the reader has already had, without blaming them.

**7. 1,044 engagements | Bold Claim**

> Labels do not organize anything. Limits do.

**Template:** `{Thing everyone buys} does not {the job they bought it for}. {Thing nobody buys} does.`
**Use it for:** a swap post. The body has to prove the swap.

**8. 980 engagements | Problem Callout**

> You are storing three sizes of clothes for three versions of yourself.

**Template:** `You are storing {N} {versions of a thing} for {N} versions of yourself.`
**Use it for:** your second-best problem callout, one of the two that reached your top 15. It works because it is about identity, not storage.

**9. 905 engagements | Bold Claim**

> The container store is the last stop, not the first.

**Template:** `{Common first move} is the last step, not the first.`
**Use it for:** reordering something the reader believes is a starting point.

**10. 902 engagements | Question Open**

> What is the one drawer you would not let a guest open?

**Template:** `What is the one {small container} you would not let a {guest} open?`
**Use it for:** a comment driver. Everyone has an answer and most of them want to say it.

---

## 5 archetypes to test next

**1. Confession | UNDERUSED: 1 post, 1,904 engagements, 4.15x your median**

One post, so it is a single observation rather than a pattern, which is exactly why it belongs on a test list instead of in the ranking above. It is also your third-best post of the last 130 days and the only time in 60 posts you admitted a room you have not fixed. You spend most of your captions being the person who has this handled. The one time you were not, it outperformed everything except two posts.

**Drafted for you:** "I still have a box of my kids' school papers I have never opened, and I have been telling clients to open theirs for eleven years."

**2. Bold Claim | UNDERUSED: 3 posts, median 1,044, 2.28x your median**

Three attempts, three of your top ten, none in your bottom ten, and the tightest spread of any small bucket in the file, which means it was not one lucky post carrying the other two. This is the highest-confidence recommendation in the analysis. Write two more this month and it clears the ranking floor, at which point you will know rather than suspect.

**Drafted for you:** "Storage does not solve a storage problem. A limit does, and a limit is free."

**3. Curiosity Gap | UNDERUSED: 2 posts, median 959, 2.09x your median**

Both attempts landed in your top 15 out of 60. Two posts is not evidence, but two for two on an archetype you barely touch is worth a third and a fourth.

**Drafted for you:** "There is one drawer in every house that tells me exactly how the rest of it works, and it is never the one people show me."

**4. Permission Grant | UNEXPLORED: never used as an opening line**

**You already write this.** It shows up in the body of two of your posts and has never once been your first line:

> "You are allowed to make a temporary place work for you." (line 3 of your renters post)
> "Nobody has ever opened a linen closet and graded your corners." (line 3 of your fitted-sheets post)

Both times you buried a release in line 3 under a hook that was doing something else. It is the only archetype in this analysis that lowers the reader's workload in the first line instead of adding to it, and you are already fluent in it.

**Drafted for you:** "You are allowed to keep the ugly bin that works. Nobody is coming to inspect your linen closet." *(This is `hook-template-library.md` template 43, `You are allowed to keep the {ugly or imperfect thing} that works. Nobody is coming to inspect your {domain}.`, filled with Maya's own subject matter, per rubric section 6's instruction to draft gap hooks from the library rather than invent generic ones.)*

**5. Contrarian Take | UNEXPLORED: never used**

Zero instances anywhere in your 60 posts, hooks or bodies. Your bold claims are already this archetype minus one clause: "Most organizing systems fail because they were designed on a good day" becomes a contrarian take the moment you name who is telling people otherwise. Same argument, more comments, and more people arguing with you in the replies, which you should decide you want before you use it.

**Drafted for you:** "Everyone tells you to buy the bins first. That is exactly backwards, and it is why you own four empty bins and a full closet." *(This is `hook-template-library.md` template 27, `Everyone tells you to {common first step}. That is exactly backwards, and it is why you own {evidence of the failure}.`, filled with Maya's own subject matter.)*

---

## What this analysis is standing on

Analyzed 60 posts captured 2026-03-21 to 2026-07-28, 130 days. No posts were excluded: all 60 had captions and all 60 classified into an archetype. Rankings use median engagement, which is reactions plus comments plus shares, unweighted. Archetypes with fewer than 5 posts are listed with their numbers but never ranked. Story Cold Open and Number Promise are each carried by a single post, so their averages are not used anywhere in this analysis. The question-mark result is the Question Open result restated on the same 11 posts, not independent evidence.

Not in your export, so not in this analysis: sponsored or paid-partnership flags, so a boosted post looks identical to an organic one here. Per-emoji reactions. Reach or impressions. Comment text. Follower history.

PostSnag captures what you scrolled, so this is a sample of the account, not its full history.

Analysis based on 60 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-hook-analyzer

---

# APPENDIX: the same analysis on a free-tier export

Run against `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv`, which is the most recent 30 rows of the same file. This is what a free-tier user gets, and it is included so nobody has to guess how honest the degradation actually is.

```
posts                30
date range           2026-05-30 to 2026-07-28
span                 60 days
lite mode            ON (30 posts < 40)
corpus median        530
top quartile         k = 7, cut value 902
```

**Buckets that clear the 5-post floor: 3 of 9.**

| Archetype | n | median | Rankable? |
|---|---|---|---|
| Question Open | 6 | 699.5 | yes |
| Problem Callout | 6 | 377 | yes |
| Story Cold Open | 5 | 344 | yes |
| Number Promise | 4 | 630 | no |
| Direct Address | 4 | 503 | no |
| Bold Claim | 2 | 1,046.5 | no |
| Confession | 1 | 1,904 | no |
| Curiosity Gap | 1 | 1,206 | no |
| Command | 1 | 238 | no |

**What survives:** the Question Open finding, the Problem Callout over-investment finding (6 of 30, tied with Question Open as her most-used archetype and sitting at 377 against a slice median of 530), the top-10 hook templates, and the Bold Claim signal, which is visible but on 2 posts instead of 3.

**What does not:** six of nine archetypes fall below the floor, so two thirds of the pattern table is unranked. The gap list gets thinner because there is less evidence to tier with. And the free slice is her **most recent** 30 posts, not a random 30, so it describes what she has been doing since May rather than what she does.

**The banner this run would open with:**

> **Lite mode.** This capture has 30 posts across 60 days. Below 40 posts or 60 days this analysis runs shallow on purpose. Degraded here: 6 of your 9 used archetypes fall below the 5-post ranking floor, and the gap list is built on less evidence. To rank most of your archetypes, capture about 60 posts across at least 120 days.

That banner gives the number of additional posts, the date span and the analysis they would support.
