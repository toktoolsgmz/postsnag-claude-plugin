# rubric.md

The full method for Competitor Content Gap Finder. Written so an agent with no other context can run it on any two exports and reach the same gap table as anyone else running it on the same two files.

Version 1.0 | 2026-08-04

---

## Section 0: What this skill is actually answering

Two accounts in the same niche almost never post the same mix. One of them is proof that a topic or a format works, on an audience that is not yours. The question worth answering is not "what does the competitor post about," it is narrower and more useful: **which of the competitor's proven winners does the user's own account never touch, or barely touch.** That is the only thing this skill ranks. A topic the competitor posts about constantly but that flops for them is not a gap, it is a trap, and this skill says so when it finds one.

**Two files, two roles, never confused:**
- **Your export.** The account the recommendation is for. Coverage on this side is a raw post count, never a performance claim.
- **Competitor's export.** The account being read for evidence. Every claim about it is a multiple of the competitor's own corpus median, never a raw number compared against your raw numbers.

Section 5 explains why those two files never get compared on the same raw scale.

---

## Section 1: Parse and validate, both files independently

Compute every number in this analysis with code.

1. Parse both CSVs with a real CSV parser, columns by header name. Full rules: `references/csv-parse.md` (condensed; full version in the complete bundle).
2. For each file, report row count, date range, span in days, and whether it is a profile-schema or group-schema export.
3. Compute `engagement = Reactions + Comments + Shares` per post, per `references/foundations.md` section 1.
4. Compute each file's own corpus median and mean, independently. **Never pool the two files into one corpus.** A pooled median mixes two different audiences and answers a question nobody asked.
5. Report LITE MODE per file, independently, using `references/foundations.md` section 5 (`posts < 40 OR span_days < 60`). If either file is in lite mode, say which one and what it costs (Section 8).

---

## Section 2: Topic inventory, both files, identical method

Run the mechanical clustering procedure in `topic-inventory-method.md` **once per file, independently.** Never look at one file's clusters while forming the other's; the clustering must not be tuned to make a gap appear. Both runs use the same STOPWORD list, the same FILLER list, the same stemmer, and the same 5-post floor (`references/foundations.md` section 3, reused here rather than invented).

Output of this step, per file: a list of topic clusters, each with a canonical display name, the set of post indices it covers, `n` (posts containing it), median engagement, mean engagement, and the highest-engagement member post.

**A post can belong to more than one cluster.** Composition percentages for topics do not need to sum to 100 percent, and the output says so once.

---

## Section 3: Format inventory, both files, the real Type values only

Group each file's posts by `Type`. The only values that exist anywhere in a PostSnag export are `text`, `photo`, `video`, `link`, `album` (`references/csv-parse.md` section 2; there is no poll type). Compute `n`, median engagement, and mean engagement per type, per file, same as any other bucket. Types with `n < 5` in a file are reported with their numbers and not ranked, same rule as everywhere else in this catalog.

**If the competitor's file is a group export, it has no format diversity beyond `Type` and no media columns at all** (`references/csv-parse.md` section 2). Say so and continue; the topic inventory still works, the format inventory is just shorter.

---

## Section 4: The competitor-winner definition

A topic cluster or format bucket on the **competitor's** side qualifies as a winner if ALL of these hold:

1. **Clears the floor.** `n >= 5` (the same floor from Section 2 and `references/foundations.md` section 3).
2. **Over-represented in their own top quartile.** Using their file's own top quartile (`k = floor(N/4)`, `references/foundations.md` section 6), the cluster's share of the top-k posts is strictly greater than its share of the whole corpus. This is the same composition test `facebook-hook-analyzer` uses to separate "used a lot" from "actually working": a bucket that is exactly as common in the winners as it is everywhere else is not proof of anything, it is just volume.
3. **Concentration check reported.** Run `references/foundations.md` section 4 (median-after-deletion, top-post share, mean-over-median) on every qualifying bucket before it becomes a recommendation. One flag: the bucket still qualifies, and the flag rides along with the number in the output, inline, per the standing rule. Two or three flags: the bucket does not qualify as a winner at all; name the single post responsible instead.

**A bucket that is common but not over-represented in the top quartile is reported, never recommended, and named as such.** If the competitor posts about a topic constantly (high corpus share) but that topic is under-represented or absent from their own top quartile, that is worth one sentence in the output: it tells the user not to copy that part, evidence they would otherwise have to discover the hard way.

**Every claim about a winner is expressed as a multiple of the competitor's own corpus median:**
```
their_multiple = winner_cluster_median / their_corpus_median
```
Never as a raw engagement number compared against anything of yours. Section 5 explains why.

---

## Section 5: Cross-profile normalization, the problem stated head-on

Two Facebook accounts almost never have the same audience size, the same age, or the same posting history, and PostSnag captures none of those things (no follower history beyond a single point-in-time number on the Markdown export, no reach, no impressions). A competitor's post that pulled 3,000 engagements and one of the user's posts that pulled 800 are not directly comparable numbers; the competitor might have ten times the audience, or a third of it, and there is no field in either export that says which.

**The fix used throughout this skill: each profile is measured against its own median, never against the other profile's raw numbers.**

- The competitor's evidence is always a **multiple of their own corpus median** (`their_multiple`, Section 4). "Rental content earns 1.34 times what a typical post of theirs earns" is a claim their own file proves, regardless of how big their audience is.
- The user's coverage is always a **raw post count in their own file** (Section 6): zero posts, one post, four posts. It is never converted into an engagement comparison against the competitor's numbers, because there is nothing in either export that would make that conversion honest.

**What this means the skill will never say:** "the competitor's rental post beat your best post by 4x" is a claim this skill refuses to make. It compares audiences that are not comparable. What it says instead: "the competitor's rental content beats their own typical post by 1.34x, and you have zero posts touching the topic." Two true, checkable claims, stitched together by absence, not by a raw-number matchup.

---

## Section 6: The gap definition and the absent/underweighted floor

A **gap** is a competitor-winner bucket (topic cluster or format, Section 4) where the user's own file shows one of these two states:

**ABSENT.** Zero of the user's posts contain any surface form of the winning topic's keyword set (for a topic cluster: any word matching the cluster's stemmed unigram or bigram key, searched against the user's own captions using the identical extraction and stemming rules from `topic-inventory-method.md`; for a format: zero posts of that `Type`).

**UNDERWEIGHTED.** 1 to 4 of the user's posts match. This is the same 5-post floor from Section 2 and `references/foundations.md` section 3, reused a third time in this rubric rather than invented fresh: below 5, the user has touched the topic but never built a real cluster of their own around it, the same reason a 4-post hook archetype does not get ranked in `facebook-hook-analyzer`.

**Not a gap.** 5 or more of the user's posts match. The user has real coverage, whether or not it currently performs as well as the competitor's. That comparison is a different skill's job (`facebook-profile-audit`), not this one's.

---

## Section 7: The gap-ranking formula

```
gap_score = their_multiple * absence_factor

where:
  their_multiple  = winning cluster's median / competitor's own corpus median      (Section 4)
  absence_factor  = 1.0                        if the user is ABSENT (0 matching posts)
                   = (5 - your_count) / 5       if the user is UNDERWEIGHTED (1 to 4 matching posts)
```

**Reading it.** `absence_factor` is 1.0 at zero coverage and shrinks toward 0.2 as the user's own count climbs toward the floor at 4. A gap where the user has 1 post scores nearly as high as full absence; a gap where the user has 4 posts scores a fifth as high, because the user has already started closing it themselves. A worked illustration, invented numbers, not from the shared dataset: a competitor topic at `their_multiple = 1.8` with the user fully absent scores `1.8 * 1.0 = 1.80`. The same topic with the user sitting at 3 matching posts scores `1.8 * (5-3)/5 = 1.8 * 0.4 = 0.72`, well below a fully-absent gap at a lower multiple, for example `1.2 * 1.0 = 1.20`. Rank the gap list by `gap_score`, descending.

**Ties**, in order: higher `their_multiple` wins (the stronger proof beats the emptier absence), then more competitor posts backing the cluster (`n`), then alphabetical, stated as such.

---

## Section 8: What lite mode and free-tier depth do to a two-file skill

`references/foundations.md` section 5 defines lite mode per file. This skill checks it **twice, independently**, because either file being thin degrades a different part of the output:

- **Your file in lite mode:** your own coverage counts (Section 6) are still exact counts and still trustworthy, a count of 0, 1, or 4 does not need 40 posts to be true. What gets worse is the confidence that an ABSENT reading is really absence and not a blind spot: a 30-post free-tier slice is your most recent posts only (`references/foundations.md` section 5), so "zero rental posts in your last 30" is a true, narrower claim than "zero rental posts, ever."
- **Competitor's file in lite mode:** this is the more damaging direction. Fewer topic and format clusters clear the 5-post floor on their side, so fewer buckets are even eligible to become winners (Section 4), and the gap list gets shorter, not wrong. Say the specific number: "6 of 9 candidate clusters fell below the floor on their file, so the gap list below is built from the 3 that survived."

**Both files free-tier (30 posts each) is the worst case and the most common one**, since this skill needs two captures by definition. State it plainly rather than softening it: with two 30-post slices, expect a short gap list, and name the deeper capture that would lengthen it on whichever side is thinner.

---

## Section 9: Evidence citation, non-negotiable

Every gap in the output cites the competitor's single best-performing member post from that cluster, **verbatim**, with its full engagement breakdown (`reactions / comments / shares`, and the total). Never a paraphrase, never a composite description of "posts like this." The reader has to be able to go find that exact post and check the numbers themselves.

---

## Section 10: The 5 drafted post ideas, written in the user's own voice

**The instruction that matters most in this section: draft in the user's voice, using the competitor's topic as the subject, never the competitor's sentences as source text.** A draft that could be pasted unchanged into the competitor's own feed is wrong, the same failure mode `facebook-hook-analyzer` names for a hook template that could belong to any creator in any niche.

1. **Take the ranked gap list from Section 7.** If it has 5 or more entries, draft one idea per gap, top 5 by `gap_score`. If it has fewer than 5 (the common case: gap-finding is intentionally strict, and most captures surface 1 to 3 real gaps), fill the five with multiple angles on the strongest gaps, weighted toward the higher-scored ones, and say the split out loud: "2 gaps cleared the winner bar, so the five drafts below split 3 and 2 across them, not evenly by default."
2. **Pull the user's own proven hook style**, not the competitor's. This skill does not re-derive a voice profile; it cites `facebook-hook-analyzer/references/rubric.md` sections 2 and 5 for the full archetype system, and uses the local `references/hook-archetypes.md` (condensed; full version in the facebook-hook-analyzer skill and the complete bundle) when that skill has not been run: identify the user's own top 1 or 2 rankable hook archetypes by median engagement (5+ posts, from their own file, using the same 12-archetype ladder). If `facebook-hook-analyzer` has already been run on this file, its output table can be used directly instead of recomputing.
3. **Write the gap's subject matter into that archetype's shape.** The topic comes from the competitor's evidence (Section 9). The sentence shape, the rhythm, and the address (second person, first person, a bold declarative) come from the user's own winners.
4. **Cite the source of both halves inline**: which gap the draft fills, and which of the user's own archetypes or posts it is modeled on.

**These drafts are unproven ideas filling a proven gap; nothing here predicts performance.** The gap is real (the competitor's own file proves it). The draft filling it has never been posted by anyone, and this skill does not claim it will work.

Archetype identification uses the full 12-archetype ladder and precedence order in `references/hook-archetypes.md`, not a shortened stand-in table, so the same hook classifies the same way here as it does in `facebook-hook-analyzer`.

---

## Section 11: What this rubric refuses to do

- **No format or topic claim without the competitor-winner test passing.** A topic the competitor posts about a lot is not, by itself, evidence of anything. Composition against their own top quartile is the test, every time.
- **No raw cross-profile engagement comparison, ever.** Section 5 is not a caveat, it is a rule this skill cannot break in either direction.
- **No claim that a drafted idea will perform.** The draft fills a demonstrated gap in subject matter, written in a demonstrated voice pattern. Neither PostSnag nor this skill has ever posted it, and the output says so once.
- **No sponsored-versus-organic split on either file.** Neither export carries a paid-partnership flag, so a competitor's boosted post looks identical to an organic one in their evidence. Say so once.
- **No claim about why the competitor's audience responded.** Correlation between a topic and their engagement is what the file supports. The reason is not in the data.
