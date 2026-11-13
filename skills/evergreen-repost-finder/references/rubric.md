# rubric.md

The full method for Evergreen Repost Finder. Written so an agent with no other context can execute it and reach the same shortlist as anyone else running it on the same file.

Version 1.0 | 2026-08-04

---

## Section 0: What this rubric is adapting, and why organically

The idea this skill is built on comes from paid ads: the longest-running ad in an account is the ad that is still making money, because nobody keeps spending on a loser. There is no spend signal in an organic Facebook export, so this rubric builds the organic equivalent out of what the export actually has: does a post's own audience still beat expectations when you correct for when it was posted, and has enough time passed that reposting it would not just be showing the same people the same thing twice.

Two different questions, both required, neither one enough on its own:

1. **Did it work, corrected for its moment?** Answered by era-adjusted scoring, section 1.
2. **Has it aged out of memory and stayed true?** Answered by the evergreen filter and the reuse-safety age gate, sections 2 and 3.

A post that scores well but is 20 days old is not evergreen, it is recent. A post that is a year old but built on a claim that expired months ago is not evergreen either, it is stale. This skill only recommends posts that clear both bars.

---

## Section 1: Era-adjusted scoring

**Compute every number in this analysis with code.** This section's era-adjusted scores, the corpus-median fallback, and every worked example below follow that rule; a wrong number presented with confidence is worse than no number.

**Use the exact method in `_shared/engagement-math.md` section 7. This rubric does not redefine it.**

Restated for this skill's context, with the boundary rule spelled out because reposting decisions live disproportionately at the edges of a file:

1. Sort all posts ascending by parsed `Posted`. Index them `0 .. N-1`.
2. For the post at index `i`, take its **10 nearest neighbors by index**, excluding itself. Normally `i-5 .. i+5` minus `i`.
3. **At the edges, extend one-sided so the neighbor count is always exactly 10.** Post `0` uses indices `1` through `10`. Post `N-1` uses indices `N-11` through `N-2`. This is not a special case you invent, it is the rule stated in `engagement-math.md` section 7, and it is worth verifying with a count, not an assumption: if a post's neighbor list does not have exactly 10 members, the code is wrong, not the data.
4. `era_median` = the median engagement of those 10 neighbors.
5. `era_score = post_engagement / era_median`, reported to two decimals.

**Preconditions, all three, checked before any era score is computed:**

- `N >= 21`
- `span_days >= 90`
- Not in lite mode. **The lite-mode trigger, stated here rather than only cited:** `LITE MODE if posts_analyzed < 40 OR span_days < 60` (`references/foundations.md` section 5, condensed from `_shared/engagement-math.md` section 6, full version in the bundle).

If any precondition fails, do not compute era scores at all. Use `post_engagement / corpus_median` instead, call it a **multiple of the corpus median**, and never call it an era score. This is the exact substitution `engagement-math.md` section 7 specifies, and it is the path every free-tier run takes, because a free export is always under 40 posts and therefore always in lite mode.

### Worked boundary math, three posts in full, on the shared synthetic file

`profile-maya-torres.csv`: N=60, span 130 days. Full-mode preconditions all hold. Sorted ascending by `Posted`, indexed `0..59`.

**Post at index 0 (2026-03-21, engagement 246), the low edge of the file.**

Neighbor indices: `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]` (extended one-sided per the edge rule, since index 0 has nothing below it).

Neighbor engagements, in index order: `388, 312, 302, 291, 488, 688, 341, 610, 244, 268`
Sorted for the median: `244, 268, 291, 302, 312, 341, 388, 488, 610, 688`
`era_median = (312 + 341) / 2 = 326.5`
`era_score = 246 / 326.5 = 0.7534` -> **0.75**

**Post at index 20 (2026-05-07, engagement 4,118), an interior post and the highest score in the file.**

Neighbor indices: `[15, 16, 17, 18, 19, 21, 22, 23, 24, 25]` (a clean two-sided window, this post is nowhere near either edge).

Neighbor engagements, in index order: `470, 402, 615, 152, 214, 702, 420, 980, 402, 455`
Sorted for the median: `152, 214, 402, 402, 420, 455, 470, 615, 702, 980`
`era_median = (420 + 455) / 2 = 437.5`
`era_score = 4118 / 437.5 = 9.4126` -> **9.41**

**Post at index 59 (2026-07-28, engagement 902), the high edge of the file.**

Neighbor indices: `[49, 50, 51, 52, 53, 54, 55, 56, 57, 58]` (extended one-sided per the edge rule, since index 59 has nothing above it).

Neighbor engagements, in index order: `305, 355, 398, 1402, 566, 388, 1206, 560, 208, 238`
Sorted for the median: `208, 238, 305, 355, 388, 398, 560, 566, 1206, 1402`
`era_median = (388 + 398) / 2 = 393.0`
`era_score = 902 / 393.0 = 2.2952` -> **2.30**

**Why show the edges deliberately.** A rolling window that silently shrank at the edges (using only 5 or 6 neighbors instead of 10) would understate the sample at exactly the posts most likely to be old enough to repost. The one-sided extension keeps every score built on the same 10-post evidence base, from the very first post in the file to the very last.

---

## Section 2: The evergreen filter

Every shortlist candidate gets exactly one of four classifications. Run the tests in order; the first one that fires wins.

### 2.1 The test that separates a story's time anchor from a currency claim

Before applying any marker below, ask this question of every time-flavored phrase found in a post's hook or body:

> **Does this phrase assert something true AT PUBLISH TIME that could be false or misleading AT REPOST TIME?**

If yes, it is a dated-language marker. If no, either it is a narrative detail describing something that already happened (a weekday inside a first-person past-tense story, a specific year inside a personal-history detail) or it is a generic instruction the reader applies to their own current moment (a bin category described as "for this week" that means "whatever week you are reading this in," not "the week of 2026-05-07"). Neither of those changes truth value on repost, so neither one is a marker.

Two real examples from the shared synthetic file, worked to show the test firing both ways on similar-looking language:

- **Not a marker.** `I opened a client's coat closet last Tuesday and a sled fell on me. A sled. In May.` (post 2026-04-04, era score 2.11). "Last Tuesday" and "In May" describe when the scene happened. Reposted in November, the sentence is still exactly as true as it was in April, because it is recounting an event, not asserting a current state.
- **A marker.** `2 shelves, 6 categories, zero rearranging since March.` (post 2026-07-16, era score 0.64, not itself a winner but shown here because it is the clean example of the failure mode). "Since March" is a currency claim: it is true because of how much time has passed since the post's own publish date, and it is either false or requires a rewrite the moment that arithmetic changes. Reposted unchanged, the reader has no way to know if it is still accurate.

### 2.2 The marker list

**Category A: currency-anchor phrases, own-timeline claims. Any one marker is sufficient to flag DATED.**

| Marker | Example (real, from the file) |
|---|---|
| `"since {month or year}"` describing the author's own streak or claim | `"zero rearranging since March"` (2026-07-16) |
| A near-term deadline word paired with a weekday, aimed at the reader's calendar | `"read this before Sunday"` (2026-05-23, hook line) |
| `"this week" / "this month" / "this year"` when the subject is the author's own current state or an implied deadline, not a generic reader-facing category label | none in this file: hypothetical, `"this month's decluttering challenge closes Friday"` |
| `"as of {time}" / "currently" / "right now" / "these days"` applied to a fact that can change | none in this file: hypothetical, `"the return window is currently 30 days"` |

Apply the test in 2.1 before flagging: `"shoes that get worn this week"` (2026-04-30, inside a bin description) is NOT this marker, because it instructs the reader to apply the label to whatever week they are reading in, not to a specific week in Maya's calendar.

**Category B: explicit year or version references used as currency claims. Any one marker is sufficient to flag DATED.**

| Marker | Example |
|---|---|
| A bare calendar year attached to "current," "new," "latest," "this year's" | none in this file: hypothetical, `"this year's back-to-school storage checklist"` |
| A product or app version number, release name, or "the new X" phrasing | none in this file: hypothetical, `"the new closet app just added a feature that changes this"` |

Apply the test in 2.1: `"a bag of flour her mother bought her in 2019"` (2026-05-07, inside a client story) is NOT this marker. It is a personal-history detail. The sentence's truth does not depend on today's date; it happened in 2019 and will always have happened in 2019. Same for `"a phone charger for a phone I have not owned since 2019"` (2026-07-28): a joke about a specific long-held possession, not a claim that depends on being read soon after posting.

**Category C: named live events. Any one marker is sufficient to flag DATED.**

| Marker | Example |
|---|---|
| A named sale, launch, or one-time event used as the reason to act now | none in this file: hypothetical, `"our Black Friday organizing bundle"`, `"the sale ends Friday"` |

**Category D: seasonal topic reference. This is NOT a DATED marker. It is its own class, section 2.3.**

The post's subject is a season or holiday, described generally, with no currency claim layered on top: `"packing away winter coats"`, `"holiday decor storage"`, `"back-to-school bins"`. None of the 60 posts in the shared synthetic file are seasonal by subject; this dataset happens not to exercise the class. The mechanism is defined here anyway, because a real capture will hit it.

### 2.3 Classification precedence

Run in this order. First match wins.

```
1. If a Category A, B, or C marker is found INSIDE THE BODY (not just the hook):
   -> DATED-BODY, EXCLUDED. The core claim, not just the opening line, needs
      a factual update. A hook swap cannot fix this. The post is removed from
      the shortlist entirely and named in the honesty footer as excluded for
      a dated body claim.

2. Else if a Category A, B, or C marker is found ONLY IN THE HOOK (the body
   is clean):
   -> DATED-HOOK-ONLY. The post stays eligible. It is a candidate for the
      dated-hook remake trigger in section 4.1, because the body's claim
      still holds and only the opening line needs replacing.

3. Else if the post's subject is a season or holiday per the Category D test:
   -> SEASONAL EVERGREEN. Name the season and the repost window: the same
      season next year, not any time of year.

4. Else:
   -> CLEAN EVERGREEN. No dated language anywhere, no seasonal dependency.
```

**Hook extraction uses the identical procedure as `references/hook-archetypes.md` section 1** (condensed from `facebook-hook-analyzer/references/rubric.md` section 1; full version in the bundle): the first substantive sentence of `Content`, after the CTA and chrome skip tests. This skill does not redefine hook extraction; two skills disagreeing about what counts as a hook on the same file would be a worse outcome than picking one procedure and citing it.

---

## Section 3: The reuse-safety age gate

**Working number: 90 days (3 months).** Deliberately the same 90-day figure `engagement-math.md` section 7 already uses to unlock era-adjusted scoring, which is not a coincidence: 90 days is roughly how long it takes a post to both earn a real era-adjusted comparison on the way in, and to have cycled out of an audience's recent feed memory on the way out. This is a working number, not a platform fact about Facebook's algorithm or attention span, and the output says so.

```
age_days = (today's date) - (post's Posted date), in whole days
reuse_safe = age_days >= 90
```

**A post below the gate never enters the shortlist, regardless of score.** It goes on the watch list instead, with `clears_on = Posted date + 90 days` computed and stated exactly, so the user knows precisely when to check back rather than being told "wait a while."

**Worked boundary, from the shared file.** The single highest-scoring post in the whole file, `A client cried in her own pantry on Monday...` (2026-05-07, era score 9.41), is 89 days old against a reference date of 2026-08-04. It needs exactly one more day. This is the sharpest illustration in this rubric that the gate is not decorative: the best post in the file, by a wide margin, is withheld for a single day, and the shortlist says so rather than quietly excluding it with no explanation.

**Per-post detail checklist**, for a user who wants to sanity-check one specific post by hand: `references/reuse-safety-checklist.md`.

---

## Section 4: The repost-as-is versus remake decision rule

A post reaches this section only after clearing three gates: it is CLEAN EVERGREEN, SEASONAL EVERGREEN, or DATED-HOOK-ONLY (section 2), it is reuse-safe (section 3), and its score, era-adjusted or corpus-median multiple, is **at least 1.5x** (this skill's working recommend floor, the same shape of number as the divergence flag in `engagement-math.md` section 3, chosen so a repost is recommended only when a post clearly beat its own moment, not merely matched it). **This comparator, and every comparator in this rubric, is applied to the raw score, never the rounded two-decimal display value (R1).** A score that displays as 1.50 but is 1.4964 before rounding does not clear the floor.

**A DATED-HOOK-ONLY post that clears all three gates is remake-only.** Its own classification from section 2.3 already says its hook needs replacing before it goes back out, so trigger A below fires on it automatically and REPOST AS-IS is never an available outcome for it, regardless of what the other two triggers find.

Once a post clears all three gates, check it against three mechanical triggers, in order. **Any one trigger that fires moves the post from REPOST AS-IS to REMAKE**, except a DATED-HOOK-ONLY post, which enters this check already in REMAKE via trigger A. Report every trigger that fires, not just the first, because a post can be both dated in the hook and in the weaker format at the same time, and hiding the second reason behind the first is exactly the "one flags column" failure this catalog has already been corrected on once.

### 4.1 Trigger A: dated hook, evergreen body

**Fires if the post's classification from section 2.3 is DATED-HOOK-ONLY.**

The body's claim is still true. Only the opening line needs replacing. This is the cheapest kind of remake: keep everything, swap the hook.

**Worked illustration, since neither of this file's two DATED-HOOK-ONLY posts clears both the score floor and the age gate.** DATED-HOOK-ONLY posts are entry-eligible for this section, as remake-only candidates, per the entry gate above. On this file specifically, idx 50 (era score 0.64, age 19 days) and idx 27 (era score 0.43, age 73 days) both fail the score floor and the age gate, so the trigger still does not fire on an actual shortlisted post here. That absence is a fact about this particular dataset, not a claim that the trigger cannot fire. Shown here on a real post that fails a different gate, so the mechanism is demonstrated honestly rather than illustrated on the nearest available case: `2 shelves, 6 categories, zero rearranging since March.` (2026-07-16, era-adjusted score 0.64, well below the 1.5x floor, and only 19 days old). It is not a shortlist candidate on either score or age. It is shown purely so the classification-into-remake mechanism has a real worked example: were this post ever to clear both gates, its hook would be swapped for something built from its own body ("Frequency is the only sort that survives real life," which has no date in it) via the fallback source in section 5.2 (the body's own language, or `references/hook-template-mini.md`) while the shelf method stays untouched.

### 4.2 Trigger B: format-upgrade opportunity

**Fires if the post's `Type` median engagement, across the whole corpus, is below the corpus's best RANKABLE type's median by a ratio of 1.3x or more.**

```
best_rankable_type_median = the highest per-Type median among types with n >= 5
                             (the same 5-post per-bucket floor as
                             references/foundations.md section 3)
type_gap = best_rankable_type_median / this_post's_type_median
fires if type_gap >= 1.3
```

**Working number: 1.3x.** Labeled, not discovered. Report the exact ratio, never round it into a vaguer "significantly better."

**Worked on the shared file.** Per-Type medians, rankable types only (`link` has n=4 and is excluded from this comparison, same floor as everywhere else in this catalog):

| Type | n | Median | Rankable? |
|---|---|---|---|
| video | 14 | 585 | yes |
| album | 8 | 393 | yes |
| photo | 17 | 388 | yes |
| text | 17 | 388 | yes |

`video` is the best rankable type at 585. Any shortlisted post whose own type is album, photo, or text clears the 1.3x gap (585/393 = 1.49, 585/388 = 1.51, 585/388 = 1.51). A shortlisted video post never triggers this one, because it is already in the best-performing rankable format.

### 4.3 Trigger C: engagement pattern, concentration-carried win

**Fires if the post's own `Type` bucket has fewer than 5 posts (below the per-bucket floor, so the type itself is never ranked) AND this post's share of that type-bucket's total engagement exceeds 40 percent**, the identical threshold `engagement-math.md` section 5 uses for the concentration check, applied here per-type instead of per-archetype.

```
type_share = this_post's_engagement / sum(engagement of all posts sharing this Type)
fires if the Type's n < 5 AND type_share > 0.40
```

**What it means when it fires.** The win is not evidence that the format works for this creator, because there are not enough posts in that format to say so. It is evidence that this one post worked. Reposting the identical artifact bets on the same result happening twice by coincidence. A remake, the same proven idea in a new hook or a stronger format, tests the idea on its own merits instead.

**Worked illustration, again shown on a post that fails the age gate, since no reuse-safe winner in this file happens to sit in an under-floor type.** The `link` type has n=4, below the floor, total link engagement across the file is 3,236. The post `You do not need more storage. You need fewer decisions.` (2026-07-20, era score 2.99) is 1,402 of that 3,236, a 43.3 percent share, clearing the 40 percent trigger. It is 15 days old, nowhere near the 90-day gate, so it is not a shortlist member. It demonstrates the mechanism: if this post clears the age gate on 2026-10-18, the concentration trigger fires on it and it ships as a remake, a new angle on the same argument (rebuilt per section 5.2 using a different archetype from `references/hook-archetypes.md` section 3's precedence ladder), not a straight repost, because the `link` format has only 4 data points behind it and this post is nearly half of all of them.

### 4.4 Default

**If none of the three triggers fire, the post is REPOST AS-IS.** No refresh needed. The exact original, unchanged, is the recommendation.

---

## Section 5: The refreshed-draft method

Runs once per REMAKE entry. This skill does not invent a second voice-matching system. It reuses the one already built and shipped in `facebook-caption-writer`, because a hook analyzer, a caption writer, and this skill all classifying and voicing hooks by three different rulebooks would give a user three different answers on the same file.

### 5.1 Build the current voice profile, not the original post's own mechanics

**Why this matters and is not just a formality.** A remake modeled on the original post's OWN sentence rhythm and structure reproduces how the creator wrote months ago. The point of a refresh is to sound like the creator writes NOW. Run `../../facebook-caption-writer/references/rubric.md` sections 1 and 2 (condensed locally in `references/caption-mechanics-mini.md`) on the CURRENT top quartile of the same export (the same style-source selection that skill already defines), not on the single post being remade.

Condensed locally rather than requiring a second skill install: `references/caption-mechanics-mini.md` (condensed from `facebook-caption-writer`; full version in `../../facebook-caption-writer/references/rubric.md` and the bundle) carries all 9 mechanics with their measurement rules, one paragraph each:

| Mechanic | What it captures |
|---|---|
| Opening-line pattern | Hook archetype distribution, per `references/hook-archetypes.md` section 2 |
| Sentence-length rhythm | Words per sentence, tight or loose, per the 3.0-word working flag |
| Line-break and whitespace style | Dominant line count and paragraph structure |
| Emoji usage | Count and position, 0 is a real finding |
| CTA placement and phrasing | Platform-mechanic CTAs versus a closing imperative, counted separately |
| Hashtag behavior | Count, repetition, position |
| Capitalization habits | Hook case, ALL-CAPS word count, numerals versus spelled-out numbers |
| Question frequency | Share of hooks ending in a question mark |
| First-versus-second person | Distribution across the style-source set |

Full method: `references/caption-mechanics-mini.md`, or `../../facebook-caption-writer/references/rubric.md` sections 2 and 3 for the uncondensed version.

### 5.2 Apply the fix that matches the trigger that fired

- **Trigger A fired (dated hook):** keep the body exactly as written, it already proved itself. Replace only the hook. Draw the replacement from one of two places: the body's own language via the latent-fit test (`../../facebook-hook-analyzer/references/rubric.md` section 6, not part of this skill's local embeds pack; search the body for a marker the creator already writes but has not led with), or a matching archetype from `references/hook-template-mini.md` (condensed; full 44-template library in `../../facebook-hook-analyzer/references/hook-template-library.md` and the bundle) filled with this post's own specifics. Never a generic hook that would work for any creator.
- **Trigger B fired (format-upgrade):** keep the hook and the core argument. Rebuild the delivery in the stronger format named by the trigger. If the creator has existing posts in that format, model the new structure on `facebook-caption-writer` section 2.3's line-break findings for that format (`references/caption-mechanics-mini.md` mechanic 3, condensed). If they do not, say so plainly: "this creator has no existing {format} posts to model from, so this is a first attempt, not a pattern match."
- **Trigger C fired (concentration-carried win):** keep the underlying idea, rebuild the hook using a different archetype than the original (per `references/hook-archetypes.md` section 3's precedence ladder, condensed from `facebook-hook-analyzer` section 2.13), so the remake tests the idea on a second angle rather than repeating the one post that carried its whole bucket.
- **Multiple triggers fired:** apply each relevant fix. State which triggers drove which specific change.

### 5.3 Run the self-check

Before shipping a refreshed draft, run the applicable items from the 11-item self-check in `references/caption-mechanics-mini.md` (condensed from `facebook-caption-writer/references/rubric.md` section 4; full version in the bundle): word count within the current style-source range, sentence rhythm and hook-line word count within the observed ranges, line count and blank-line placement matching the dominant structure, emoji and hashtag counts matching the profile, CTA behavior matching, capitalization matching, person voice matching, question-mark presence matching, and no literal reuse of the original's exact wording where a fix was applied. If a draft fails 2 or more checks, rewrite it before it ships, per that self-check's own rule. A single narrow miss gets a one-line disclosure instead.

**The 6-word originality guardrail, checked mechanically and separately from the self-check above.** No refreshed draft reuses more than 6 consecutive words from the post it is remaking, or from any other post in the same export. Check it literally, sliding a 7-word window across the refreshed draft against every caption in the export. The template is the structure; the nouns are new. (Working number, labeled: 6 is this catalog's shared drafting threshold, not a platform fact, sourced from `facebook-content-calendar-builder`'s rubric section 4.4. It sits just above the length of a common phrase and just below the length of a distinctive clause.) This is a mechanical backstop on top of the self-check's own "no literal reuse" item, not a replacement for it: the self-check item catches a reused idea in different words, this one catches a reused run of words in the same order.

### 5.4 Always show both

Every remake entry in the output shows the original verbatim, the refreshed draft, and one line naming exactly what changed and why. The user decides. A refresh that cannot be compared against its original is a rewrite pretending to be a fix.

---

## Section 6: Building the shortlist and the watch list

1. **Shortlist** = every post that is CLEAN EVERGREEN, SEASONAL EVERGREEN, or DATED-HOOK-ONLY, reuse-safe (age_days >= 90), and scores >= 1.5x on its raw value, never the rounded display value (R1). Rank by score, descending. **A DATED-HOOK-ONLY post on the shortlist is remake-only**: trigger A (section 4.1) fires on it automatically, and it never appears as REPOST AS-IS.
2. **Ties**, in order: higher age wins (older proof beats newer proof at the same score), then alphabetical by post date, stated as such.
3. **Watch list** = every post that scores >= 1.5x but is not yet reuse-safe. Rank by `clears_on` date, ascending, so the soonest-available post is first. State `clears_on` exactly.
4. **Excluded, named once, not hidden:** any post classified DATED-BODY (section 2.3), regardless of score or age. State the count and, for the highest-scoring excluded post, name it and why, the same way an unrankable archetype gets named rather than silently dropped elsewhere in this catalog.
5. **The shortlist can be, and often will be, short or empty.** That is the correct output on a shallow capture, not a bug to paper over. State the exact number of posts that cleared each gate, in order, so the user can see which gate is the bottleneck. On the shared synthetic file, for example: "60 posts in this export. 58 clear the evergreen filter. 20 of those are old enough. 4 of those 20 also clear the 1.5x score floor and make the shortlist (one more, idx 17, misses the raw-value floor at 1.4964 and is named as a near-miss, not counted). 12 more clear the score floor and the evergreen filter but are still on the clock, listed on the watch list below."

---

## Section 7: What this rubric refuses to do

- **No claim that a post will perform the same way twice.** Era-adjusted score describes what happened the first time, corrected for its moment. It is not a prediction.
- **No sponsored-versus-organic split.** If a shortlisted post was boosted, nothing in the export shows it, and reposting it as organic content carries that same blind spot forward. Said once in the limits, not re-litigated per post.
- **No claim that a DATED-BODY exclusion is permanently disqualified.** It is excluded from THIS run because its claim needs a factual check the skill cannot perform from the export alone. A human who verifies the claim is still true can repost it manually; this skill just will not recommend it unchecked.
- **No fabricated seasonal example presented as if it occurred in the user's own data.** If a real capture has zero seasonal-evergreen posts, the output says zero, the same way this rubric said zero for the shared synthetic file, and the class stays defined for the case that does occur.
- **No repost recommendation below the 90-day gate, no matter how badly a user wants one sooner.** The gate is stated with its exact clearing date, not softened into "soon."
