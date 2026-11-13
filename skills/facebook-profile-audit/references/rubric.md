# rubric.md

The full method for Facebook Profile Audit. Written so an agent with no other context can execute it and reach the same numbers as anyone else running it on the same file.

Version 1.0 | 2026-08-04

---

## Section 0: What this audit is actually doing

A profile audit answers three questions in order: what does this creator post, what of that actually works, and what should you copy. Every section below feeds one of those three questions. None of this is hook analysis (that is Facebook Hook Analyzer's job, scoped to opening lines) and none of it is a two-profile comparison (that is Competitor Content Gap Finder's job). This skill describes one captured profile, once, in full.

**Discipline, non-negotiable:** every finding cites its `n`, its median against the corpus median, and any concentration flag, glued inline. A finding with no number attached is an opinion, and this skill is not in the opinion business past 15 posts.

---

## Section 1: Format distribution

Compute every number in this analysis with code.

**The five real types, and only these five:** `text`, `photo`, `video` (includes reels; there is no separate reel type in the export), `link`, `album`. There is no poll type. If a `Type` value appears that is not one of these five, stop and say which value you saw, because it means the export changed or the file is not a PostSnag export.

**Procedure:**

1. Group all posts by `Type`.
2. For each group: `n`, median engagement, mean engagement, highest post.
3. Split into rankable (`n >= 5`) and unrankable, per `references/foundations.md` section 3 (condensed; full version in the complete bundle). Unrankable formats are listed with their numbers, never given a rank, and never called best or worst. A format used 4 times that outperforms everything else is the same "too small to rank, worth testing" case the hook analyzer's Bold Claim archetype demonstrates: report it, do not hide it.
4. Run the three-part concentration check (`references/foundations.md` section 4) on every rankable format: median after removing its top post, that top post's share of the format's total engagement, and mean over median. Any flag is written inline, in the sentence, next to the number.
5. Compute composition: each format's share of the whole corpus (`n / N`) against its share of the top quartile (`references/foundations.md` section 6). Where the two shares diverge, that is the finding. Where a format is at or near zero share of the top quartile despite real volume, name it as a "does not work" candidate rather than softening it into "may need more variety."

**Worked example, real numbers, from the shared 60-post synthetic file (all instantiated numbers reproduced in `example-run.md`):**

| Type | n | median | mean | share of corpus | share of top 15 | flags |
|---|---|---|---|---|---|---|
| photo | 17 | 388 | 493.4 | 28.3% | 4 of 15 (26.7%) | none |
| text | 17 | 388 | 471.2 | 28.3% | 4 of 15 (26.7%) | none |
| video | 14 | 585 | 1106.4 | 23.3% | 5 of 15 (33.3%) | mean/median 1.89 |
| album | 8 | 393 | 407.6 | 13.3% | 0 of 15 (0.0%) | none |
| link | 4 | 795 | 809 | 6.7% | 2 of 15 (13.3%) | **unrankable, n<5** |

**Reading this table is where the audit starts, not where it ends.** Video carries the highest rankable median (585 against a corpus median of 458.5) and over-indexes in the top quartile, but the mean/median divergence flags: two videos are doing a lot of that work, so the median is the number to trust and the mean is not. Album is the format to question: 13.3 percent of the volume and zero presence in the top 15. Link has the single highest median of any format in the file and is not rankable at n=4, which is the exact shape of the "too small to rank, worth testing" case, not a dismissal.

---

## Section 2: Topic clustering

Facebook exports carry no topic field. Topics have to be extracted from `Content`, mechanically, so two agents running this rubric on the same file land on the same clusters.

### 2.1 The extraction algorithm

This is a **trigger-word noun-phrase extractor**. It does not require a part-of-speech tagger and is exactly reproducible in any runtime that can do regex and string splitting.

**Step 1: split into clauses.** Split `Content` on `. ! ? , ; :` and newlines. Work clause by clause so a noun phrase never runs across a comma or a sentence boundary.

**Step 2: define the trigger set.** A trigger word signals that a noun phrase is about to start:
- Determiners and possessives: `a, an, the, my, your, his, her, their, our, its, this, that, these, those`
- Prepositions: `in, on, at, of, from, into, under, behind, beside, near, inside, outside, about, with, without, by, over, above, below`

**Step 3: extract.** Scan each clause word by word. When a trigger word appears, skip any additional immediately-following trigger words (handles "your own house"), then collect up to 3 following words as the candidate noun phrase, stopping early if you hit another trigger word, a short closed-class word (`is, are, was, were, have, has, had, will, would, can, could, not, and, or, but`, or a pronoun), or the end of the clause. Words under 3 characters are skipped without ending the phrase. Singularize each collected word with a light suffix rule: strip a trailing `s` from words over 4 characters that do not end in `ss`, and convert a trailing `ies` to `y`.

**Step 4: the head.** The **head noun** of a candidate phrase is its **last collected word**. This is what gets clustered on.

**Worked example.** `"You are storing three sizes of clothes for three versions of yourself."` splits into one clause (no internal punctuation). Trigger `of` before `clothes` yields the candidate `(clothe)`, head `clothe`. Trigger `of` before `yourself` does not fire because `yourself` is a pronoun form, not collected. The word `three` is a stopword-listed number and is never itself collected as content, but does not break a phrase already in progress if it appears mid-span.

**Honestly stated:** the stop list in section 2.2 and the singularization rule in step 3 leave room for small cluster-count drift between two independent implementations of this extractor (a discard list edge case, a suffix rule tie). Treat exact head counts as implementation detail; the medians reported per cluster are the stable, comparable check, not the head count itself.

### 2.2 The known limitation, stated plainly

**A noun immediately followed by a verb with no separating stopword mis-heads.** Example, real, from the synthetic file: `"your entryway needs a bench"`. The trigger `your` starts collection, and because `needs` is not on the short-word stop list (it is a verb, not a determiner or auxiliary), the extractor collects `entryway needs`, whose head becomes `need`, not `entryway`. The true topic noun is dropped from its own cluster.

**This is why the discard step below exists.** Do not ship the raw extraction output. Before naming any cluster:

1. **Sanity-check the top 30 heads by post-count.** For each, look at 2 to 3 of its example phrases (the full collected span, not just the head).
2. **Discard heads that are not a physical object, place, or category a reader would recognize on sight.** Verb-shaped heads (`need, work, built, decide, stop, let, give, use, fail, keep`), pronoun-shaped heads (`there, them, home` used generically), and time words (`day, week, month, night`, day names) are discarded outright. They are not topics. A short discard list that catches most of these mechanically: `day, days, week, weeks, month, months, year, years, night, morning, evening` plus the seven day names, plus `work, thing, problem, decision, instead, there, them, home, for`.
3. **Report the discard, once, in one line.** "18 candidate heads were discarded as non-topics (verbs, time words, generic pronouns)." A reader told nothing about this step cannot tell whether it happened.

### 2.3 Clustering heads into named topics

Two heads merge into one named topic **only when they name the same real-world object or an object so tightly bound to it that separating them would be pedantic** (a kitchen counter is furniture that lives in a kitchen; a bin and bins are the same object at two counts). Merges are a manual step the agent performs by reading the surviving heads and their examples, not an automatic fuzzy match. Document every merge you make so the reader can see the rule was applied, not guessed.

**Worked merge table from the synthetic file:**

| Heads merged | Topic name |
|---|---|
| closet | Closets |
| pantry | Pantries |
| garage | Garages |
| shelf | Shelves |
| drawer | Drawers |
| bin, bins | Bins & Containers |
| counter, kitchen | Kitchen & Counters |
| entryway | Entryways |
| kid, child | Kids' Spaces |
| client | Client Stories |
| pile | Paper Piles |
| label, system, limit | Labels & Systems |
| paper, pile | Paper Piles |

**Topics are not exclusive, unlike `Type`.** A single post can mention a closet and a bin in the same caption and belongs to both clusters. Say so once in the output: "a post can appear in more than one topic cluster; unlike format, which is exactly one value per post, topics are additive."

### 2.4 Minimum cluster size and ranking

No new threshold is invented here. **Reuse the shared 5-post floor from `references/foundations.md` section 3** exactly as format buckets and hook archetypes do elsewhere in this catalog. A topic cluster with `n >= 5` gets ranked: median, concentration check, composition. A cluster with `1 <= n <= 4` is listed with its number and median, explicitly not ranked, and called "too small to rank, worth testing" rather than dropped or force-ranked. A cluster with `n = 0` after the merge step simply does not appear.

**Worked ranking, from the synthetic 60-post file:**

| Topic | n | median | rankable? | flags |
|---|---|---|---|---|
| Closets | 10 | 530 | yes | none |
| Labels & Systems | 7 | 402 | yes | top-share 53.1%, mean/median 2.28 |
| Bins & Containers | 5 | 470 | yes | top-share 45.4% |
| Kitchen & Counters | 5 | 462 | yes | none |
| Shelves | 4 | 429 | **no, n<5** | not checked |
| Drawers | 4 | 412 | **no, n<5** | not checked |
| Garages | 4 | 461 | **no, n<5** | not checked |
| Paper Piles | 3 | 388 | **no, n<5** | not checked |
| Pantries | 3 | 712 | **no, n<5** | not checked |
| Client Stories | 2 | 383 | **no, n<5** | not checked |
| Entryways | 1 | 268 | **no, n<5** | not checked |
| Kids' Spaces | 1 | 540 | **no, n<5** | not checked |

**A bimodal cluster is not automatically a flagged one, and Closets is the proof.** Closets spans 208 to 1904 across its 10 posts, its lowest and highest posts both real. Run the concentration check anyway rather than assuming a wide range means a carried median: median-after-removing-the-top-post moves 1.9 percent, the top post is 29.5 percent of the bucket's total, and mean over median is 1.22. All three clear. The median of 530 is a real center, not noise wearing a range.

---

## Section 3: Cadence

Cadence describes **how often and on what rhythm** the creator posts. It does not rank days by performance; that comparison, done properly with the sample floors it needs, is Best Time to Post Reader's job. This skill cites that skill rather than repeating its method.

**Compute:**

1. **Posts per week.** `N / (span_days / 7)`, one decimal.
2. **Gap-day list.** The number of calendar days between each post's date and the next post's date, sorted chronologically. **Use calendar-date subtraction, not a raw datetime subtraction.** A post at 11pm and the next post at 8am the following calendar day are 21 hours apart, and a naive `timedelta.days` on the full timestamps reports that as a 0-day gap, which reads as a same-day double post that never happened. Convert each `Posted` value to its date first, then subtract. Report the median gap, the minimum, and the maximum, and name the dates on either side of the maximum gap (there can be several ties at the max; name one or state the count).
3. **Day-of-week posting counts.** How many posts landed on each day of the week, by count, not by performance. This is a volume description: "you post on Tuesday 12 times and Wednesday once" is a fact about behavior, not a claim about which day works.
4. **Same-day doubling.** If two or more posts share the same calendar date after the correct date-based gap computation in step 2, name the date and both posts, with their times. A real gap of 0 in the corrected gap-day list is what to look for.

**No ranking, no floor, no concentration check in this section.** Cadence is a count, not an engagement bucket. The moment a cadence line starts comparing engagement by day, it has become a Best Time to Post Reader claim wearing this skill's clothes, and it does not belong here.

---

## Section 4: The video secondary lens

Only runs for rows where `Type` is `video` and `Views` is populated. `references/foundations.md` section 8 governs this in full; this section adds the duration-band read specific to this audit.

**Procedure:**

1. Compute raw engagement spread (min to max, as a multiple) across video rows with `Views` populated. Report the denominator: how many of the profile's video rows actually carry `Views`.
2. Compute engagement-per-view (`engagement / Views * 100`, one decimal) for the same rows. Compare its spread to raw engagement's spread. A flat rate against a wide raw spread is the "whatever separated the winners happened before the view, not after" finding, per `references/foundations.md` section 8, and PostSnag does not carry reach or impressions, so this skill never speculates about why one video got more views.
3. **Duration bands.** Bucket videos into `short (<= 40 seconds)`, `medium (41-70 seconds)`, `long (71+ seconds)`. Apply the 5-post floor per band. Run the concentration check on every rankable band before it becomes a recommendation.

**Worked example, and why the concentration check earns its keep here.** On the synthetic file, the medium band (n=5) carries a median of 688, ahead of the long band's 455. Before shipping "medium beats long" as advice, the concentration check runs: mean over median is 2.65 and the top post is 45.1 percent of the band's total. **Two flags. Per `references/foundations.md` section 4, this bucket does not become a recommendation.** What actually happened: both of the creator's two highest-engagement posts in the entire 60-post file happen to be medium-length videos. That is not a validated duration effect, it is two specific posts sharing a trait, and the honest write-up says exactly that: name the two posts, do not rank the band. The long band, by contrast, clears with zero flags at median 455, the lowest of the three, which is the one clean video-length finding in the file. The short band sits at n=4, unrankable, median 894, the highest of the three, "too small to rank, worth testing" again.

---

## Section 5: Trajectory, gated

**Preconditions, all three, or this section does not run at all and says so in one line:**

- `span_days >= 90`
- Not in lite mode (`references/foundations.md` section 5: lite mode already forbids reporting a trend)
- `N >= 40` (lite mode's own floor makes this redundant with the point above, stated for clarity)

**The formula, this skill's own, since no shared file defines a corpus-level trend split.** It deliberately reuses the shape of the shared concentration check rather than inventing a new statistical model:

1. Sort all posts ascending by parsed `Posted`.
2. Split into two halves by count: the first `floor(N/2)` posts are the **earlier half**, the rest are the **later half**. On an odd `N`, the extra post goes to the later half.
3. Compute median engagement for each half.
4. `trajectory_ratio = later_median / earlier_median`, two decimals.
5. **Direction, working thresholds, labeled as such:** ratio `>= 1.15` is **rising**, ratio `<= 0.87` is **falling**, anything between is **flat**. (0.87 is the reciprocal of 1.15, so the band is symmetric around 1.0.)
6. Run the concentration check on each half independently before trusting either median: median-after-top-removed, top-post share of the half, mean over median. If either half flags two or three checks, say so and treat the ratio as provisional rather than shipping it flat.

**The confound sentence is mandatory on every trajectory finding, no exceptions:** PostSnag's Markdown export carries a follower count, but only as a single point-in-time number. There is no follower history in any export. A trajectory read cannot separate "the content got better" from "the audience got bigger," and this skill never claims it can.

**Worked example, real numbers, from the synthetic 60-post file (130-day span, clears all three preconditions):**

```
earlier half: 30 posts, 2026-03-21 to 2026-05-28, median 402, mean 567.2
later half:   30 posts, 2026-05-30 to 2026-07-28, median 530, mean 712.2
trajectory_ratio = 530 / 402 = 1.32  ->  RISING (>= 1.15)

concentration check, earlier half: median-after-del 402 (0.0%), top-share 24.2%, mean/median 1.41  -> no flags
concentration check, later half:   median-after-del 520 (-1.9%), top-share 15.9%, mean/median 1.34 -> no flags
```

Both halves clear clean, so the rising read is not an artifact of one outlier post pulling a half's median around. **A useful cross-check, worth running whenever it applies:** the later half here is exactly the same 30 rows as the shared free-tier fixture `profile-maya-torres-free-slice.csv`, because that fixture is defined as the most recent 30 posts of the same file. Its corpus median (530) matches the later-half median above exactly, which is a live audit seam: if a skill's free-tier lite-mode read and its full-mode trajectory read ever disagree on the shared later window, one of them has a bug.

---

## Section 6: Building the output

**Selecting the 3 what-works findings.** Pull from the rankable, unflagged or lightly-flagged (one flag, glued) buckets across format and topic, favoring findings with real volume behind them over thin ones. A finding that is technically true on 2 posts does not belong here; that belongs in the steal-worthy section instead, labeled as untested.

**Selecting the 3 what-does-not-work findings.** At least one should be a genuine absence (zero or near-zero share of the top quartile despite real volume), and at least one should be a clean, unflagged, ranked bucket that is simply below the corpus median. **If nothing in the file is a clean underperformer, say that instead of manufacturing one.** A flat, no-signal bucket reported honestly ("Kitchen & Counters sits within 1 percent of your corpus median, on 5 posts, no flags: tested, and it does neither") is a legitimate third finding when the data does not hand you a dramatic failure, per `references/foundations.md` section 6's "no signal" instruction.

**Selecting the 5 steal-worthy patterns.** Pull named patterns from `references/findings-pattern-library.md` and instantiate each with this profile's real numbers. This is where the under-floor buckets, the concentration-flagged-but-interesting buckets, and the single standout posts belong. Every steal-worthy pattern is explicitly labeled with its evidence tier (a real bucket at n>=5 with a caveat, or an under-floor bucket, or a single post), never presented with more confidence than the `n` behind it earns.

**The 30-day recommendation list.** Every item traces back to a named finding above by name. No recommendation appears that is not grounded in a finding the reader can go check. "Post more consistently" with nothing behind it does not belong on this list; "test 3 more link-style posts, because your 4 so far have the highest median of any format in the file" does.

---

## Section 7: What this rubric refuses to do

- **No claim about why a format or topic worked beyond what the numbers support.** Correlation is what is in the file. The algorithm and causation are not.
- **No sponsored-versus-organic split.** No paid-partnership flag exists in the export. If a top post was boosted, nothing here would show it, and the skill says so once rather than pretending the ranking is clean.
- **No performance-by-day claim.** Cadence in Section 3 counts posts by day. It never ranks days by engagement. That comparison belongs to Best Time to Post Reader, cited by name, not duplicated here.
- **No trajectory claim below the 90-day, non-lite-mode gate**, and no trajectory claim that omits the confound sentence.
- **No topic cluster shipped without the discard step run first.** A raw, un-sanity-checked head list is not a topic inventory; it is noise with a table around it.
- **No superlative that has not been checked literally.** Before writing "your best", "your worst", "the only", or any word ending in "-est", confirm it against the actual ranking, not a general impression of the file.
