# example-run.md

> **SYNTHETIC.** Maya Torres is a fictional creator. Every post, number, and date below is invented. This run consumes three upstream artifacts, all synthetic, all built on `../../_shared/synthetic-data/profile-maya-torres.csv`: the worked outputs in `../../facebook-profile-audit/references/example-run.md`, `../../facebook-hook-analyzer/references/example-run.md`, and `../../best-time-to-post-reader/references/example-run.md`. The solo-mode appendix runs on `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv`. Nothing here describes a real person or a real Facebook account.

This is the rubric executed start to finish in **chain mode**, consuming the literal outputs of the three upstream skills. Every number consumed below is quoted from one of those three files. Nothing here is recomputed and nothing here is estimated. If a number here disagrees with the upstream file it cites, this file is wrong and gets fixed.

Run date: 2026-08-04. Target week: Monday 2026-08-10 to Sunday 2026-08-16, the next full Monday-to-Sunday week.

Version 1.0 | 2026-08-04

---

# PART 1: THE WORK

Everything in Part 1 is the analyst's working, shown so the chain is auditable. Part 2 is what the user actually receives.

---

## Step 0: the three artifacts and the cross-checks

**Headers, quoted:**

```
audit:      "60 posts, 2026-03-21 to 2026-07-28, 130 days."
hook:       "60 posts, 2026-03-21 to 2026-07-28, 130 days."
best-time:  "60 posts, 2026-03-21 to 2026-07-28, 130 days."
```

Identical. Cross-check 1 passes.

**Corpus median, quoted from each:** audit `458.5`, hook `458.5`, best-time `458.5`. Cross-check 2 passes.

**Posting-day counts.** The audit's Cadence section: `Saturday 19, Thursday 17, Tuesday 12, Monday 9, Wednesday 1, Friday 1, Sunday 1`. The time read's best-days table plus its too-small-to-rank line: Thursday 17, Tuesday 12, Saturday 19, Monday 9, and `Wednesday (1 post, 566), Friday (1 post, 388), Sunday (1 post, 560)`. Day for day, both sum to 60. Cross-check 3 passes.

**Format inventory.** The audit's header: `photo 17 (28.3%), text 17 (28.3%), video 14 (23.3%), album 8 (13.3%), link 4 (6.7%)`. Its own format distribution table: photo 17, text 17, video 14, album 8, link 4. Cross-check 4 passes.

**Lite mode:** all three artifacts report `lite mode OFF (60 posts >= 40, 130 days >= 60)`. Full mode. No inherited banner.

**Timezone:** the time read's header says `Times below are in America/Los_Angeles, which you confirmed.` Clock times are available on Tier 1 slots.

**One upstream discrepancy, found by this build and now resolved.** An earlier version of the hook analyzer reported Maya's video engagement-per-view spread as `1.33x`, disagreeing with the profile audit's `1.32x`. Both quoted the same endpoints, 1.66 percent and 2.20 percent. This build found the mismatch, recomputed from the CSV (2.1972 / 1.6598 = 1.3238, rounding to **1.32**), and reported it upstream: the audit had it right, the earlier hook analyzer had rounded its endpoints before dividing. The hook analyzer has since been fixed to report 1.32x, matching the audit and matching this build's own recomputation. **This calendar consumes neither number**, so nothing here changes as a result of the fix, and the discrepancy and its resolution are recorded for the record rather than silently harmonized.

---

## Step 1: the input contract, section by section

What this run reads, quoted, from each artifact. Full field map: `chain-input-map.md`.

### From the profile audit

| Section | Quoted |
|---|---|
| Cadence | `60 posts across 130 days, 3.23 posts per week.` |
| Format distribution | photo 17 / 388 / 28.3% / 4 of 15; text 17 / 388 / 28.3% / 4 of 15; video 14 / 585 / 23.3% / 5 of 15, mean-over-median **1.89**; album 8 / 393 / 13.3% / **0 of 15**; link 4 / 795 / 6.7% / 2 of 15, check columns **not checked**, `no, n<5` |
| Top 10 versus bottom 10 | `top 10 is video 4, photo 3, link 2, text 1. Bottom 10 is photo 4, text 3, album 1, link 1, video 1.` |
| Topic clusters | Closets 10 / 530.0 / no flags; Labels & Systems 7 / 402 / two flags; Bins & Containers 5 / 470 / **top-share 45.4%**; Kitchen & Counters 5 / 462 / no flags; Pantries 3 / 712 / `no, n<5`; Kids' Spaces 1 / 540 / `no, n<5` |
| Duration bands | Short (<=40s) 4 / 894.0 / `no, n<5`; Medium (41-70s) 5 / 688 / mean-over-median 2.65, top-share 45.1%, `yes, but not shipped as a recommendation`; Long (71s+) 5 / 455 / clean |
| What works | 1 Closets holds up clean. 2 Video earns a real premium, use the median. 3 `Link posts, untested but the strongest number in the file.` |
| What does not work | 1 `Album is real volume with nothing at the top.` 2 Long videos, clean and lowest. 3 `Kitchen & Counters is tested and flat.` |
| 30-day list | 7 numbered items, quoted in Step 9 |
| Trajectory | `a ratio of 1.32, which this audit calls rising`, with the follower-history confound sentence |

### From the hook analyzer

| Section | Quoted |
|---|---|
| Your hook patterns | Question Open 11 / 610 / 4 of 15; Number Promise 7 / 560 / 2 of 15; Story Cold Open 8 / 430 / 1 of 15; Direct Address 9 / 388 / **0 of 15**; Problem Callout 17 / 327 / 2 of 15 |
| Too small to rank | `Bold Claim (3 posts, median 1,044), Curiosity Gap (2 posts, median 959), Command (2 posts, median 195), Confession (1 post, 1,904)` |
| Concentration note | `Story Cold Open sits at a median of 430 across 8 posts, but the pantry story alone accounts for 59 percent... Number Promise sits at 560 across 7 posts with the four-rules post accounting for 52 percent.` |
| Over-invest / under-invest | Bold Claim 5.0% to 20.0%; Curiosity Gap 3.3% to 13.3%; Question Open 18.3% to 26.7%; Problem Callout 28.3% to 13.3%; Direct Address 15.0% to 0% |
| Top 10 hooks, as templates | all 10, with archetype, verbatim hook, engagement, and the abstracted Template line |
| Structural read | Hook length 0-50 chars 13 / 327; **51-75 chars 46 / 464**; 76-100 chars 1 / 1,206 not ranked. Caption length 0-250 chars 39 / 388; **251-400 chars 21 / 700** |
| 5 archetypes to test next | 1 Confession (UNDERUSED), 2 Bold Claim (UNDERUSED), 3 Curiosity Gap (UNDERUSED), 4 Permission Grant (UNEXPLORED, latent-fit), 5 Contrarian Take (UNEXPLORED) |

### From the best-time reader

| Section | Quoted |
|---|---|
| Your best days | 1 Thursday 17 / 540 / `Concentration checked, clean. Format checked, no confound.` 2 Tuesday 12 / 521 / same. 3 Saturday 19 / 388 / `Mean/median 1.73, carried partly by your 3,402-engagement post from June 6. Format: link posts are 2 of these 19, 1.58 times their normal share.` 4 Monday 9 / 341 / `1 of these 9 is a link post, 1.67 times a link post's normal share, and that post is also Monday's best at 1,402.` |
| Too small to rank | `Wednesday (1 post, 566), Friday (1 post, 388), Sunday (1 post, 560)` |
| Your best windows | 1 Tuesday Evening 6 / 712 / median-shift 26.7% **and** link confound 2.5x. 2 Saturday Midday 6 / 384 / link confound 2.5x, `That post earned 402, right at this window's median`. 3 **Thursday Midday 7 / 355 / `Concentration checked, clean. Format checked, no confound. The only window in this table that came through both checks clean.`** 4 Saturday Morning 10 / 336 / link confound `exactly 1.5 times`, `That post earned 244, second-lowest in the window, so link is over-represented here while pulling the number down, not up.` |
| Excluded window | Thursday Evening 6 / 613, two concentration flags, top post 58.4% of the window, also video 3 of 6 |
| Where you post versus where you win | Saturday 19 of 60, 31.7%. Thursday 540, `39.2 percent higher than Saturday's 388`. |
| Format medians | link 795 (1.73 ratio), video 585 (1.28), album 393 (0.86), photo 388 (0.85), text 388 (0.85) |

---

## Step 2: slot count

```
base          = round(3.23)  = 3          [audit Cadence: "3.23 posts per week"]
clamp [3,6]                  = 3
experimental  = 1                          [base 3 <= 4]
total         = 4
cap: ranked days in the time read's best-days table = 4 (Thu, Tue, Sat, Mon)
total = min(4, 4) = 4
```

**4 slots across 7 days.** The cap did not bite this week. It bites hard in solo mode, and it is the reason the appendix at the bottom of this file ships 3 slots instead of 5.

---

## Step 3: format mix

`lift = (share of top quartile) / (share of corpus)`, both columns read from the audit's format table. Top quartile is k=15, cut value 700.

| Type | n | median | share of corpus | share of top 15 | lift | Tier |
|---|---|---|---|---|---|---|
| video | 14 | 585 | 23.3% | 5 of 15 (33.3%) | **1.43** | **A** |
| link | 4 | 795 | 6.7% | 2 of 15 (13.3%) | **2.00** | **D** (n<5) |
| photo | 17 | 388 | 28.3% | 4 of 15 (26.7%) | 0.94 | B |
| text | 17 | 388 | 28.3% | 4 of 15 (26.7%) | 0.94 | B |
| album | 8 | 393 | 13.3% | **0 of 15 (0.0%)** | **0.00** | **C** |

**Proven slots = 3. Tier A holds one format (video).** Cap is `ceil(3/2) = 2`, so video takes 2 and the third proven slot goes to the highest-lift Tier B format.

**Photo and text tie at 0.94.** Tie-break 1, median: both 388. Tie-break 2, n: both 17. Tie-break 3, top-10 minus bottom-10, read from the audit's line `top 10 is video 4, photo 3, link 2, text 1. Bottom 10 is photo 4, text 3, album 1, link 1, video 1`:

```
photo:  3 - 4 = -1
text:   1 - 3 = -2
photo wins
```

Two formats identical on lift, median, and count, separated only by how often each lands at the bottom. That one line in the audit is the whole tie-break, and without it this comes down to a coin flip.

**Experimental format = link**, the highest-lift Tier D format and the audit's own What works finding 3: `Link, only 4 posts, median 795, the highest median of any format you use... It is the clearest "write three more and find out" in this audit.` The audit's 30-day list item 1 asks for exactly this.

**Album gets zero slots**, per Tier C and the audit's What does not work finding 1.

**Final format mix: video 2, photo 1, link 1, text 0, album 0.**

**Duration bands** for the two video slots, from the audit's duration table:

- Short (<=40s), n=4, median 894, unrankable, and the audit's steal-worthy pattern 4 calls it `One short video away from being measurable.` Assigned to one video slot as a test.
- Medium (41-70s), n=5, flags on two of three checks, and the audit's 30-day list item 2 says `Script and post one more medium-length video (41 to 70 seconds).` Assigned to the other video slot as a test, with the audit's caveat traveling: this band is not a proven recommendation, it contains her two biggest posts.
- Long (71s+): excluded, per 30-day list item 4, `Cap new long-form videos at 70 seconds.`

Constraint satisfied: the two video slots do not share a band.

---

## Step 4: hook pools

**Pool 1 (ranked, lift at or above 1.00, fewer than 2 concentration flags):**

| Archetype | n | median | share of posts | share of top 15 | lift | In Pool 1? |
|---|---|---|---|---|---|---|
| Question Open | 11 | 610 | 18.3% | 26.7% | **1.46** | **yes** |
| Number Promise | 7 | 560 | 11.7% | 13.3% | 1.14 | no, 2 concentration flags |
| Story Cold Open | 8 | 430 | 13.3% | 6.7% | 0.50 | no, lift under 1 and 2 flags |
| Direct Address | 9 | 388 | 15.0% | 0.0% | 0.00 | no |
| Problem Callout | 17 | 327 | 28.3% | 13.3% | 0.47 | no |

**Pool 1 = Question Open. One archetype.**

**Pool 2 (n between 3 and 4, zero concentration flags, median above 458.5):**

Read from the analyzer's too-small-to-rank line and its flag table. Bold Claim, n=3, median 1,044, and the analyzer states it explicitly: `Bold Claim is the only bucket in the file with a small n and zero flags.` 1,044 is above 458.5. Qualifies.

Curiosity Gap (n=2) and Confession (n=1) fall below the n>=3 floor. Command (n=2) is also below the corpus median.

**Pool 2 = Bold Claim. One archetype.**

**Pool 3 (the analyzer's test list, in its own order):**

```
1. Confession        UNDERUSED, 1 post, 1,904          -> eligible
2. Bold Claim        UNDERUSED, 3 posts, median 1,044  -> already assigned via Pool 2, skip
3. Curiosity Gap     UNDERUSED, 2 posts, median 959    -> SKIP: 2 concentration flags
4. Permission Grant  UNEXPLORED, latent-fit, 2 body hits -> eligible
5. Contrarian Take   UNEXPLORED, zero instances         -> eligible
```

**Assignment.** 3 proven slots, and Pools 1 and 2 together supply 2 archetypes. Pools run dry. Rule 2 of section 2.3 fires: the third proven slot converts to hook-experimental rather than being padded with a demoted archetype. Combined with the one designated experimental slot, that gives **2 proven hooks and 2 experimental hooks**.

- Proven: **Question Open** (Pool 1), **Bold Claim** (Pool 2)
- Experimental: **Confession** (Pool 3 #1), **Permission Grant** (Pool 3 #4)

**Curiosity Gap was skipped and Permission Grant was taken instead**, on the Pool 3 flag screen. Worth stating plainly, because it is the rule doing real work: Curiosity Gap sits higher on the analyzer's list, but its only evidence is a 2-post bucket carrying two concentration flags, and the analyzer itself notes those flags are `close to automatic` at n=2. Permission Grant's evidence is different in kind: the latent-fit test found the archetype in the body of two of her posts, verbatim, and it has never once been her first line. That is not a bigger number, it is a different sort of evidence, and it survives a screen the bigger number does not.

Rotation rule: 4 distinct archetypes across 4 slots. Satisfied.

**Zero slots for Problem Callout and Direct Address**, both by lift: 28.3 percent of her posts and 13.3 percent of her top 15 for the first, 15.0 percent and 0.0 percent for the second.

---

## Step 5: topic assignment

From the audit's topic table.

```
Proven pool (rankable, median at or above 458.5, at most 1 flag):
  Closets              10 posts, median 530.0, zero flags        -> eligible
  Bins & Containers     5 posts, median 470,   top-share 45.4%   -> eligible, 1 flag
  Kitchen & Counters    5 posts, median 462,   zero flags        -> SKIPPED, tested and flat
  Labels & Systems      7 posts, median 402,   two flags         -> excluded, below corpus median
```

**The tested-and-flat skip, worked.** Kitchen & Counters is 462 against a corpus median of 458.5. `|462 - 458.5| / 458.5 = 0.76 percent`, inside the 5 percent band, zero flags, rankable. That is the audit's own What does not work finding 3, restated: `This is not a failure, it is a null result.` It is skipped with one printed line, not hidden and not stretched.

**Proven pool supplies 2 topics for 3 proven slots.** Falls to the highest-median unrankable topic: **Pantries**, 3 posts, median 712, the highest median in the whole topic table.

**Experimental topic:** the audit's 30-day list item 5, `Write 3 to 4 more Kids' Spaces posts.` Kids' Spaces, 1 post, 540.

Assigned highest median to highest-confidence slot, resolved in Step 6: Closets (530, clean), Bins & Containers (470, one flag), Pantries (712, unrankable), Kids' Spaces (540, unrankable).

---

## Step 6: time assignment and the tiers

**Tier ladder applied to each of the four ranked days.**

| Day | Day row | Windows on that day | Tier | Why |
|---|---|---|---|---|
| Thursday | 17, 540, both checks clean | **Thursday-Midday 7 / 355, both checks clean**; Thursday-Evening 6 / 613 **excluded upstream, 2 concentration flags** | **1** | a window came through both checks clean, and the timezone is confirmed |
| Tuesday | 12, 521, both checks clean | Tuesday-Evening 6 / 712, median-shift 26.7% **and** link confound 2.5x | **2** | day clean, no clean window on it |
| Saturday | 19, 388, divergence 1.73 **and** link confound 1.58x | Saturday-Midday 6 / 384 link confound 2.5x; Saturday-Morning 10 / 336 link confound 1.500 | **3** | day carries flags |
| Monday | 9, 341, link confound 1.67x | none cleared the 5-post floor (3 / 3 / 2 / 1 across the four bands) | **3** | day carries a flag |

**Saturday carries two flags and is still Tier 3, not Tier 4.** They are two different checks: one concentration flag (divergence 1.73) plus one format-confound flag. The 2-flag exclusion rule counts concentration parts only, and the time reader ranked Saturday third knowing both. Miscounting this would throw away a ranked day.

**The Thursday number worth saying out loud.** Thursday's day-level median is 540. The one Thursday window this file can stand behind is midday at 355. The difference is Thursday-Evening at 613, which the time reader excluded because a single post is 58.4 percent of that window's total engagement. So the Thursday slot schedules into the day the file ranks first and the window inside it the file can defend, and those are two different numbers. Both get printed.

**Slot confidence order:** Thursday (Tier 1) > Tuesday (Tier 2) > Saturday (Tier 3, median 388) > Monday (Tier 3, median 341).

**The clock time is the upstream's band verbatim: midday, 11am to 5pm, America/Los_Angeles.** Not narrowed to an hour. The time reader measured four bands, not 24 hours.

**Schedule gap.** The time read: most-posted Saturday at 31.7 percent, best-median Thursday. At 4 slots across 4 ranked days every day gets exactly one, so the gap closes by evening out rather than by loading Thursday:

```
Saturday  31.7% -> 25.0%   (-6.7 points)
Thursday  28.3% -> 25.0%   (-3.3)
Tuesday   20.0% -> 25.0%   (+5.0)
Monday    15.0% -> 25.0%   (+10.0)
```

Monday is her lowest-median rankable day at 341 and takes the biggest relative increase, which is a consequence of the arithmetic and not a recommendation. It is why Monday is named as the cut-first slot in the summary.

---

## Step 7: pairing

**Co-occurrence overrides, from the analyzer's top-10 template list.** Each entry names an archetype and belongs to a post whose format is in the audit:

| Archetype | Her best instance | That post's format | Format allocated this week? | Override |
|---|---|---|---|---|
| Question Open | 902, `What is the one drawer you would not let a guest open?` | photo | yes (1 slot) | **photo** |
| Bold Claim | 1,188, `Most organizing systems fail because they were designed on a good day.` | link | yes (1 slot) | **link** |
| Confession | 1,904, `I have a closet in my own house I do not film.` | video | yes (2 slots) | **video** |
| Permission Grant | never used as a hook, so no top-10 entry | n/a | n/a | falls to the remaining video slot |

Three of four pairings come from her own file. The fourth is assigned by elimination and the slot says so.

**Evidence scores** (`hook points + format points`):

```
Question Open (Pool 1, 3) + photo (Tier B, 2)   = 5
Confession (Pool 3, 1)    + video (Tier A, 3)   = 4
Permission Grant (Pool 3, 1) + video (Tier A, 3) = 4
Bold Claim (Pool 2, 2)    + link (Tier D, 1)    = 3
```

The two 4s tie. Tie-break: a co-occurrence citation in the creator's own top 10. Confession has one (the 1,904 video). Permission Grant does not. Confession ranks above.

**Naive rank-to-rank match:**

```
Thursday (T1) <- Question Open + photo
Tuesday  (T2) <- Confession + video
Saturday (T3) <- Permission Grant + video
Monday   (T3) <- Bold Claim + link
```

**The double-cite rule fires on Monday.** Monday's day row carries a link format-confound: `1 of these 9 is a link post, 1.67 times a link post's normal share, and that post is also Monday's best at 1,402.` Scheduling a link post on Monday reproduces the exact confound the evidence warned about, and it does it while printing an evidence line pointing at that confound.

Preference (a), move the format to a link-clean day. Link-clean days among the four, from the time read's format-confound table:

```
Thursday  checked, no confound. Nothing clears 1.5.        -> link-clean
Tuesday   checked, no confound. "Link is 1/12 at 1.25."    -> link-clean, explicitly
Saturday  CONFOUND flagged on link, 1.58x                  -> blocked
Monday    CONFOUND flagged on link, 1.67x                  -> blocked
```

Thursday holds the highest-evidence pair on the highest-tier slot. So the link moves to Tuesday, and Confession moves down to Monday:

```
Thursday (T1) <- Question Open + photo
Tuesday  (T2) <- Bold Claim + link          [moved by the double-cite rule]
Saturday (T3) <- Permission Grant + video
Monday   (T3) <- Confession + video         [moved by the double-cite rule]
```

**Re-check every pairing after the move:**

| Slot | Format | Confound result on that bucket | Verdict |
|---|---|---|---|
| Thursday, Tier 1, tests the **window** | photo | Thursday-Midday: `checked, no confound`, and the day-level row lists `photo 4/17 at 0.83` | clean, and independently confirmed |
| Tuesday, Tier 2, tests the **day** | link | Tuesday day: `checked, no confound. Link is 1/12 at 1.25.` | clean, and independently confirmed |
| Saturday, Tier 3, tests the **day** | video | Saturday's confound named **link** at 1.58x. Video's own representation on Saturday was not printed. | not flagged, and not independently confirmed clean |
| Monday, Tier 3, tests the **day** | video | Monday's confound named **link** at 1.67x. Video's own representation on Monday was not printed. | not flagged, and not independently confirmed clean |

Two slots confirmed clean, two slots not flagged but not confirmed. The calendar prints the difference rather than letting "not flagged" read as "checked and passed."

**Duration bands.** Confession's own instance is a 22-second video, so co-occurrence puts Monday at **short (<=40s)**. Permission Grant has no video instance, so Saturday falls to the audit's explicit instruction, 30-day list item 2, **medium (41-70s)**, and carries the audit's two-flag caveat on that band.

**Topics, matched to the confidence order:**

```
Thursday (T1) <- Closets            10 posts, median 530.0, zero flags
Tuesday  (T2) <- Bins & Containers   5 posts, median 470, top-share 45.4%
Saturday (T3) <- Pantries            3 posts, median 712, unrankable
Monday   (T3) <- Kids' Spaces        1 post,  540, unrankable, 30-day item 5
```

---

## Step 8: the confound budget

Four axes per slot: time, format, hook, topic. The duration band is a refinement of format, not a fifth axis.

| Slot | Time | Format | Hook | Topic | Untested |
|---|---|---|---|---|---|
| Thursday | ranked, both clean | photo, Tier B, rankable | Question Open, Pool 1, n=11 | Closets, n=10, clean | **0** |
| Tuesday | ranked, both clean | **link, Tier D, n=4** | **Bold Claim, Pool 2, n=3** | Bins & Containers, n=5, 1 flag | **2** |
| Saturday | ranked, flagged | video, Tier A, n=14 | **Permission Grant, never used** | **Pantries, n=3** | **2** |
| Monday | ranked, flagged | video, Tier A, n=14 | **Confession, n=1** | **Kids' Spaces, n=1** | **2** |

Six untested placements across four slots. Every slot is at or under budget. Thursday is the clean slot of the week: if it lands, four separate pieces of evidence held, and if it misses, all four are worth re-examining.

**The audit's 30-day list item 7 is declined this week, for two independent reasons, both stated.**

The item: `Test one post on a day you rarely use, Wednesday, Friday, or Sunday, and see whether the audience is there.`

```
Reason 1, the slot cap. Section 2.1 step 5 caps the week at the number of days
the time read ranked. That is 4. Wednesday, Friday, and Sunday are all in the
too-small-to-rank line at 1 post each. There is no fifth slot to put one in.

Reason 2, the confound budget. Even if a fifth slot existed, Maya's hook evidence
supports 2 proven archetypes and her topic evidence supports 2 proven clusters.
Every slot after the second is already carrying 2 untested axes. Adding an
untested day makes it 3, and a 3-axis-untested slot that underperforms tells you
nothing about which of the three was responsible.
```

**Deferred, with the design named:** run it next week, on a Wednesday, with photo, with a Question Open hook, and with a Closets topic. Every other axis proven. Then the day is the only variable and the answer is readable.

Declining an upstream instruction with a stated reason is a finding. Declining it silently is a bug.

---

## Step 9: the flag propagation ledger

Every flag read from any of the three artifacts, with its disposition. A flag with no disposition would be a bug.

| # | Source | Flagged bucket | Flag | Inherited by | How it appears |
|---|---|---|---|---|---|
| 1 | audit, format table | video | mean/median 1.89 | slots on Saturday and Monday | caveat: use the median 585, two videos carry the mean |
| 2 | audit, format table | link | check columns `not checked`, n=4 | Tuesday slot | caveat: link is Tier D, unrankable, so this format axis is untested and the concentration check never ran on it |
| 3 | audit, duration bands | Medium (41-70s) | mean/median 2.65 and top-share 45.1% | Saturday slot | caveat: the band contains her two biggest posts, so this is a deliberate test, not a proven band |
| 4 | audit, duration bands | Short (<=40s) | unrankable, n=4 | Monday slot | caveat: band untested, one video from measurable |
| 5 | audit, topic table | Bins & Containers | top-share 45.4% | Tuesday slot | caveat: one post is 45.4 percent of the cluster's total, and the median of 470 still holds under the other two checks |
| 6 | audit, topic table | Labels & Systems | two flags, median 402 | nothing | value not used: below the corpus median before the flags are even counted |
| 7 | audit, What does not work 3 | Kitchen & Counters | tested and flat | nothing | value skipped, with one printed line |
| 8 | hook, pattern table | Story Cold Open | top-share 58.8%, divergence 2.04 | nothing | value not used: the single-post screen keeps it out of a proven slot, and Pool 3 never reached it |
| 9 | hook, pattern table | Number Promise | top-share 52.2%, divergence 1.66 | nothing | value not used, same screen |
| 10 | hook, too small to rank | Curiosity Gap | 2 concentration flags at n=2 | Saturday slot | **skipped in Pool 3**, Permission Grant taken instead; this skip is printed on the Saturday slot's rule-fired note, so this row prints, it does not vanish into "nothing" |
| 11 | hook, too small to rank | Command | 2 flags, median 195 | nothing | value not used, below the corpus median |
| 12 | hook, structural read | question marks in hooks | double-counts the Question Open result on the same 11 posts | Thursday slot | the calendar does not cite question marks as a separate reason for the Question Open assignment |
| 13 | best-time, best days | Saturday | divergence 1.73, carried by the 3,402 post from June 6 | Saturday slot | caveat printed on the slot |
| 14 | best-time, best days | Saturday | link confound 1.58x | Saturday slot | caveat, folded into row 13's Saturday checks text; separately, when the double-cite rule chose a destination for Monday's moved link, this same flag ruled Saturday out as blocked. Saturday's own slot format is video, never link, so nothing on Saturday itself moved: this is a destination exclusion, not a move |
| 15 | best-time, best days | Monday | link confound 1.67x, and that post is Monday's best at 1,402 | **moved a slot**, plus caveat | link moved off Monday to Tuesday by the double-cite rule; the caveat prints as "read 341 as 8 ordinary posts plus one strong link post" |
| 16 | best-time, best windows | Tuesday-Evening | median-shift 26.7% and link confound 2.5x | Tuesday slot | the reason the Tuesday slot is day-level, and the reason its posting warning says post earlier in the day |
| 17 | best-time, best windows | Saturday-Midday | link confound 2.5x, the post sits at the window median | Saturday slot | contributes to the Saturday slot being day-level |
| 18 | best-time, best windows | Saturday-Morning | link confound exactly 1.500, and the post is second-lowest, pulling **down** | Saturday slot | printed with its direction: over-represented while pulling the number down, not up |
| 19 | best-time, excluded | Thursday-Evening | 2 concentration flags, top post 58.4%, also video 3 of 6 | Thursday slot | Tier 4. Named once as why the Thursday slot is midday and not evening. |

**Nineteen flags read. Fourteen print on a slot, as a caveat or as a posting warning (row 10 prints on the Saturday slot's rule-fired note; the original pass had miscounted it as unused). Of those fourteen, one (row 15) moved a slot, and one (row 14) separately excluded a destination without moving anything itself. Five name a value this calendar did not use.** Flag 18 is the one to read twice: it fired, it is true, and its direction is the opposite of what a careless calendar would print.

---

## Step 10: voice extraction and the drafting checks

**Voice profile, extracted mechanically from the 10 posts in the analyzer's top-10 template list:**

```
paragraph shape       hook line, blank line, then 2 to 3 body lines. Median 2.
                      One post (the 4-rules video) uses 4 numbered lines instead.
sentence rhythm       tight, not bimodal, matching `facebook-caption-writer`'s own
                      measured read on this same style-source set: median 12.0
                      words per sentence, range 5.4 to 16.3 per-post average,
                      2.7-word population standard deviation, under the 3.0
                      tight/loose flag. "She does not swing between clipped
                      one-liners and long run-ons; her winning posts hold a
                      narrow lane." Individual sentence lengths inside the
                      analyzer's top-10 template list run from 2 words
                      ("Limits do.") to 24 words ("I am telling you because
                      the version of this job where the organizer has no bad
                      closet is a version that does not exist."), with the
                      great majority under 20; there is no cluster of
                      sentences in a 20-to-30-word range to call a second mode.
punctuation           heavy comma for asides; colons in list posts; quoted speech
                      in 8 of 60 posts; numerals and spelled-out numbers both used
emoji                 0 across all 60 posts
hashtags              0 across all 60 posts
explicit CTA lines    0. The analyzer reports "CTA lines skipped: 0."
closing move          an aphorism or a turn back on the reader, in 8 of the 10.
                      "The stuff is never about the stuff." "That is the entire
                      system." "Start there, not with the pretty closet."
```

**Character targets, from the analyzer's structural read:** hook line **51 to 75 characters** (46 posts, median 464, against 13 posts at 0-50 chars, median 327). Caption **251 to 400 characters** (21 posts, median 700, against 39 posts at 0-250 chars, median 388). The 76-100 character hook bucket has n=1 and is never used as a target.

**On video slots the draft has two parts**, because a caption is not a script: the caption is governed by the 251-to-400-character target, and the on-camera script is governed by the assigned duration band at roughly 2.2 words per second.

**Caption-length arbitration against Maya's measured word band (R3), run honestly rather than silently.** `creator-voice-skill-builder/references/example-run.md` measured Maya's own caption length directly, in words, at 38 to 69, and her sentence rhythm at a median of 12.0 words per sentence with an observed per-post range of 5.4 to 16.3. Per this rubric's section 4.3 arbitration rule, that measured word band governs over the hook analyzer's character-based bucket. Checked against it, word by word, this run's four drafts do not all clear it:

| Slot | Caption word count | Against the 38-to-69 word band | Sentence rhythm |
|---|---|---|---|
| 1, Monday | 72 | **over, by 3** | 18.0 words/sentence average, over her 16.3 observed per-post max |
| 2, Tuesday | 72 | **over, by 3** | 9.0 words/sentence average, inside her range |
| 3, Thursday | 79 | **over, by 10** | 13.2 words/sentence average, inside her range |
| 4, Saturday | 54 | inside the band | 10.8 words/sentence average, inside her range |

**Three of four drafts, slots 1, 2, and 3, run past Maya's measured word band, and slot 1 additionally runs past her observed sentence-rhythm maximum.** This was not caught before this run, and it does not get quietly fixed by re-drafting all three now, because that would hide the miss rather than name it. The instruction that follows from it is one line: **tighten these three captions to the 38-to-69 word band, and slot 1's sentences toward its 16.3-word observed maximum, before posting.** The drafts as printed in Part 2 below are shown as originally drafted, word counts and all, so the miss is visible rather than corrected after the fact.

**Originality checks on the four drafts:**

| Check | Result |
|---|---|
| Subject test | all four use objects from her own file (closets, bins, pantries, playrooms) with new specifics |
| 6-word rule | longest run found: **5 words**, `you would not let a`, in the Thursday hook against her 902 post. Deliberate template reuse, under the limit, noted rather than rewritten. Second longest: 5 words, `a four year old cannot`, in the Monday script against her playroom post. |
| Same-example test | her closet post names a sled and a router box; the Thursday draft names folding chairs and a humidifier. Her pantry posts name flour and cumin is new. No example reused. |
| Performance silence | no draft and no line near a draft claims any of them will perform |

**One discretionary tighten, not a rule-forced rewrite (R2).** The Tuesday hook was first drafted as `Bins do not create space. A deadline written on the side does.` Her 2026-04-30 entryway post contains `the returns pile, with a deadline written on the side`, and the shared run between the two, `a deadline written on the side`, is exactly 6 words, at this skill's 6-word limit, not over it. Per `rubric.md` section 4.4, a run at 5 or 6 words is expected on a deliberate template reuse and is meant to be noted in the working notes, not rewritten; only a run of 7 or more words forces a rewrite. This one did not clear that bar. It was tightened anyway, to `A date written on the side does`, which drops the shared run to 4 words: a discretionary choice made for a tighter-reading hook, not something the 6-word rule as written required. Noted here rather than left implying the rule fired when it did not.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable. Part 1 was the working.

---

**Drafts only.** Nothing here is scheduled, connected, or published. This skill does not touch your Facebook account. It writes text and puts dates next to it. You post it.

# Content calendar: Maya Torres, 2026-08-10 to 2026-08-16

Built from your profile audit, hook analysis, and best-time read, all three on the same 60-post capture, 2026-03-21 to 2026-07-28. Times are in America/Los_Angeles, the timezone you confirmed in the time read.

4 slots across 7 days. Your cadence is 3.23 posts per week, which rounds to 3, plus 1 experimental slot. Your time read ranked 4 days, so the cap did not cut anything this week.

---

## The week

| Day | Date | Slot | Format | Hook archetype | Confidence |
|---|---|---|---|---|---|
| Monday | 2026-08-10 | 1 | video, short (40s or under) | Confession | Tier 3 |
| Tuesday | 2026-08-11 | 2 | link | Bold Claim | Tier 2 |
| Wednesday | 2026-08-12 | no slot | | | |
| Thursday | 2026-08-13 | 3 | photo | Question Open | **Tier 1** |
| Friday | 2026-08-14 | no slot | | | |
| Saturday | 2026-08-15 | 4 | video, medium (41 to 70s) | Permission Grant | Tier 3 |
| Sunday | 2026-08-16 | no slot | | | |

**Wednesday, Friday, and Sunday are empty on purpose.** Your time read has 1 post on each of those days in 130 days, which is not enough to rank them. Your audit asked you to test one of them. This week cannot do it well, and the reason is in the week summary below, along with the design for doing it properly next week.

---

## Slot 1: Monday, 2026-08-10

**Time:** day-level slot, no clock time | **Confidence: Tier 3**
**Checks:** Monday carries a format-confound flag. 1 of your 9 Monday posts is a link post, 1.67 times a link post's normal share of your account, and that post is also Monday's best at 1,402 engagements. Read Monday's median of 341 as 8 ordinary posts plus one strong link post, not as a Monday effect. No Monday time band reached 5 posts (3, 3, 2, and 1 across your four bands), so there is no window to schedule inside.
**Format:** video, short band, 40 seconds or under | **Hook:** Confession | **Topic:** Kids' Spaces
**Untested axes:** 2 of 4 (hook, topic)

**Template used:** `I still {do the wrong thing} and I have been doing this for {N years}.`

---

**Caption (362 characters, target 251 to 400):**

> I still organize playrooms for adults and I have done it for eleven years.
>
> I catch it in the photos. Everything at my eye level, everything in a lid, everything labeled in a font a four year old cannot read.
> The room resets beautifully and it is back on the floor by dinner, because the person who has to put it away is thirty inches tall and I built it for me.

**On-camera script (target 40 seconds or under, this runs about 33):**

> I still organize playrooms for adults and I have done it for eleven years.
>
> You can see it in my own photos. Lids on everything. Labels in a font a four year old cannot read.
> It resets beautifully and it is on the floor again by dinner.
> The fix is not discipline. Take the lids off, drop the shelf, and tape a picture of the thing to the front of the bin.

---

**because: time** Monday is rank 4 of your 4 rankable days, 9 posts, median 341, in your time read's best-days table. It carries the link format-confound above and no concentration flag.
**because: format** Video is your only Tier A format: 23.3 percent of your posts and 33.3 percent of your top 15, a lift of 1.43. Your audit's What works finding 2 says to use the median, 585, because mean over median is 1.89 and two videos carry the mean. The short band (40s or under) is 4 posts at a median of 894, the highest of your three duration bands and unrankable at n=4. Your audit's steal-worthy pattern 4 calls it "one short video away from being measurable." This is that video.
**because: hook** Confession is #1 on your hook analyzer's test list. One post, 1,904 engagements, 4.15 times your median, and the only time in 60 posts you admitted a room you have not fixed. One post is an observation, not a pattern, which is why this slot is experimental on the hook axis.
**because: topic** Kids' Spaces, 1 post, 540 engagements, above your corpus median of 458.5 on a single data point. Your audit's 30-day list item 5: "Write 3 to 4 more Kids' Spaces posts." This is 1 of those 3 to 4.

*Rule fired: the double-cite rule moved the link format off Monday, because link posts are 1.67 times their normal share of your Monday sample and that link post is Monday's best. Confession and video took this slot instead.*
*Format pairing note: Monday's confound flag names link, not video. Your time read prints the highest-representation format per bucket, so video's own representation on Monday was never printed. This pairing is not flagged and it is also not independently confirmed clean.*

---

## Slot 2: Tuesday, 2026-08-11

**Time:** day-level slot, no clock time | **Confidence: Tier 2**
**Checks:** Tuesday's day-level row is clean on both checks: concentration checked, clean, format checked, no confound. Your highest-median window anywhere in the file is Tuesday evening at 712, and it is not scheduled here, because it carries two caveats: the median drops 26.7 percent to 522 when its best post is removed, and that same post is a link post at 2.5 times a link post's normal share.
**Posting warning:** post this one earlier in the day. If you post it in the evening you land in the Tuesday evening band, and this slot is a link post, which is the exact format that band's confound flag names.
**Format:** link | **Hook:** Bold Claim | **Topic:** Bins & Containers
**Untested axes:** 2 of 4 (format, hook)

**Template used:** `{Thing everyone buys} does not {the job they bought it for}. {Thing nobody buys} does.`

---

**Caption (359 characters, target 251 to 400):**

> Bins do not create space. A date written on the side does.
>
> A bin holds whatever you put in it, including the decision you are avoiding. That is not storage, it is a waiting room.
> Put a date on masking tape and stick it to the side. Returns: fourteen days. Outgrown: end of season.
> I wrote up the three bins I put in every house and the dates that go on them.

*The link destination is yours to supply. This draft is written to set up a click, not to name a page.*

---

**because: time** Tuesday is rank 2 of your 4 rankable days, 12 posts, median 521, and the only ranked day besides Thursday that came through both upstream checks clean. Your time read lists link at 1 of 12 on Tuesday, a ratio of 1.25, under the 1.5 threshold, so this slot's format is explicitly clean here.
**because: format** Link has the highest lift of any format in your file: 6.7 percent of your posts and 13.3 percent of your top 15, a lift of 2.00, on the highest median of any format you use at 795 against your corpus median of 458.5. It is unrankable at 4 posts, its concentration check was never run, and your audit calls it "the clearest write three more and find out in this audit." Your 30-day list item 1 asks for 3 of these. This is the first.
**because: hook** Bold Claim is your hook analyzer's highest-confidence small bucket: 3 posts, median 1,044, 2.28 times your median, 3 of your top 10, zero of your bottom 10, and the only bucket in your file with a small n and zero concentration flags. Your best Bold Claim, at 1,188, is a link post, which is why these two are paired.
**because: topic** Bins & Containers, 5 posts, median 470, above your corpus median of 458.5. One post accounts for 45.4 percent of the cluster's total engagement, so treat 470 as the honest center and the total as noise. The median holds under the other two concentration checks.

*Rule fired: the double-cite rule moved this link slot here from Monday. Link posts fire a format-confound flag on both Saturday (1.58 times normal share) and Monday (1.67 times). Tuesday and Thursday are your only link-clean ranked days.*

---

## Slot 3: Thursday, 2026-08-13

**Time:** midday band, 11am to 5pm, America/Los_Angeles | **Confidence: Tier 1**
**Checks:** Concentration checked, clean. Format checked, no confound. This is the only slot this week that gets a clock time, because Thursday midday is the only window in your entire best-windows table that came through both checks clean.
**Note on the two numbers:** Thursday's day-level median is 540, and Thursday midday's is 355. The difference is Thursday evening at 613, which your time read excluded from ranking entirely because one post, your May 7 pantry story, is 58.4 percent of that window's total engagement. So this slot sits in the day your file ranks first and in the window inside it your file can defend, and those are two different numbers. Both are printed so you can decide.
**Format:** photo | **Hook:** Question Open | **Topic:** Closets
**Untested axes:** 0 of 4

**Template used:** `What is the one {small container} you would not let a {guest} open?`

---

**Caption (398 characters, target 251 to 400):**

> What is the one closet you would not let a house guest hang their coat in?
>
> Everyone has one, and it is never the biggest closet or the one in the photos.
> It is the closet holding things you have not decided about: the folding chairs, the coat that fits nobody, and a humidifier you have never filled.
> Open it this weekend with a timer and one bag. Not to organize it. To find out what is in there.

---

**because: time** Thursday is rank 1 of your 4 rankable days, 17 posts, median 540, concentration checked clean and format checked with no confound. Thursday midday is 7 posts at a median of 355, and it is the only window in your best-windows table that cleared both checks. Photo is 4 of 17 Thursday posts at a representation ratio of 0.83, well under the 1.5 threshold, so this pairing is confirmed clean rather than merely unflagged.
**because: format** Photo is 28.3 percent of your posts and 26.7 percent of your top 15, a lift of 0.94, which is Tier B. It gets this slot because your only Tier A format, video, is capped at 2 slots per week. Photo beat text on the tie-break that separates them: photo is 3 of your top 10 and 4 of your bottom 10, text is 1 of your top 10 and 3 of your bottom 10. Identical medians, identical counts, different failure rates.
**because: hook** Question Open is your only ranked archetype that over-indexes in your top quartile: 18.3 percent of your posts and 26.7 percent of your top 15, a lift of 1.46, at 11 posts and a median of 610, the highest median of any rankable archetype in your file. Your best one, at 902, is a photo, which is why these two are paired. (Your structural read also shows question marks earning 610 against 402, and that is the same 11 posts restated, not separate evidence, so it is not cited here as a second reason.)
**because: topic** Closets, 10 posts, median 530 against your corpus median of 458.5, and the only topic cluster in your file with real volume and zero concentration flags. It spans your lowest post (208) and your highest (1,904) and still comes through all three checks. Your audit's What works finding 1 and 30-day list item 6.

*This is the clean slot of the week: zero untested axes. If it lands, four separate pieces of evidence held. If it misses, all four are worth re-examining, which is exactly what a zero-untested slot buys you.*
*One note on rate: this is one Closets post this week, against your historical rate of 0.54 Closets posts per week (10 posts across 130 days). That is above your rate, not at it. Your 30-day list item 6 says keep the Closets rate where it is, so hold at roughly one every other week across the month.*

---

## Slot 4: Saturday, 2026-08-15

**Time:** day-level slot, no clock time | **Confidence: Tier 3**
**Checks:** Saturday carries two flags from two different checks. First, mean over median 1.73, carried partly by your 3,402-engagement post from June 6, so 388 is the number that describes a normal Saturday post. Second, a format-confound flag: link posts are 2 of these 19, 1.58 times their normal share of your account, and link is your strongest format at a median of 795 against your corpus median of 458.5.
**Posting warning:** neither Saturday window is clean. Saturday midday has a link post at 2.5 times normal share, sitting at 402, essentially at that window's median of 384. Saturday morning has a link post at exactly 1.5 times normal share, and that post earned 244, second-lowest of the 10 posts in that window, so link is over-represented there while pulling the number **down**, not up. Neither of those is a reason to avoid a time of day. Both are a reason not to read either window as a finding yet.
**Format:** video, medium band, 41 to 70 seconds | **Hook:** Permission Grant | **Topic:** Pantries
**Untested axes:** 2 of 4 (hook, topic)

**Template used:** `You are allowed to keep the {ugly or imperfect thing} that works. Nobody is coming to inspect your {domain}.`

---

**Caption (287 characters, target 251 to 400):**

> You are allowed to keep cereal in its own bag. Nobody inspects pantries.
>
> Decanting is a choice, not a rule. It is beautiful, it takes ninety minutes, and it hides the expiration date.
> The pantry that survives is the one you can put groceries into in four minutes with a kid on your hip.

**On-camera script (target 41 to 70 seconds, this runs about 57):**

> You are allowed to keep cereal in its own bag. Nobody inspects pantries.
>
> Decanting is a choice, not a rule. It looks incredible, it takes about ninety minutes, and it throws away the expiration date printed on the box.
> Here is what I actually do in a client pantry. Bags stay bags. Boxes stay boxes. One bin per category, and the bin is the limit.
> The only things that get decanted are the ones you reach for daily and the ones that spill. Flour, rice, cereal you eat every morning.
> Everything else keeps its packaging, and the pantry survives, because the test of a pantry is not the photo. It is whether you can put groceries away in four minutes with a kid on your hip.

---

**because: time** Saturday is rank 3 of your 4 rankable days, 19 posts, median 388, with the two flags described above. It gets a slot rather than being skipped because it is a ranked day and its flags are one concentration flag plus one format-confound flag, which is not the two-concentration-flag combination that excludes a bucket.
**because: format** Video, your only Tier A format, lift 1.43, median 585. The medium band (41 to 70 seconds) is 5 posts and it is the band your audit refused to turn into a recommendation, because it flags on two of three concentration checks and what is actually inside it is your two highest-engagement posts in the entire capture: the 4,118 pantry story at 47 seconds and the 3,402 four-rules post at 64 seconds. Your 30-day list item 2 asks for one more video in that band, structured like those two. This is a deliberate test of a coincidence, not a bet on a proven band, and the draft above is built to that spec: a specific number of clean beats, under 70 seconds.
**because: hook** Permission Grant is #4 on your hook analyzer's test list and the only UNEXPLORED archetype it found evidence for. The latent-fit test found it in the body of two of your posts, verbatim, and never once as your first line: "You are allowed to make a temporary place work for you" (line 3 of your renters post) and "Nobody has ever opened a linen closet and graded your corners" (line 3 of your fitted-sheets post). It is also the only archetype in your analysis that lowers the reader's workload in the first line instead of adding to it.
**because: topic** Pantries, 3 posts, median 712, the highest median in your entire topic table and unrankable at n=3, so it is untested rather than proven. It takes this slot because your two clean rankable topics went to slots 2 and 3, and stretching a flat topic would have been worse than naming an untested one.

*Rule fired: Curiosity Gap sits above Permission Grant on your test list and was skipped here. Its only evidence is a 2-post bucket carrying two concentration flags, and your hook analyzer notes those flags are close to automatic at n=2. Permission Grant's evidence is a different kind: two verbatim instances in your own post bodies. Not a bigger number, a better one.*
*Format pairing note: Saturday's confound flag names link, not video. Video's own representation on Saturday was never printed upstream. This pairing is not flagged and it is also not independently confirmed clean.*

---

## Week summary

**Slot arithmetic.** 3 from your cadence of 3.23 posts per week, plus 1 experimental. Your time read ranked 4 days, so the day cap did not cut anything. Final: 4 slots.

**Format mix.** video 2, photo 1, link 1, text 0, album 0, against your capture's photo 28.3 percent, text 28.3 percent, video 23.3 percent, album 13.3 percent, link 6.7 percent. Two deliberate divergences. **Album gets zero slots**: it is 13.3 percent of your output and 0 of your top 15, which is your audit's What does not work finding 1 and 30-day list item 3. **Link gets 25 percent of this week against 6.7 percent of your capture**, because it has the highest lift in your file at 2.00 and the highest median at 795, and it needs one more post to clear the 5-post ranking floor.

**Hook rotation.** 4 distinct archetypes across 4 slots. 2 proven, 2 experimental. Your file supports exactly two proven archetypes: Question Open, the only ranked archetype that over-indexes in your top quartile, and Bold Claim, your only small bucket with zero concentration flags. The other two slots are experimental by arithmetic, not by choice. **Zero slots for Problem Callout**, which is 28.3 percent of what you write and 13.3 percent of what works, and **zero for Direct Address**, which is 15 percent of what you write and 0 percent of your top 15.

**Time tiers.** 1 at Tier 1 (clock time, both checks clean: Thursday midday). 1 at Tier 2 (day-level, clean: Tuesday). 2 at Tier 3 (day-level, carrying flags: Saturday, Monday). 4 Tier 4 values were named and not scheduled: Thursday evening, Wednesday, Friday, Sunday.

**Trajectory.** Your audit calls your capture rising, an earlier-half median of 402 against a later-half median of 530, a ratio of 1.32. It cannot separate better content from a bigger audience, because PostSnag does not capture follower history. This calendar does not change anything on the basis of that line, and it does not add volume on the strength of it.

**Flags this week inherited.** 19 flags read across the three artifacts. 14 print on a slot. Of those, 1 also moved a slot and 1 also excluded a destination for that move without moving anything on its own slot. 5 name a value this calendar did not use.

1. video, mean/median 1.89 (audit) | slots 1 and 4 | caveat
2. link, checks not checked at n=4 (audit) | slot 2 | caveat, format axis untested
3. medium duration band, 2 of 3 checks (audit) | slot 4 | caveat, deliberate test
4. short duration band, unrankable n=4 (audit) | slot 1 | caveat, band untested
5. Bins & Containers, top-share 45.4% (audit) | slot 2 | caveat
6. Labels & Systems, 2 flags (audit) | none | value not used
7. Kitchen & Counters, tested and flat (audit) | none | value skipped, printed
8. Story Cold Open, 2 flags (hook) | none | value not used
9. Number Promise, 2 flags (hook) | none | value not used
10. Curiosity Gap, 2 flags at n=2 (hook) | slot 4 | **skipped in the test list**, printed on slot 4
11. Command, 2 flags (hook) | none | value not used
12. question marks double-counting Question Open (hook) | slot 3 | not cited as separate evidence
13. Saturday, divergence 1.73 (best-time) | slot 4 | caveat
14. Saturday, link confound 1.58x (best-time) | slot 4, plus **excluded Saturday as a destination** for the link the double-cite rule moved off Monday (Saturday's own format, video, never carried link, so nothing moved on Saturday itself)
15. Monday, link confound 1.67x (best-time) | **moved a slot**, plus caveat on slot 1
16. Tuesday-Evening, median-shift 26.7% and link confound 2.5x (best-time) | slot 2 | why it is day-level, and the posting warning
17. Saturday-Midday, link confound 2.5x (best-time) | slot 4 | posting warning
18. Saturday-Morning, link confound 1.500, post pulling **down** (best-time) | slot 4 | posting warning, with its direction
19. Thursday-Evening, excluded on 2 concentration flags (best-time) | slot 3 | named as why the slot is midday

**Cut this one first.** Slot 1, Monday. It is your lowest-median rankable day at 341, that median is partly one strong link post, and the slot carries 2 untested axes. If you get three posts out this week instead of four, drop Monday and keep Tuesday, Thursday, and Saturday.

**Upstream recommendations this week consumed.**

| Item | Status |
|---|---|
| Audit 30-day 1: write 3 more link-style posts | **1 of 3**, slot 2. Two remain for the next two weeks. |
| Audit 30-day 2: one more medium-length video, 41 to 70 seconds | **consumed**, slot 4 |
| Audit 30-day 3: cut album, reassign to photo or video | **consumed**: album 0 of 4 slots, video 2, photo 1 |
| Audit 30-day 4: cap new long-form videos at 70 seconds | **consumed**: both video slots are under 70 seconds |
| Audit 30-day 5: write 3 to 4 more Kids' Spaces posts | **1 of 3 to 4**, slot 1 |
| Audit 30-day 6: keep the Closets rate where it is | **consumed**, slot 3, with the rate note attached |
| Audit 30-day 7: test one post on Wednesday, Friday, or Sunday | **declined this week**, two reasons, deferred with a design. See below. |
| Hook test list 1: Confession | **consumed**, slot 1 |
| Hook test list 2: Bold Claim | **consumed**, slot 2 |
| Hook test list 3: Curiosity Gap | **skipped**, 2 concentration flags at n=2 |
| Hook test list 4: Permission Grant | **consumed**, slot 4 |
| Hook test list 5: Contrarian Take | **not reached**, 4 slots and 4 archetypes. Next week. |

**Why item 7 was declined, and how to do it properly.** Two independent reasons. First, this week caps at 4 slots because your time read ranked 4 days, and Wednesday, Friday, and Sunday each have 1 post in 130 days. There is no fifth slot to put one in. Second, even if there were: your hook evidence supports 2 proven archetypes and your topic evidence supports 2 proven clusters, so every slot after the second is already carrying 2 untested axes. Add an untested day and that slot has 3, and if it underperforms you will not know whether it was the day, the hook, or the topic.

**The design that works:** next week, put one post on Wednesday with photo, a Question Open hook, and a Closets topic. Every other axis proven. Then the day is the only variable and the answer is readable.

**What to do after.** Post them. Then two specific numbers are worth watching, and both are one post from changing state:

- **Link is at 4 posts.** Slot 2 makes it 5, which clears the 5-post ranking floor. Your highest-median format stops being unrankable and starts being a finding.
- **Bold Claim is at 3 posts.** Slot 2 makes it 4. One more after that and it clears the floor too, which is exactly what your hook analyzer asked for: "Write two more this month and it clears the ranking floor, at which point you will know rather than suspect."

Capture the profile again in 30 days, which at 3.23 posts per week is about 14 more posts, rerun all three upstream skills, and check those two buckets first.

---

## What this calendar is standing on

This calendar measured nothing. It allocated a week from three artifacts that did the measuring, and every number above traces to a line in one of them. Sources: `facebook-profile-audit`, `facebook-hook-analyzer`, and `best-time-to-post-reader`, all three run on the same 60-post capture, 2026-03-21 to 2026-07-28, 130 days. All three headers, all three corpus medians, the posting-day counts, and the format inventory were cross-checked and matched before any allocation ran.

All three artifacts ran in full mode, so nothing here is degraded by lite mode. Your timezone was confirmed as America/Los_Angeles in the time read, which is the only reason any slot on this calendar carries a clock time.

Six of the sixteen axes across these four slots are untested: two hooks drawn from your test list rather than your rankings, two topics under the 5-post floor, one format under the floor, and one hook from a 3-post bucket. Every one of them is marked on its slot. No slot carries more than two.

Two of your ranked buckets were flagged for format confounds involving link posts, and rather than caveating those pairings this calendar moved the link slot off both of them. Two other slots pair video with days whose confound flags named link, and your time read did not print video's own representation on those days, so those pairings are unflagged and not independently confirmed. That distinction is printed on both slots.

**Caption-length check, against your own measured word band, not just a character bucket.** Slots 1, 2, and 3 run past the 38-to-69-word caption band `creator-voice-skill-builder` measured directly from your writing, and slot 1's sentence rhythm runs past your observed 16.3-words-per-sentence maximum. Tighten those three before posting; this run did not silently rewrite them for you, because that would hide the miss instead of naming it.

Not in your export, so not in this plan: sponsored or paid-partnership flags, so if any upstream finding is standing on a boosted post, this plan inherited that and cannot see it. Reach or impressions, so no slot here predicts how many people will see anything. Per-emoji reactions. Comment text. Follower history over time.

PostSnag captures what you scrolled, so this plans from a sample of the account, not its full history.

**Drafts only. You post them.** No publishing, no scheduling, no account access.

Analysis based on 60 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-content-calendar-builder

---
---

# APPENDIX: SOLO MODE on the free-tier slice

Run against `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv`, the most recent 30 rows of the same account, with no upstream artifacts supplied. This is what a first-time user gets before they download the other three skills, and it is included so nobody has to guess how honest the degradation is.

The user supplied three topics: **pantries, closets, kids' spaces.** The timezone question was asked and not answered.

## The three lite reads

**Audit-lite.** 30 posts, 2026-05-30 to 2026-07-28, 60 days. Lite mode ON. Corpus median 530.0. Top quartile k=7, cut value 902. Posts per week 3.5.

| Type | n | median | share of corpus | share of top 7 | lift | Tier |
|---|---|---|---|---|---|---|
| video | 7 | 604 | 23.3% | 2 of 7 | **1.22** | A |
| photo | 8 | 597.5 | 26.7% | 2 of 7 | **1.07** | A |
| link | 2 | 1,295 | 6.7% | 2 of 7 | **4.29** | D (n<5) |
| text | 8 | 396.5 | 26.7% | 1 of 7 | 0.54 | B |
| album | 5 | 355 | 16.7% | 0 of 7 | 0.00 | C |

No topic clustering. No duration bands. No trajectory. No 30-day list.

**Hook-lite.** Same 12 archetypes and the same precedence ladder as the real skill, so these numbers are reproducible against a real hook-analyzer run on this file.

| Archetype | n | median | share of top 7 | lift | Rankable |
|---|---|---|---|---|---|
| Question Open | 6 | 699.5 | 1 of 7 | 0.71 | yes |
| Problem Callout | 6 | 377 | 1 of 7 | 0.71 | yes |
| Story Cold Open | 5 | 344 | **0 of 7** | 0.00 | yes |
| Number Promise | 4 | 630 | 1 of 7 | 1.07 | no |
| Direct Address | 4 | 503 | 0 of 7 | 0.00 | no |
| Bold Claim | 2 | 1,046.5 | 2 of 7 | 4.29 | no |
| Confession | 1 | 1,904 | 1 of 7 | 4.29 | no |
| Curiosity Gap | 1 | 1,206 | 1 of 7 | 4.29 | no |
| Command | 1 | 238 | 0 of 7 | 0.00 | no |

**Pool 1 is empty.** No rankable archetype in this slice reaches a lift of 1.00. On the full 60-post file, Question Open reaches 1.46. On the most recent 30, it drops to 0.71, because her top quartile at this depth is one post from each of six archetypes plus two Bold Claims.

**Pool 2 is empty.** The only candidate is Number Promise at n=4, median 630, and it flags twice: top-share 67.8 percent (its 3,402 post out of a 5,017 bucket total) and mean over median 1.99 (mean 1,254.25 against median 630). Direct Address at n=4 sits at 503, below the 530 corpus median.

**Pool 3, solo fallback** (unrankable, median above the corpus median, sorted by median, skipping 2-flag buckets): Confession 1,904, Curiosity Gap 1,206, Bold Claim 1,046.5. Number Promise skipped on its two flags.

**Time-lite.** Day-of-week only. Timezone not confirmed, so relative language only, and no clock time anywhere.

| Day | n | median | Flags |
|---|---|---|---|
| Tuesday | 8 | 677.5 | Concentration checked, clean. **Format: not checked.** |
| Thursday | 7 | 466 | Concentration checked, clean. **Format: not checked.** |
| Saturday | 9 | 398 | Mean/median 2.53, carried by the 3,402 post from June 6. **Format: not checked.** |

Too small to rank: Monday 3 / 305, Wednesday 1 / 566, Friday 1 / 388, Sunday 1 / 560.

## The allocation

```
base          = round(3.5) = 4
experimental  = 1
total         = 5
cap: ranked days = 3
total = min(5, 3) = 3
```

**The cap cuts two slots.** Solo mode on a free-tier export ships a 3-slot week where chain mode on the deeper capture shipped 4.

Formats: 2 proven across Tier A, proportional to top-quartile share, which is 2 of 7 for both video and photo, so 1 each. Experimental: link, Tier D, lift 4.29.

Hooks: Pools 1 and 2 are both empty, so **all three slots are hook-experimental**, drawing Pool 3 in order: Confession, Curiosity Gap, Bold Claim.

Pairing: the co-occurrence override is unavailable, because it reads the hook analyzer's top-10 template list and solo mode does not build one. Falling back to which format each archetype's own instances used in this slice: Confession's single instance is a video, Bold Claim's higher instance (1,188) is a link, Curiosity Gap's single instance (1,206) is text, which is not allocated.

| Slot | Day | Time | Format | Hook | Topic | Untested (of 3) |
|---|---|---|---|---|---|---|
| 1 | Tuesday | day-level, relative only | video | Confession | pantries | 1 |
| 2 | Thursday | day-level, relative only | photo | Curiosity Gap | closets | 1 |
| 3 | Saturday | day-level, relative only | link | Bold Claim | kids' spaces | 2 |

One full draft, slot 1, to show that the drafting method is unchanged:

**Caption (280 characters, no target available):**

> I still buy the same spice twice and I have done this for eleven years.
>
> Cumin. Always cumin. Three jars, right now, on a shelf I built and labeled myself.
> It is not a shelf problem. My pantry is fine. It is that I leave the house without looking, and no system fixes not looking.

**On-camera script:** no duration instruction. Solo mode does not compute duration bands, so there is no band to write to. Keep it short and check it against your own file.

The template came from `references/hook-template-mini.md` (condensed; full 44-template library in `../../facebook-hook-analyzer/references/hook-template-library.md` and the bundle) rather than from your own top 10, because solo mode does not build the top-10 template list.

## What solo mode cost, item by item

1. **Three slots instead of four**, because the free slice ranks 3 days instead of 4.
2. **No clock time on any slot.** Chain mode gave Thursday a real band (midday, 11am to 5pm) because that window came through both checks clean. Solo mode never builds the 28-cell grid, so there is no window to award.
3. **The double-cite rule never runs.** Every format-confound cell above reads **not checked**, and slot 3 puts a link post on Saturday without ever testing that pairing. Be precise about what this means: it is not that solo mode checked Saturday and cleared it. It is that solo mode never looked. On the fuller 60-post capture of this same account, the format-confound check fires on 5 of 8 ranked buckets and it is the flag that moved the link slot off Saturday and off Monday. Unchecked is not the same as clean.
4. **Pool 3 loses its best member.** Chain mode's fourth slot was Permission Grant, found by the latent-fit test, which searches post bodies for archetype markers and found two verbatim instances she had never used as a first line. Solo mode does not run that test, so its Pool 3 is just the small buckets sorted by median, and Permission Grant does not appear anywhere.
5. **Every hook is experimental.** Pools 1 and 2 are both empty at this depth. Chain mode had two proven archetypes.
6. **Topics are whatever the user typed.** No cluster, no median, no flag, no ranking. The confound budget counts three axes instead of four as a result, which means a solo-mode slot that looks in budget would be over budget in chain mode: add a real topic axis to slot 3 and it carries three untested axes, not two.
7. **No character targets.** Solo mode skips the structural read, so the drafts are not steered toward the caption-length band that outperforms for this creator by 1.80x on the fuller file.
8. **Library templates instead of her own.** The top-10 template list is a hook-analyzer output. Without it, drafts use `references/hook-template-mini.md` library patterns, which are good and are not hers.

Eight losses, each one nameable. That is the honest version of "chain mode is better": not a warning, a list. Run the three skills on this same export, paste their outputs back here, and every item above changes state.