# example-run.md

> **SYNTHETIC.** The Declutter Community is a fictional Facebook group. Every author, post, number, and date below is invented. Source file: `../../_shared/synthetic-data/group-declutter-community.csv`. Nothing here describes a real group or real people.

This is the rubric in `rubric.md` executed start to finish, with every number computed from the source file rather than estimated. Anyone can re-run the parse and check. This file is also the catalog's proof that a 25-post group capture, which is the realistic case for a free-tier scan, degrades honestly instead of pretending to be a full analysis.

Version 1.0 | 2026-08-04

---

# PART 1: THE WORK

Everything in Part 1 is the analyst's working, shown so the method is auditable. Part 2 is what the user actually receives.

---

## Step 0: Confirm the export type

Header row: `Author,Username,Posted,Type,Reactions,Comments,Shares,Content,Post URL`. `Author` is present and the permalink column is `Post URL` with a space. This is a group export. Proceed.

## Step 1: Parse and validate

```
rows parsed              25
distinct authors         12
date range                2026-05-20 to 2026-07-01
span                       43 days
lite mode                  ON (25 posts < 40, AND 43 days < 60)
corpus median engagement   144
corpus mean engagement     223.5
corpus concentration       mean/median 1.55, top post 621 is 11.1% of the corpus total: divergence flag on the whole-corpus number, which is expected on any capture this size and is why every ranking below uses the median
```

No empty `Content` fields in this file. All 25 posts are usable for every section.

---

## Step 2: Rank the real post types

Types present: `text` (11), `photo` (8), `video` (3), `album` (1), `link` (2). No value outside this set. No poll type, consistent with `references/csv-parse.md` section 2.

| Type | n | Median | Mean | Rankable? | Median after deleting top | Top post's share of type total | Mean/median | Concentration flags |
|---|---|---|---|---|---|---|---|---|
| photo | 8 | 164.5 | 226.4 | yes | 159 | 26.3% | 1.38 | none |
| text | 11 | 133 | 254.3 | yes | 119.0 | 22.2% | 1.91 | **divergence** |
| video | 3 | 228 | 270.3 | no | n/a | n/a | n/a | too small to rank |
| album | 1 | 144 | 144 | no | n/a | n/a | n/a | too small to rank |
| link | 2 | 12.0 | 12.0 | no | n/a | n/a | n/a | too small to rank |

**Ranked by median: photo (164.5) beats text (133).** Ranked by mean instead, text (254.3) would beat photo (226.4). The two rankings disagree, and one post explains most of it: Author A's Friday check-in text post at 621 engagements, the corpus's top post, sits inside the 11-post text bucket and pulls its mean well above its median. The median ranking ships.

**The overlap check, run per rubric.md section 2 step 7.** Both of this group's 2 link posts are the same 2 posts flagged as promo-marked in Step 4 below (Author C's "virtual organizing service" post at 14, and Author D's affiliate post at 10). Link's median of 12.0 is not a "links underperform in this group" finding. It is a "these two specific promotional posts underperformed" finding, and they both happen to be links. A group capture with more, non-promotional link posts could rank link very differently.

**Video is the most interesting unranked line.** At n=3, median 228, it is the highest median of any type in the file, rankable or not, and it clears the whole-corpus median (144) by 1.58x. Too small to rank. Worth testing, and it is what Draft 3 in Step 6 tests.

---

## Step 3: Group norms

### 3.1 Length

Word counts, all 25 posts, sorted: 12, 17, 18, 19, 20, 20, 20, 20, 21, 22, 22, 23, 23, 24, 25, 26, 26, 26, 26, 30, 31, 36, 36, 37, 39. Median: 23.

| Band | n | Median | Mean | Rankable? | Concentration flags |
|---|---|---|---|---|---|
| 0-19 words | 4 | 92.0 | 95.8 | no | too small to rank |
| 20-29 words | 15 | 133 | 200.1 | yes | divergence (1.50) |
| 30+ words | 6 | 423.0 | 367.0 | yes | none |

**The 30+ band is the cleanest signal in the whole capture: 2.9 times the group median, 6 posts, zero concentration flags.** But the author check that Section 4 requires applies here directly. The 6 posts in this band: Author A (609, 477), Author B (369, 483), Author E (105), Author F (159). Four of the six belong to the two recurring high performers named in Step 4. The other two, 105 and 159, sit far below the band's own median of 423. **The honest claim is "long posts do well here, and they do especially well when a proven poster writes one," not "long posts win" as a standalone effect.**

### 3.2 Tone

**First-person, tested as a presence match anywhere in `Content` for `I, I'm, I've, I'll, my, me, we, we're, we've, our`:**

| Bucket | n | Share | Median | Rankable? | Concentration flags |
|---|---|---|---|---|---|
| First-person | 19 | 76.0% | 159 | yes | divergence (1.58) |
| Not first-person | 6 | 24.0% | 128.0 | yes | none |

Both buckets clear the 5-post floor, so this is a checked comparison, not a directional one. First-person posts out-median the rest, 159 against 128, a real 1.24x gap. The first-person bucket carries one concentration flag (divergence). The not-first-person bucket comes back clean on all three parts (mean/median 1.06, top post 28.1 percent of the bucket, median moves 12.5 percent with the top post removed), so its side of the comparison needs no caveat.

**Question marks, tested as presence of `?` anywhere in `Content`:**

| Bucket | n | Share | Median | Rankable? | Concentration flags |
|---|---|---|---|---|---|
| Contains `?` | 5 | 20.0% | 133 | technically yes at n=5 | **top-share (40.9%) and divergence (2.29): two flags** |
| No `?` | 20 | 80.0% | 151.5 | yes | none |

**Two flags on the question-mark bucket means it does not become a recommendation, per `references/foundations.md` section 4.** Its top post's share alone is 40.9 percent, and 2 of its 5 posts, at 609 and 621 engagement, are the group's two highest-engagement posts overall, and both are Author A's. Meanwhile the no-question-mark bucket is clean at n=20 and its median, 151.5, is actually higher than the question bucket's 133. **This group does not reward question hooks as a device. It rewards one author who happens to open with them.** Reporting "ask questions" as a norm here would have been exactly backwards.

### 3.3 Promo tolerance

**Marker list checked, case-insensitive, anywhere in `Content`:** `affiliate, % off, percent off, discount, link in my profile, link in bio, dm me, spots open, book a, discovery call, virtual organizing service, my service, rates`.

**False-positive risk, stated before the numbers:** this list will miss a promotional post that avoids all of this language (a bare "check my profile" with no other marker), and it can flag a genuine post that happens to use one of the phrases for an unrelated reason. On this file it did not produce a false positive: all 3 flagged posts read as promotional on inspection. That will not be true of every group.

| Bucket | n | Share | Median | Rankable? | Concentration flags |
|---|---|---|---|---|---|
| Promo-marked | 3 | 12.0% | 14 | no | not checked, below floor |
| Not promo-marked | 22 | 88.0% | 164.5 | yes | divergence (1.53) |
| Whole group | 25 | 100% | 144 | n/a | n/a |

The 3 flagged posts: Author C's "virtual organizing service" link post (14 engagements), Author D's affiliate bin-set link post (10), and Author C's "free discovery call" text post (26). Too small to rank, but a median of 14 against the group's median of 144 is an 11-times gap. Reported as too small to rank, worth testing, same as any other under-floor bucket, and the direction is stark enough to say so plainly.

---

## Step 4: Recurring high performers via `Author`

Two of 12 authors clear the 3-post floor.

| | n | Median | Mean | Median after top removed | Top share | Mean/median | Flags |
|---|---|---|---|---|---|---|---|
| Author A | 3 | 609 | 569.0 | 543.0 | 36.4% | 0.93 | none |
| Author B | 3 | 460 | 437.3 | 414.5 | 36.8% | 0.95 | none |

Both clean, both well above the group median of 144, neither carried by a single lucky post.

**Anonymized per rubric.md section 4, point 4: Author A (higher median) and Author B, in descending order of median engagement.**

**Author A's mechanical pattern.** All 3 posts open with a direct question aimed at the group ("What is the ONE zone you are attacking this week?", "Who did the thing they said they would do on Wednesday?") and explicitly grant permission for an incomplete answer in the next line or two ("No judgment thread", "'I did not' is a complete and welcome answer"). This is a repeated thread format, not three unrelated posts. It is also the entire explanation for the question-mark bucket's inflated look in Step 3.2: Author A supplies 2 of the group's 5 question-mark posts, and they are the group's 2 highest-engagement posts overall.

**Author B's mechanical pattern.** All 3 posts reference a prior post or prior group advice before showing a result ("after the closet post," "the thing everyone here told me to do"), written first person, past tense, closing on a concrete count (bags out, minutes taken, "no drilling, we rent"). A callback-and-result structure, distinct from Author A's open-question structure.

**What this section does not claim.** 6 of 25 posts belong to these two authors. That is real evidence for two specific mechanisms, not a majority pattern for the group. The mechanism, not the person, is what Draft 2 in Step 6 borrows.

---

## Step 5: Day-of-week, reused from `best-time-to-post-reader`

Method, floors, concentration check, and format-confound check reused by reference from `../../best-time-to-post-reader/references/rubric.md` section 5, per this skill's `rubric.md` section 5. Day-of-week only: a 25-post capture split across 12 authors has nowhere near the volume for a 28-cell day-by-time grid, and this skill does not run one for any group.

| Day | n | Median | Mean | Rankable? | Concentration flags | Format confound |
|---|---|---|---|---|---|---|
| Wednesday | 6 | 326.0 | 342.3 | yes | none | **video flagged** |
| Monday | 4 | 151.5 | 149.0 | no | too small to rank | not checked |
| Saturday | 4 | 78.5 | 197.0 | no | too small to rank | not checked |
| Friday | 4 | 92.0 | 171.8 | no | too small to rank | not checked |
| Sunday | 3 | 369.0 | 328.3 | no | too small to rank | not checked |
| Tuesday | 2 | 126.0 | 126.0 | no | too small to rank | not checked |
| Thursday | 2 | 112.5 | 112.5 | no | too small to rank | not checked |

**Only Wednesday clears the floor**, at 2.26 times the group's overall median. Its concentration check is clean. **Its format-confound check is not.** Wednesday's 6 posts break down: text 3, video 2, photo 1. Video's `rep_ratio = (2/6) / (3/25) = 0.333 / 0.12 = 2.78`, well over the 1.5 line. Video is also the group's highest-median type corpus-wide at 228, `type_median_ratio = 228 / 144 = 1.58`, over the 1.2 line. Both conditions clear: **confound flagged.** Text, Wednesday's most common type there, does not fire (`rep_ratio` 1.14, and text's own `type_median_ratio` is 0.92, under the line regardless). Photo does not fire either (`rep_ratio` 0.52).

**The sentence this earns:** "Wednesday's median is real and its own concentration check is clean, but 2 of its 6 posts are video, this group's single strongest format, at nearly 3 times video's normal share of a Wednesday post. Some of Wednesday's edge may be a video effect wearing a day costume, not purely a day effect."

**Monday is worth naming though unranked:** n=4, one post short of the floor, median 151.5, close to the group median. Listed, not ranked.

---

## Step 6: Three drafted posts

**Norms actually confirmed, going into the drafts:** photo ranks cleanly as the top type (Step 2); the 30+ word band is clean, though leaning on the two proven authors (Step 3.1); first-person tone shows a real, modest lean (Step 3.2, one flag); question marks are excluded, they are Author A's mechanism, not a group norm (Step 3.2); video is unranked but has the highest median of any type (Step 2); Wednesday is the one rankable day, with a confound caveat attached (Step 5).

**Draft 1, the highest-confidence norm draft: photo, 30+ words, first-person.**

> I finally tackled the garage shelf I have been avoiding since spring. Pulled everything down, kept twelve items, donated the rest, and labeled three bins by season instead of by category. Forty minutes, one trip to donation, and I can see the floor for the first time this year.

**Satisfies:** type (photo, Step 2's cleanest rankable type, no concentration flags), length (49 words, inside the clean 30+ band from Step 3.1), tone (first-person throughout, the confirmed lean from Step 3.2).

**Draft 2, modeled on Author A's mechanism, not their identity.**

> What is the one shelf in your house you keep meaning to fix and keep walking past? The one in my house is the hallway linen closet. No shame thread, "I have not touched it since March" is a completely fine answer today.

**Satisfies:** borrows Author A's proven mechanism from Step 4, a direct opening question plus explicit permission for an incomplete answer. This is stated as a single proven author's format, not the group's question-mark norm, because Step 3.2 excluded question marks as a group-wide finding. Length lands at 43 words, inside the 30+ band. Tone is first-person.

**Draft 3, a test of video, not a repeat of a confirmed finding.**

> Two minute walk through the mudroom cubby system I rebuilt this weekend. Nothing fancy, four hooks, one bin per kid, and the shoes finally live in one place instead of by the door, the stairs, and the car. Filmed on my phone, no editing, just the after.

**Satisfies:** tests video, Step 2's highest-median type in the file (228) that is too small to rank at n=3. Not a repeat of the proven photo finding; explicitly a test. Length still lands inside the clean 30+ band, and tone stays first-person, so the draft only varies the one thing actually being tested.

---

## Step 7: A pass through the wider taxonomy (`group-norms-taxonomy.md`)

`rubric.md` sections 3 and 4 measure the four norms this skill reports on every run. The other 20 norms in `group-norms-taxonomy.md` are checked here, by taxonomy number, against this same 25-post fixture, to show the file actually gets read rather than cited and ignored.

**Norm 6, Direct-question comment bait, gated by trust: FIRES.** This is the taxonomy's own worked example. The question-mark bucket (Step 3.2 above) technically clears the 5-post floor at n=5 but carries two concentration flags, and 2 of its 5 posts, both Author A's, are the group's 2 highest-engagement posts overall. The taxonomy's call is confirmed by the rubric's own concentration check, not just asserted: questions work for Author A specifically, not for the room generally.

**Norm 10, Admin or moderator tagging etiquette: FIRES.** Author D's affiliate bin-set link post closes with "Mods, let me know if this is not allowed" and is also the single lowest-engagement post in the 25-post capture (10 engagements). Keyword match on `mod` confirms one instance in the file, exactly the case the taxonomy names.

**Norm 15, External link tolerance, beyond promotion: NOT MEASURABLE on this fixture.** Both of this group's 2 link posts are also promo-marked (Step 4 above), so there is no non-promotional link post left to check once the promo overlap is separated out. The taxonomy names this exact limitation; this run confirms it rather than guessing at an answer the data cannot give.

**Norm 14, Hashtag absence: checked, zero found.** A regex scan of all 25 `Content` fields for `#word` tokens finds zero hashtag posts. This is a text-only, hashtag-free room, consistent with a general-interest declutter group rather than a platform where hashtag discovery matters.

**Norm 13, Emoji density: checked, zero found.** Counting emoji-range characters across all 25 posts and dividing by the 619-word corpus word count gives a rate of 0.0 per 100 words. This group's posts carry no emoji at all in this capture; a post arriving dense with them would be a real departure from what is here, not a neutral choice.

**Norm 22, Comment-versus-reaction balance: checked.** Corpus-wide `comment_ratio = Comments / (Reactions + Comments + Shares) = 1,550 / 5,587 = 27.7 percent`. Comments make up over a quarter of all engagement in this group, which reads as a discussion room, not a pure broadcast room where reactions would dominate.

**The rest of the 24 (1 through 5, 7 through 9, 11 through 12, 16 through 21, 23 through 24) were not run this pass.** Several need a human read rather than a mechanical marker (location tagging, cross-post detection), and the point of this step is to show the taxonomy gets used where it applies cleanly, not to force every norm onto one 25-post file whether or not it fits.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable. Part 1 was the working.

---

> **Lite mode.** This group capture has 25 posts across 43 days. Below 40 posts or 60 days this analysis runs shallow on purpose: only 2 of 5 post types clear the ranking floor, only 2 of 3 length bands clear it, only 1 of 7 days clears it, and only 2 authors clear the repeat-poster floor. To get a fuller type ranking, more rankable days, and more author patterns, capture about 40 to 60 posts from this group.

# Group analysis: The Declutter Community

25 posts, 2026-05-20 to 2026-07-01, 43 days, 12 distinct authors. This group's export carries no media columns, so this analysis is text and engagement only.

Median engagement across the group: 144. Engagement here means reactions plus comments plus shares.

---

## What wins in this group

| Type | Posts | Median engagement | Mean engagement | Concentration flags | Best example, verbatim |
|---|---|---|---|---|---|
| Photo | 8 | 164.5 | 226.4 | none | "Chest freezer, done. 14 items expired in 2023..." (477) |
| Text | 11 | 133 | 254.3 | divergence, mean is 1.91x the median | "Friday check in. Who did the thing they said they would do on Wednesday?..." (621) |

**Ranked by median, photo beats text.** Ranked by mean instead, text would win, because one post, a 621-engagement check-in thread, pulls the 11-post text bucket's average up without moving its median much. The median ranking is the one above.

**Too small to rank, listed because they matter:** Video (3 posts, median 228), Album (1 post, median 144), Link (2 posts, median 12.0). **Video's median is the highest of any type in this capture**, rankable or not, at 1.58 times the group median. Three posts is not a measurement, but it is the clearest thing worth testing here. **Link's low median is not a "links don't work" finding.** Both of this group's link posts are also the group's only promo-marked link posts, covered below. The type and the promo flag are the same two posts, not two separate signals.

---

## The group's norms

**Length.** Median post: 23 words.

| Band | Posts | Median | Rankable? |
|---|---|---|---|
| 0-19 words | 4 | 92.0 | no |
| 20-29 words | 15 | 133 | yes |
| 30+ words | 6 | 423.0 | yes, no concentration flags |

**The 30+ word band is the cleanest number in this whole analysis: 2.9 times the group median, on 6 posts, with a clean concentration check.** Read it with one caveat: 4 of those 6 posts belong to the group's two proven repeat posters, covered below. The honest version is "longer posts do well here, especially from someone who has already proven their format," not "write long and you win" on its own.

**Tone.** First-person posts (mentioning "I," "my," "we," or similar anywhere in the post): 76.0 percent of the capture, 19 of 25, median 159, one concentration flag (divergence). Posts without first-person language: 6 posts, median 128, clean, no concentration flags. Both buckets clear the ranking floor, so this is a checked comparison: first-person posts genuinely out-earn the rest here, 159 against 128, a real 1.24x gap.

**Question-mark posts: 20.0 percent of the capture, 5 of 25, median 133, but this one does not clear as a norm.** Its top post alone is 40.9 percent of the bucket's total engagement, and 2 of its 5 posts are the group's 2 highest-engagement posts overall, both from the same author. The 20 posts without a question mark are clean and actually score higher, median 151.5. **This group does not reward questions as a device. One author's questions work, because of who is asking, not because of the question mark.**

**Promo tolerance.** Marker list checked: affiliate, percent off, discount, link in my profile, link in bio, dm me, spots open, book a, discovery call, virtual organizing service, my service, rates. This is a language heuristic, because PostSnag captures no promotional flag anywhere: it will miss a pitch that avoids this language and can flag a genuine post that happens to use one of these words for an unrelated reason. Promo-marked posts here: 3, 12.0 percent of the capture, median 14, too small to rank. Not promo-marked: 22 posts, median 164.5. That is an 11-times gap between the two, on 3 posts, worth testing before you post anything promotional here, not worth treating as a rule.

---

## Who wins repeatedly (anonymized)

**Author A | 3 posts, median 609, no concentration flags**

Opens every post with a direct question to the group ("What is the ONE zone you are attacking this week?") and explicitly grants permission for an incomplete answer in the next line or two ("No judgment thread," "'I did not' is a complete and welcome answer"). This is the group's highest-median repeat poster and the entire reason the question-mark tone read looked stronger than it is: 2 of this author's 3 posts are the group's 2 highest-engagement posts overall.

**Author B | 3 posts, median 460, no concentration flags**

Opens by referencing a prior post or prior group advice ("after the closet post," "the thing everyone here told me to do") before showing a first-person result, closing on a concrete count: bags out, minutes taken, a detail like "no drilling, we rent." A callback-and-result structure, distinct from Author A's open-question format.

Only these two authors in this capture posted 3 or more times. That is 6 of 25 posts, real evidence for two specific mechanisms, not a majority pattern.

---

## Best days to post

Day-of-week only. A group capture this size, split across 12 authors, does not carry the volume for a day-by-time grid, and this skill never runs one for a group. Method reused from `best-time-to-post-reader`. `Posted`'s timezone is not stated anywhere in this export, so read Wednesday's edge as relative, not as a specific clock hour to post at.

| Day | Posts | Median engagement | Rankable? | Concentration flags | Format confound |
|---|---|---|---|---|---|
| Wednesday | 6 | 326.0 | yes | none | video flagged |
| Monday | 4 | 151.5 | no | too small to rank | not checked |
| Sunday | 3 | 369.0 | no | too small to rank | not checked |
| Saturday | 4 | 78.5 | no | too small to rank | not checked |
| Friday | 4 | 92.0 | no | too small to rank | not checked |
| Tuesday | 2 | 126.0 | no | too small to rank | not checked |
| Thursday | 2 | 112.5 | no | too small to rank | not checked |

**Wednesday is the only day that clears the floor, at 2.26 times the group median, and its own concentration check is clean.** But 2 of its 6 posts are video, this group's strongest format overall, at nearly 3 times video's normal share of a Wednesday post. Some of Wednesday's edge may be a video effect wearing a day costume, not purely a day effect. Test Wednesday, and test it with more than one format before crediting the day alone.

Monday sits one post short of the floor at a median of 151.5, close to the group median. Too small to rank, worth testing.

---

## 3 posts drafted for this group

**1. The highest-confidence norm draft**

> I finally tackled the garage shelf I have been avoiding since spring. Pulled everything down, kept twelve items, donated the rest, and labeled three bins by season instead of by category. Forty minutes, one trip to donation, and I can see the floor for the first time this year.

**Satisfies:** photo type (this group's cleanest rankable type, no concentration flags), 30+ word length band (clean, no flags), first-person tone (the confirmed lean).

**2. Modeled on Author A's mechanism, not their identity**

> What is the one shelf in your house you keep meaning to fix and keep walking past? The one in my house is the hallway linen closet. No shame thread, "I have not touched it since March" is a completely fine answer today.

**Satisfies:** Author A's proven mechanism, a direct opening question plus explicit permission for an incomplete answer, borrowed as a format, not a claim that questions win group-wide (they do not, see the norms section above). 30+ word band, first-person tone.

**3. A test of video, not a repeat of a confirmed finding**

> Two minute walk through the mudroom cubby system I rebuilt this weekend. Nothing fancy, four hooks, one bin per kid, and the shoes finally live in one place instead of by the door, the stairs, and the car. Filmed on my phone, no editing, just the after.

**Satisfies:** tests video, the highest-median type in this capture (228) that is too small to rank at 3 posts. This is explicitly a test, not a repeat of the photo finding. Still uses the clean 30+ word band and the confirmed first-person lean, so only the format is being tested, not everything at once.

---

## What this analysis is standing on

Analyzed 25 posts from 12 authors, captured 2026-05-20 to 2026-07-01, 43 days. Rankings use median engagement, reactions plus comments plus shares, unweighted. Buckets under 5 posts are listed but not ranked: video, album, and link post types; the 0-19 word length band; the promo-marked bucket; 6 of the 7 days of the week. The text type and the first-person tone bucket each carry a divergence flag (one or two posts pulling the mean well above the median). The 30+ word length band, the not-first-person tone bucket, and Wednesday all cleared the ranking floor and passed their concentration checks clean. Wednesday's format-confound check flagged video as over-represented and itself strong, so its median carries that caveat.

Promo-marker detection is a language heuristic, not a captured field. It will miss posts that avoid its marker list and can flag genuine posts that happen to use a marker phrase. Read the flagged posts before treating the list as a verdict.

Not in this export, so not in this analysis: sponsored or paid-partnership flags. Per-emoji reactions. Comment text. Reach or impressions.

This group's export carries no media columns, so nothing here describes an image or a video's content, only its engagement.

PostSnag captures what you scrolled, so this describes the posts in this export, not the group's full archive.

Analysis based on 25 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-group-post-analyzer
