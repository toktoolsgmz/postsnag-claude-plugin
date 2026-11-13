# rubric.md

The full method for Facebook Content Calendar Builder. Four sections, in the order the run executes them: the input contract, the allocation logic, solo mode, and the drafting method.

This skill is the only one in the catalog that consumes other skills' finished outputs as its primary input. Section 1 is therefore the most important section in the file: get the contract wrong and every number downstream is confidently wrong.

Version 1.0 | 2026-08-04

---

# SECTION 1: THE INPUT CONTRACT

**Compute every number in this analysis with code.** The cross-check in 1.1, the lift and slot-count arithmetic in Section 2, and solo mode's inline reads in Section 3 all follow that rule; this skill does not recompute the upstream numbers it cites, but every number it does compute or compare, it computes with code, and a wrong number presented with confidence is worse than no number.

## 1.0 What this skill reads, in one paragraph

Chain mode reads three finished artifacts: a `facebook-profile-audit` output, a `facebook-hook-analyzer` output, and a `best-time-to-post-reader` output, all three produced from the same PostSnag export. It reads named sections out of each. It does not recompute anything they computed. It does not re-parse the CSV in chain mode at all. Its entire job is allocation, propagation, and drafting on top of numbers three other skills already earned.

The field-by-field mapping lives in `chain-input-map.md`, 46 rows, one per consumed field. Section 1 here gives the rules that govern the whole contract. Walk both before allocating anything.

---

## 1.1 The cross-check that runs before anything else

Read these three lines, one from each artifact's header:

```
audit header:       "{N} posts, {first date} to {last date}, {span} days."
hook header:        "{N} posts, {first date} to {last date}, {span} days."
best-time header:   "{N} posts, {first date} to {last date}, {span} days."
```

**All three must match on N, on both dates, and on span.**

If any of the three disagrees, **STOP the run**. Print what each artifact said, name which one is the odd one out, and ask for a rerun on a single export. Do not build a partial calendar, do not take the majority, do not take the smallest.

The reason is not fussiness. If the audit ran on 60 posts and the time read ran on 30, the calendar would allocate formats from a 60-post distribution onto days ranked from a 30-post file, and every evidence line on the output would be a true sentence pointing at a false pairing. That failure is invisible on the page, which is exactly why it gets a hard stop instead of a caveat.

**The one permitted exception:** an artifact whose header is missing entirely (the user pasted only part of it). Treat that as an absent section, not a mismatch, and follow the absence rules below.

---

## 1.2 What each upstream section drives, by artifact

Full detail with absence and flag behavior per field: `chain-input-map.md`. The summary:

### From `facebook-profile-audit`

| Section consumed | What it drives here |
|---|---|
| Header line (N, dates, span, format mix, corpus median) | the cross-check, the pointer-line N, and the corpus median every comparison on this calendar uses |
| Lite-mode banner, if present | forces day-level slots only and caps the week at the number of ranked days |
| **Cadence** (posts per week, posting-day counts) | the base slot count, and a second cross-check against the time read's day counts |
| **Format distribution** (per-type n, median, share of corpus, share of top quartile, the check columns, Rankable) | the format mix, via the lift tiers in section 2.2 |
| Top-10 versus bottom-10 line | the tie-break when two formats tie on lift, median, and n |
| **Topic clusters** (per-topic n, median, check columns, Rankable) | the topic assigned to each slot |
| Video: views and duration (duration bands with n, median, checks) | the duration instruction on every video slot |
| What works / What does not work (three findings each) | the exclusion list, and the promotion of an untested standout into an experimental slot |
| Trajectory, if present | one line on the week summary. It does not change the slot count. |
| **Your 30-day list** (the numbered items) | the experimental slot's content, and the consumed-recommendations checklist in the week summary |

### From `facebook-hook-analyzer`

| Section consumed | What it drives here |
|---|---|
| Header line | the cross-check |
| **Your hook patterns** (archetype, posts, median, share of top quartile, concentration flags) | Pool 1, the ranked archetypes eligible for a proven slot |
| **Too small to rank** line | Pool 2, the small-n clean archetypes |
| **Over-invest / under-invest table** | the Pool 1 lift screen, and the "stop writing this one" line in the week summary |
| **Your top 10 hooks, as templates** (the verbatim hook, its archetype, the post's format, and the abstracted Template line) | the fill-in template each draft is written from, and the format co-occurrence override in section 2.5 |
| **5 archetypes to test next** (the ordered list, its UNDERUSED / UNEXPLORED labels, the latent-fit evidence) | Pool 3, the experimental hooks |
| The structural read (hook length and caption length buckets with medians) | the character targets written onto every draft |
| Honesty footer (concentration flags restated) | copied into this calendar's footer |

### From `best-time-to-post-reader`

| Section consumed | What it drives here |
|---|---|
| Timezone line | whether any slot can carry a clock time at all |
| Date-only banner, if present | forces every slot to day-level |
| Lite-mode banner, if present | forces day-level slots and caps the week at the number of ranked days |
| **Your best days** table (day, posts, median, Flags) | the slot days, in rank order, and each slot's confidence tier |
| Your best days, "Too small to rank" line | the Tier 4 day list. Never a slot time. |
| **Your best windows** table (window, posts, median, Flags) | the clock time on a slot, when one is available |
| The excluded-window note (a window carrying 2 or more concentration flags) | Tier 4. Named once on the calendar so the user knows why a higher-median band was skipped. |
| Early signal section, in lite mode | may be named once as a test. Never becomes a scheduled clock time. |
| **Format-confound flags anywhere in either table** | the double-cite rule in section 2.7 |
| Where you post versus where you win | the schedule-gap line, and the one-slot cap on the over-posted day |

---

## 1.3 When an upstream section is missing

The user pasted part of an artifact, or ran a version that omitted a section. Three behaviors, and the calendar always says which one fired:

**Behavior A, degrade with a named fallback.** The section has a defensible substitute inside the artifacts you do have. Use it, and print the substitution on the slot: "format mix derived from median against corpus median, because the audit's top-quartile share column was not supplied."

**Behavior B, mark the axis untested.** No substitute exists, but the calendar can still ship. The axis is assigned from the user or from the highest-median unranked candidate, and it counts against the confound budget in section 2.8.

**Behavior C, refuse.** Three sections have no fallback at all:

| Missing section | Why there is no fallback |
|---|---|
| The hook analyzer's **Your hook patterns** table | With no archetype ranking there is no hook to assign and no template to draft from. The calendar asks for the hook analysis rather than drafting from a general idea of what a good hook is. |
| The time read's **Your best days** table | With no ranked day there is no defensible date for anything. A calendar whose dates are arbitrary is a list. |
| The audit's **Format distribution** table | With no format evidence, every slot's format is a guess, and format is the axis that costs the most to get wrong (a video is an afternoon, a text post is ten minutes). |

Refusal is one paragraph: what is missing, which skill produces it, and what the calendar could ship if the user supplies it. Not an apology.

---

## 1.4 When an upstream ran in lite mode

Lite mode is not a caveat here, it is a mode change. Any upstream banner reading `**Lite mode.**` triggers all of the following, and the banner is reprinted at the top of this calendar with the upstream skill named:

1. **No slot carries a clock time.** Every slot is day-level. This is the single loudest consequence and it is the one users notice.
2. **The week is capped at the number of days the time read ranked.** On a typical free export that is 3 of 7. A four-slot cadence and a three-day cap produce a three-slot week, and the calendar says which slot got cut and why.
3. **The best-windows table is absent by design upstream.** Do not go looking for it, do not treat its absence as a missing section, and do not promote the Early signal cell into a scheduled time. It may be named once, on an experimental slot, as a thing to test on purpose.
4. **Topic axes are mostly untested.** On a 30-post capture the audit typically clears 1 topic cluster of 10. Every slot beyond the first is drawing an unranked topic, which counts against the confound budget.
5. **No trajectory line.** The audit omits it below 90 days of span, so the week summary omits it too rather than inferring one.

**A lite-mode upstream never silently produces a full-mode calendar.** If any of the three artifacts is in lite mode, the calendar is in lite mode. There is no partial version of this.

---

## 1.5 Flag propagation: the rule this skill exists to get right

This is the heart of the skill. Read it twice.

Every one of the three upstream skills attaches caveats to findings, glued inside the sentence rather than trailing in a parenthetical, precisely so the caveat cannot be separated from the number. **A content calendar is the exact place where that separation happens**, because a calendar's job is to compress a report into an instruction, and compression is how caveats die. "Tuesday evening, median 712" is a much cleaner-looking slot than "Tuesday evening, median 712, which drops 26.7 percent to 522 if one link post is removed, and that link post is 2.5 times a link post's normal share of the account." The first one is what a calendar wants to print. The second one is what is true.

### The five propagation rules

**Rule 1. A flagged finding is used, and its caveat travels onto the slot.**

Flagged does not mean discarded. An upstream that wanted a finding discarded would have excluded it from its own ranking table, and the ones it excluded are handled by rule 4. A finding that was ranked with a flag was ranked on purpose: the upstream decided the number was real and the caveat was material. The calendar honors both halves. The number becomes the slot; the caveat becomes a line printed on the slot.

**Rule 2. The caveat travels with its DIRECTION, not just its existence.**

This is where a careless implementation produces a false statement out of a true flag. A format-confound flag measures **representation**, not **direction**: it says a format is over-represented in a bucket, not that the format lifted the bucket. The time reader is explicit about this and worked an example on it: on Saturday morning, the over-represented link post earned 244, second-lowest of the 10 posts in that window, so link is over-represented there while pulling the median **down**.

If the calendar prints "this window may be inflated by link posts" on that slot, the calendar has told the user something false using a flag that was true. So:

```
When copying a format-confound caveat onto a slot, copy three things:
  1. the type named and its representation ratio
  2. that type's own median ratio against the corpus median
  3. WHERE the over-represented post sits inside the bucket (top, middle, bottom)
If the upstream stated the third thing, restate it. If the upstream did not state
it, write "the upstream did not say where that post sits in the window", and do
not guess the direction.
```

**Rule 3. A slot never carries a caveat-free restatement of a caveated finding.**

Concretely: the calendar may not write "Thursday, your best day" when the upstream row for Thursday carries a flag. It writes the day, the median, and the flag, in the same sentence. If a slot's caveat line is empty, that means both upstream checks ran on that row and both cleared, and the slot says so explicitly: "Concentration checked, clean. Format checked, no confound." It never says "none", and it never says nothing, because on a row a user is about to act on, silence and clean look identical.

**Rule 4. Anything the upstream excluded from ranking is Tier 4 and never becomes a slot time, a slot format, or a slot hook.**

Two upstream states produce Tier 4:

- **Excluded from ranking** (a bucket carrying 2 or more concentration flags). The upstream already made this call. The calendar does not relitigate it. Example: a window whose median is the highest in the file but which the time reader excluded because one post is 58.4 percent of the window's total engagement. It does not get scheduled. It gets named once, on the calendar, so the user understands why the higher number was skipped.
- **Too small to rank** (a bucket under the 5-post floor). Not evidence for a slot. Eligible only as an experimental value, subject to the confound budget.

**Rule 5. Flags that recommend a MOVE are executed, not printed.**

One flag type does more than caveat: the format-confound flag identifies a specific pairing of format and time slot that the upstream evidence cannot separate. Printing a caveat about it and then scheduling that exact pairing anyway is the worst available behavior, because it reproduces the confound the evidence warned about while looking rigorous. That flag drives the double-cite rule in section 2.7, which moves the slot. See there.

### The propagation ledger

Every run keeps one, and it becomes the numbered flag list in the week summary:

```
For each flag read from any upstream artifact:
  source artifact | source section | the flagged bucket | the flag type
  | which slot inherited it | how it appears on that slot (caveat line / moved
  the slot / excluded the value)
```

Any flag with no entry in the "which slot inherited it" column is a flag on a value this calendar did not use, and the ledger says so. A flag that vanishes with no disposition is a bug.

---

## 1.6 Sanity checks that run before allocation

Three, all cheap, all worth it:

1. **Day-count cross-check.** The audit's Cadence section lists posting-day counts. The time read's best-days table plus its too-small-to-rank line lists the same counts. They must match day for day. A mismatch means the two artifacts ran on different files even if their headers agreed. Stop.
2. **Corpus median cross-check.** All three artifacts print a corpus median. Same number, all three, or stop.
3. **Format inventory cross-check.** The audit's format mix in its header must list the same types with the same counts as its own format distribution table. This catches a truncated paste.

---

# SECTION 2: ALLOCATION LOGIC

Every allocation rule below produces both a value and a citation. **A slot value with no upstream citation does not ship.** If a rule cannot name the line it came from, the axis is marked untested instead of guessed.

The week is always the next full Monday-to-Sunday week after the run date, so nothing lands in the past.

---

## 2.1 Slot count

```
1. base = round(posts_per_week), half up, read verbatim from the audit's
   Cadence section ("{N} posts across {span} days, {posts_per_week} posts per week")
2. clamp base to [3, 6] (working number, labeled, not a platform fact). Below 3
   a week is not a plan. Above 6 leaves no room for the experimental slot
   under the one-slot-per-day cap.
3. experimental = 1 if base <= 4, else 2 (working number, labeled, not a
   platform fact; see the proportional-risk reasoning below)
4. total = base + experimental
5. cap: total = min(total, number of days in the time read's best-days table)
   One slot per day, maximum. A day the time read did not rank is not a day
   this calendar schedules on.
6. cap: total = min(total, 7)
```

**Why the experimental slots are added and not substituted.** Substituting would spend a proven slot to run a test, and the cadence evidence covers the proven slots specifically. One extra post in a week sits inside the variance the capture already shows: a creator averaging 3.23 posts per week has written plenty of 4-post weeks. Adding one is inside the observed range. Adding three is a different creator.

**Why 1 experimental slot below 5 and 2 at 5 or above.** One experiment in a 4-slot week is 25 percent of the week. Two in a 7-slot week is 28.6 percent. Same proportion, so the rule scales the risk rather than the count. Below a quarter of the week you learn too slowly to bother; above a third, one bad week of experiments costs you the month.

**When step 5 cuts the week, say so on the calendar, with both numbers:** "Your cadence supports {total} posts a week. Your time evidence supports {days} days. This week is {days} slots, because a slot with no defensible day is a guess with a date on it."

---

## 2.2 Format mix, the proportional method

Read the audit's **Format distribution** table. Every format has a share of the corpus and a share of the top quartile printed in it. Compute:

```
lift(type) = (share of top quartile) / (share of corpus)
```

Both shares come straight from the audit's own columns. Report lift to two decimals. This is the audit's own headline method for reading that table ("the quartile finding that matters is composition, not membership"), applied to allocation instead of to prose.

**The tiers:**

| Tier | Condition | What it may hold |
|---|---|---|
| **A** | rankable (n at or above 5) AND lift at or above 1.00 | proven slots |
| **B** | rankable AND 0 < lift < 1.00 | a proven slot only when Tier A is exhausted or capped, and the slot says the format came from Tier B |
| **C** | rankable AND lift = 0 (no presence in the top quartile at all) | nothing. Zero slots. Named once in the week summary with the audit's own finding cited. |
| **D** | not rankable (n under 5) | experimental slots only, never a proven slot |

**Allocating the proven slots:**

```
1. Distribute proven slots across Tier A, proportional to each Tier A format's
   share of the top quartile, normalized to Tier A only, using largest-remainder
   rounding.
2. Cap: no format may hold more than ceil(proven_slots / 2) slots. A week is a
   portfolio, not a bet, and the audit's evidence is a median across a bucket,
   not a guarantee about the next post.
3. Any slot the cap displaces goes to the next Tier A format by lift, then to the
   highest-lift Tier B format.
```

**Allocating the experimental slot's format:** the highest-lift Tier D format, which is usually the "too small to rank, worth testing" finding the audit already promoted into its What works section. If Tier D is empty, the experimental slot takes the same format as the highest-lift Tier A format and its experiment runs on the hook axis instead.

**Tie-breaks, in order.** Two formats tie on lift more often than you would expect, because top-quartile shares come in small integers:

```
1. higher median (from the audit's format table)
2. higher n
3. higher (top-10 count minus bottom-10 count), read from the audit's
   "Top 10 versus bottom 10 by format" line
4. alphabetical, and the calendar says the tie was broken arbitrarily
```

Tie-break 3 is the one that usually resolves it, and it is worth naming why: two formats can have identical medians, identical counts, and identical top-quartile shares, and still differ in how often they land at the bottom. A format that is 3 of the top 10 and 4 of the bottom 10 is a different animal from one that is 1 of the top 10 and 3 of the bottom 10, and only that line in the audit tells them apart.

**Video slots additionally take a duration band** from the audit's Video: views and duration section:

```
- Never assign a duration band the audit reported as its lowest clean ranked band,
  if the audit's 30-day list carried a cap instruction. Honor the cap.
- A band carrying 2 or more concentration flags may be assigned, but only as an
  experiment, and the slot says the band is not a proven recommendation and names
  the specific posts driving it.
- Two video slots in one week never share a duration band. A week that tests one
  band twice tests one thing.
- If the audit's duration section is absent or all bands are under the floor,
  video slots carry no duration instruction and the calendar says so.
```

---

## 2.3 Hook assignment

Build three pools from the hook analyzer's output, in this order.

**Pool 1, ranked and over-represented.** From the analyzer's **Your hook patterns** table crossed with its **over-invest / under-invest** table:

```
n at or above 5
AND (share of top quartile) / (share of posts) >= 1.00
AND fewer than 2 concentration flags on the archetype
```

**Pool 2, small and clean.** From the analyzer's **Too small to rank** line:

```
n between 3 and 4 inclusive (working number, labeled: this skill's screen for
  "small but not automatic", not a platform fact; see the n>=3 reasoning below)
AND zero concentration flags
AND median above the corpus median
```

The n>=3 floor matters. At n=1 or n=2, the concentration check is arithmetically near-automatic and tells you nothing, so a clean result at n=2 is not evidence of cleanliness. Those archetypes belong in Pool 3, which is where the analyzer already puts them.

**Pool 3, the test list.** The analyzer's **5 archetypes to test next**, in the analyzer's own order, which is its own evidence tiering and this skill does not reorder it. Two skips apply:

```
skip any archetype already assigned this week
skip any archetype whose only evidence is a bucket carrying 2 or more
  concentration flags, UNLESS Pool 3 is otherwise exhausted
```

**Assignment:**

```
1. Proven slots draw from Pool 1 first, then Pool 2, highest median first
   within each pool.
2. If Pools 1 and 2 run dry before the proven slots are filled, DO NOT pad with
   a demoted archetype. Convert the unfilled proven slot into a hook-experimental
   slot, draw from Pool 3, and print the reason on the slot: "this slot is
   experimental on the hook axis because your hook evidence supports only {n}
   proven archetypes."
3. Experimental slots draw from Pool 3, top of the list first.
```

**The rotation rule:**

```
No archetype fills more than one slot in a week of 4 or fewer slots.
No archetype fills more than two slots in a week of 5 to 7 slots.
```

A week that opens the same way twice teaches your reader your shape and teaches you nothing. The two-slot allowance at 5 or more exists so a genuinely dominant archetype in a busy week is not artificially suppressed, and even then it is capped, because the point of a week is a readable comparison between openings.

**The single-post screen.** Any archetype the analyzer flagged as carried by one post (2 or more concentration flags) never holds a proven slot. It may hold an experimental slot, and that slot's evidence line states that the archetype's number is standing on one post and names it.

**How many experimental slots, and why.** The experimental slot count comes from section 2.1: one per week below 5 slots, two at 5 or more. Rule 2 above can create additional hook-experimental slots when the proven pools run dry, which is a property of the creator's file rather than a choice this skill makes. On a corpus that supports only two proven archetypes, a four-slot week has two experimental hooks by arithmetic, and the calendar says that out loud rather than dressing two guesses as findings.

---

## 2.4 Topic assignment

Read the audit's **Topic clusters** table.

```
Proven slots take:
  rankable topics (n at or above 5)
  AND median at or above the corpus median
  AND at most 1 concentration flag
  highest median first

Skip, with one printed line: any topic the audit reported as a tested null
  result. Recognition: rankable, zero flags, and a median within 5 percent of
  the corpus median. The line reads "{topic} is measured and flat, not failing.
  A week has better uses." That is the audit's own finding, restated once.

Skip entirely: any topic the audit named under What does not work.

Experimental slots take, in order:
  1. a topic the audit's 30-day list explicitly asked for more of
  2. the highest-median unrankable topic in the table
  and the slot says the topic is untested and names its n.

If the audit's topic table is absent: ask the user for 3 to 5 topics, use them,
and mark every topic axis untested. This is solo mode's permanent state.

No topic repeats inside one week.
```

If the proven pool runs dry before the proven slots are filled, fall to the highest-median unrankable topic and mark that slot's topic axis untested. Do not reuse a topic and do not stretch a topic the audit reported as flat into a finding.

---

## 2.5 Pairing content to slots

Two steps: build the pairs, then match pairs to slots.

**Step 1, the co-occurrence override.** Before pairing by score, check the analyzer's **Your top 10 hooks, as templates** section. Each entry names an archetype and belongs to a post whose format is in the audit. When an archetype's own best-performing instance used a format that is already allocated this week, pair them, and cite the post. That pairing is evidence from the creator's own file rather than an inference from two separate tables.

When two archetypes both co-occur with the same format and only one slot of that format exists, the higher-engagement instance wins.

**Step 2, the evidence score, for everything the override did not settle:**

```
hook points:    3  ranked, over-represented (Pool 1)
                2  small and clean (Pool 2)
                1  experimental (Pool 3)

format points:  3  Tier A
                2  Tier B
                1  Tier D

pair_evidence = hook points + format points
```

**Step 3, match rank to rank.** Sort the time slots by confidence tier (section 2.6), sort the pairs by `pair_evidence` descending, and match position for position. The most confident time in the file gets the most confident content in the file. An experimental pair never occupies the single most confident slot of the week.

**Two hard constraints on the result:**

```
No two slots on the same day share a format.
No two video slots share a duration band.
```

---

## 2.6 Time assignment and the confidence tiers

Read the time read's two tables. **The tier ladder below is a working number: four confidence tiers, labeled, not a platform fact about how many gradations of confidence exist.** It is chosen because it is the smallest ladder that keeps "clock time, both checks clean" separate from "day-level, flagged" separate from "never scheduled", which are the three distinctions this skill's allocation rules actually act on. Applied per slot:

| Tier | Source | What the slot gets |
|---|---|---|
| **1** | a window in the best-windows table, on this slot's day, with **both** upstream checks clean, and a confirmed timezone | a clock time, printed as the upstream's band verbatim |
| **2** | the day itself, ranked, both checks clean, with no clean window available on it | a day-level slot, no clock time |
| **3** | the day itself, ranked, carrying one or more flags | a day-level slot, plus every flag's caveat written onto it with its direction |
| **4** | excluded from ranking upstream, or listed as too small to rank | never a slot time. May be named once on the calendar as a thing not scheduled, and why. |

**The ordering rule that matters: confidence beats specificity.** A clock time is awarded only to a window that came through **both** upstream checks clean. Every other slot is day-level, including slots on days whose windows are ranked but flagged. Say so on the slot: "your highest-median window on this day is {window} at {median}, and it carries {flag}, so this slot is day-level."

This is the time reader's own framing, applied to scheduling: a user should be able to act on the day-of-week table alone and treat the window table as supplementary evidence. A flagged window is a warning, and that is exactly how it is used here:

**Flagged windows become a posting warning on the day-level slot, not the slot's time.** When the chosen day has a ranked-but-flagged window, print it on the slot as an instruction: "This slot is day-level. If you post it in the {band} band you land in {window}, where {the flag, with its direction}. Post this one {the other part of the day}." The user is going to pick an hour whether or not the calendar names one, so a day-level slot that says nothing about the bands has quietly left the user to walk into the flagged one.

**No clock time without a confirmed timezone.** If the time read's header says times are relative only, every slot is day-level regardless of tier, and the calendar says why in one line. Slots may still use band names as groupings ("earlier in the day", "later in the day") because the grouping does not depend on knowing the timezone. Only advice to post at a specific hour does.

**A clock-time slot is the upstream's band, verbatim, never narrowed to an hour.** The time reader measures four bands. Narrowing "midday, 11am to 5pm" down to "post at 1pm" invents a precision that was never in the file, and it is the single easiest way for a calendar to launder a band into a false claim. Print the band and its hours, exactly as the upstream wrote them.

**Counting flags: concentration and format-confound are different checks and are counted separately.** The 2-flag exclusion rule in `_shared/engagement-math.md` section 5 counts the three parts of the **concentration** check only. A bucket carrying one concentration flag plus one format-confound flag is **not** excluded, because the upstream ranked it, and the upstream ranked it knowing both. That bucket is Tier 3 and it carries two caveats. Miscounting this is how a usable day gets thrown away, and throwing away a ranked day is the same error the 5-post floor exists to prevent in the other direction.

**Assignment order:** best-median ranked day first, one slot per day, until the slots or the days run out. Within a tier, higher median first.

**The schedule-gap rule.** If the time read's **Where you post versus where you win** section names a most-posted day that is not the best-median day:

```
1. The over-posted day gets at most one slot.
2. The slot that would have gone there goes to the best-median day, if the
   one-slot-per-day cap allows.
3. The calendar prints the historical share and this week's share, both.
4. When the week is small enough that every ranked day gets exactly one slot,
   the gap closes by evening out rather than by loading the best day. Say that,
   with both numbers, rather than claiming a shift that did not happen.
```

---

## 2.7 The double-cite rule

```
IF a slot's assigned format is the same format that fired a format-confound flag
   on that slot's day or window
THEN the calendar does one of exactly two things and prints which:
   (a) move the slot's format to a day where that format did not fire a confound
   (b) keep the pairing and label the slot a deliberate confound test, which is
       permitted only on an experimental slot
It never places the pair silently.
```

Preference order is (a), then (b). Moving costs nothing; testing a known confound costs a slot.

**Which bucket the rule tests against depends on the slot's tier.** A Tier 1 slot has a clock time, so the rule tests the slot's format against the **window's** confound result. A Tier 2 or Tier 3 slot is day-level, so the rule tests against the **day's** confound result. A format can be clean at the day level and flagged inside one band on that day: that is not a contradiction, it is the two layers doing their jobs, and the day-level slot handles the band with the posting warning in section 2.6 rather than with a move.

**The rule tests the format the upstream NAMED, and nothing else.** The time reader prints the highest-representation format per bucket. If it named link, the rule fires on link. It does not fire on a format the upstream did not name, and the calendar does not infer that unnamed formats were cleared. On a slot whose format was neither named as the confound nor explicitly listed with its own ratio, print: "the upstream named {type} as this bucket's confound, not {slot format}, and it did not print {slot format}'s own representation here. This pairing is not flagged and it is also not independently confirmed clean."

**Why this rule exists.** A format-confound flag says: in this window, this format is over-represented relative to its share of the account, and this format has its own corpus-wide performance difference. The upstream cannot separate the window effect from the format effect. If the calendar then schedules that exact format in that exact window, next week's post cannot separate them either, and the user has spent a slot buying a data point they already had. Worse, the calendar will have printed an evidence line pointing at the very flag it just reproduced.

**When the double-cite rule cannot run.** If the time read's flag columns say "not checked" for a bucket, the rule does not fire and **the calendar says so on the slot**: "the format-confound check did not run on this bucket upstream, so this pairing is unchecked. Unchecked is not the same as clean." Never leave the absence silent, and never let it read as a pass.

---

## 2.8 The confound budget

Every slot has four axes: **time, format, hook, topic.** An axis counts as **untested** when its value came from a bucket the upstream refused to rank, excluded, or never measured.

```
Working number, labeled: no slot may carry more than TWO untested axes.
```

**Four axes, not five. The duration band is a refinement of the format axis, not an axis of its own.** A video slot whose format is Tier A but whose duration band is unrankable is marked "format tested, duration band untested" and the band does not count against the budget. The reason: a band is an instruction inside a format rather than a separate bet. If the video underperforms, the format evidence still holds and the band is the obvious first thing to change, which is exactly what a diagnosable result looks like. Counting it as a fifth axis would blow the budget on every video slot in every capture, which would mean the rule never let a video ship, which would be a worse skill.

**Why two.** A slot with one untested axis is a clean single-variable test: if it lands, you know what landed. Two is still readable, because the two axes are usually independent (a new hook on a proven format tells you about the hook). Three or four is a result you cannot diagnose. If a four-axis-untested slot underperforms, you do not know whether it was the day, the format, the hook, or the topic, and you have spent a post to learn nothing. The budget is not caution, it is the difference between an experiment and a coin flip.

**The budget is applied during allocation, not after.** Count the untested values you have to place, spread them across the slots highest-confidence-first, and if they do not fit, something gets dropped.

**When the budget cannot be satisfied:**

```
Drop the untested TIME first, and say so.
```

Time is the axis to sacrifice, for two reasons that are both about cost. First, an untested day costs the whole slot: if nobody is there on a Wednesday, the format, hook, and topic never get a fair read, so an untested day poisons every other axis on that slot. Second, time is the cheapest axis to retest later, because you can post the same draft on a different day next week at no writing cost, and you cannot do that with a topic or a format.

So when the budget blows, the experimental slot moves to the highest-tier available ranked day, and the untested day becomes its own named recommendation on the calendar: "test {day} on purpose, next week, with your best format, your best hook, and your best topic. That makes it a single-variable test. Stacked on top of three other untested axes, it is not a test at all."

That recommendation frequently comes straight from the audit's 30-day list, which means the calendar is declining an upstream instruction for a stated reason. It says exactly that, cites the item number, and puts it on the next week. Declining with a reason is a finding. Declining silently is a bug.

---

# SECTION 3: SOLO MODE

Solo mode runs from one raw PostSnag export plus 3 to 5 topics from the user. It executes lighter inline versions of all three upstream reads. It exists so a first-time user gets a week without downloading four skills, and it is honestly worse. The honesty line goes at the top of every solo-mode output, not the bottom:

> **Solo mode.** This ran lighter versions of three skills inside one pass. Every slot below is day-level, no slot's format was checked against a confound, and the hook list is missing the one test that finds archetypes you already write and have never led with. Run `facebook-profile-audit`, `facebook-hook-analyzer`, and `best-time-to-post-reader` on this same export and feed their outputs back here, and this calendar gets {the specific list} that it does not have now.

## 3.1 Audit-lite, standing in for `facebook-profile-audit`

**Runs:** parse and validate per `references/csv-parse.md` (condensed; full version in `_shared/csv-contract.md` and the bundle); format distribution with n, median, mean, share of corpus, and share of top quartile; the concentration check on every rankable format per `references/foundations.md` section 4 (condensed from `_shared/engagement-math.md` section 5); posts per week; posting-day counts; top-10 versus bottom-10 by format.

**Skips:** topic clustering entirely, video duration bands, trajectory, the five steal-worthy patterns, the 30-day list, the video views-versus-rate lens.

**Cost, stated on the output:** with no topic clustering, every slot's topic axis is untested by construction. With no duration bands, video slots carry no length instruction. With no 30-day list, the experimental slot has no upstream recommendation to execute and falls to the highest-lift unrankable format.

## 3.2 Hook-lite, standing in for `facebook-hook-analyzer`

**Runs:** the full 12-archetype classification from `references/hook-archetypes.md` (condensed from `../../facebook-hook-analyzer/references/rubric.md` section 2; full version in the bundle), using its precedence ladder unchanged, so solo-mode numbers are reproducible against a real hook-analyzer run on the same file; per-archetype n and median; the concentration check on each; the over-represented screen against the top quartile; the too-small-to-rank list.

**Uses the same 12 archetypes on purpose.** A shortened archetype list would produce numbers that quietly disagree with the real skill's numbers on the same export, and the user would have no way to tell which was right. Solo mode is allowed to do less. It is not allowed to do the same thing differently.

**Skips:** the latent-fit test (the search of post bodies for archetype markers that finds unexplored archetypes the creator already writes), the structural read (hook-length and caption-length buckets), the visual-hook section, and the conversion of the top 10 hooks into fill-in templates.

**Cost, stated on the output:** Pool 3 loses its best member. The latent-fit test is what produces an UNEXPLORED archetype with real evidence behind it, and without it Pool 3 is just the small-n archetypes sorted by median, which is a weaker list. Drafts also lose their character targets, because the structural read is where hook-length and caption-length bands come from, and they lose the creator's own abstracted templates, falling back to `../../facebook-hook-analyzer/references/hook-template-library.md`.

## 3.3 Time-lite, standing in for `best-time-to-post-reader`

**Runs:** the timezone question (still asked, always); the date-only precision check per `references/csv-parse.md` section 4 (condensed from `_shared/csv-contract.md` section 5; full version in the bundle); day-of-week bucketing with the 5-post floor; median per rankable day; the concentration check on each rankable day; the schedule-gap comparison at the day level.

**Skips:** the four time bands and the entire 28-cell day-by-time grid, the format-confound check, the best-windows table, the early-signal carve-out.

**Cost, stated on the output, and this is the biggest single loss in solo mode:** with no format-confound check, the double-cite rule in section 2.7 cannot run. Every slot's format-confound cell reads **not checked**. That is not a pass. On a fuller capture the format-confound check routinely fires on the majority of ranked buckets, and it is the flag that moves a slot rather than caveating it. Solo mode does not check and cannot move.

Every solo-mode slot is day-level. There is no path to a clock time, because clock times require the 28-cell grid solo mode does not build.

## 3.4 Solo-mode allocation differences

```
- The confound budget (2.8) counts THREE axes, not four, because the topic axis
  is unmeasured on every slot by construction. State the exclusion. A slot that
  looks in budget in solo mode would be over budget in chain mode.
- The double-cite rule (2.7) does not run. Every slot says so.
- Every slot is Tier 2 at best (ranked clean day, day-level) or Tier 3
  (ranked flagged day). Tier 1 is unreachable.
- Topics come from the user's 3-to-5 list, in the order they gave them, one per
  slot, no repeats.
```

## 3.5 The honest comparison, stated once

Chain mode is better and here is exactly why, in the terms a user can check:

1. **Clock times exist.** Solo mode's every slot is day-level. That is a real, visible difference on the page.
2. **The double-cite rule runs.** Chain mode moves a slot off a pairing its own evidence cannot separate. Solo mode ships that pairing unchecked and cannot tell you it did.
3. **Pool 3 has its best member.** The latent-fit find is regularly the most interesting slot of the week, and solo mode cannot produce it.
4. **Topic axes are measured.** Chain mode assigns topics from ranked clusters with medians and flags. Solo mode assigns whatever the user typed.
5. **The confound budget counts all four axes.** Solo mode counts three, which means a solo-mode week can be more confounded than it looks.

That is five specific losses, not a general warning. Run the three skills once and this calendar becomes a different artifact.

---

# SECTION 4: THE DRAFTING METHOD

Every slot ships a complete draft, not a brief. A brief is a second task disguised as a deliverable.

## 4.1 Where the voice comes from

**From the creator's own winners, mechanically, not from a general idea of good Facebook writing.**

Read the posts the hook analyzer listed in its **Your top 10 hooks, as templates** section and extract five things:

```
1. Sentence length and rhythm. Count words per sentence across those 10 posts.
   Match the distribution, not the average: if the creator writes a 6-word
   sentence next to a 22-word sentence, do that.
2. Paragraph shape. Hook line, blank line, then how many body blocks, and how
   many sentences per block.
3. Punctuation habits. Colons, question marks, quoted speech, sentence
   fragments, numerals versus spelled-out numbers.
4. Emoji, hashtag, and CTA behavior. Count them. If the creator uses zero
   emoji across their top 10, the draft uses zero. This is the single most
   common way a generated draft announces itself.
5. The closing move. Most creators have one: an aphorism, an instruction, a
   turn back to the reader, a number. Name theirs and use it.
```

Write the observed values into the run's working notes so the draft can be checked against them.

## 4.2 Where the hook comes from

The assigned archetype's template, in this order:

```
1. The abstracted Template line from the hook analyzer's top-10 list, if that
   archetype appears there. This is the creator's own winning structure,
   already abstracted for reuse by the skill that measured it.
2. Otherwise a template for that archetype from references/hook-template-mini.md
   (condensed, 2 templates per archetype; full 44-template library in
   ../../facebook-hook-analyzer/references/hook-template-library.md and the
   bundle), and the slot says the template is a library pattern rather than
   one of the creator's own winners. This is always the fallback in solo
   mode, because solo mode never builds a top-10 list (section 3.2).
```

Print the template string verbatim on the slot, above the draft. The reader should be able to see the structure and the fill separately.

## 4.3 Structure rules for the draft body

```
- Hook line first, alone, then a blank line. This is near-universal in captured
  Facebook captions and it is what the hook analyzer's extraction assumes.
- Hook-line length targets the analyzer's best-performing hook-length bucket.
  Only a bucket that cleared the 5-post floor is a target; an unranked bucket
  is never a target.
- Caption length targets the analyzer's best-performing caption-length bucket,
  same floor rule. Count the whole caption including the hook line.
- **Caption-length arbitration (R3).** The hook analyzer's caption-length
  bucket is measured in characters. If a `creator-voice-skill-builder` or
  `facebook-caption-writer` voice profile exists for the same creator and
  reports a measured WORD-count band, that word band governs the draft's
  actual length, because it is the creator's own observed writing rhythm
  measured directly, not a character-count proxy for it (on the shared
  synthetic fixture, `facebook-caption-writer` measured Maya's band at 38 to
  69 words). The character bucket is secondary: use it only when no measured
  word band exists for this creator. State on the slot which one governed.
- On a video slot, the draft has TWO parts, and this distinction matters:
    the CAPTION, governed by the caption-length target, and
    the ON-CAMERA SCRIPT, governed by the assigned duration band.
  A caption is not a script. Writing one 60-second script into a 300-character
  caption target produces a bad caption and a bad script.
  Script length: roughly 2.2 words per second of the target band.
- On a link slot, the draft's last line sets up the click without naming a page.
  The destination is the user's to supply. This skill does not invent a URL and
  does not invent a page that exists on someone's site.
- No em dashes. No emoji or hashtags unless the voice extraction in 4.1 found
  them in the creator's own top 10.
```

## 4.4 The originality guardrail

A drafted post that reads like a template has cost the creator the slot. Four checks, all run before the draft ships:

```
1. SUBJECT TEST. Every draft uses an object, place, or scenario drawn from the
   creator's own captured posts. A draft that would work unchanged for any
   creator in any niche is wrong and gets rewritten. This is the same bar the
   hook analyzer sets on its own drafted hooks.

2. THE 6-WORD RULE. No draft reuses more than 6 consecutive words from any
   captured post. Check it literally, sliding a 7-word window across every
   caption in the export. The template is the structure; the nouns are new.
   (Working number, labeled: 6 is this skill's threshold, not a platform fact.
   It sits just above the length of a common phrase and just below the length
   of a distinctive clause.)

3. THE SAME-EXAMPLE TEST. A draft may reuse a topic. It may not reuse the
   topic AND the specific example. If the creator's closet post named a sled,
   the new closet post does not name a sled.

4. THE PERFORMANCE SILENCE RULE. No draft, and no line near a draft, claims the
   post will perform. The calendar states which evidence the slot stands on and
   stops. "This should do well" is not a finding, it is a mood.
```

When check 2 fires close to its limit (a 5-or-6-word run), that is expected on a deliberate template reuse and it is worth noting in the working notes rather than rewriting. When it fires at 7 or more, rewrite.

## 4.5 What every draft ships with

```
- the hook line, matching its archetype's template
- the full body
- on video slots, the on-camera script and its target duration band
- the template string used, verbatim
- the character counts: hook length and caption length, against their targets
- the four evidence lines: time, format, hook, topic, each written as
  "because: {upstream citation}"
- the untested-axis count for the slot
```

## 4.6 Things the drafting method never does

- Never writes a caption for an image it has not been shown. `Media_URLs` are expiring links and no skill in this catalog fetches them.
- Never invents an engagement prediction, a reach estimate, or a best-time claim beyond what the time read supplied.
- Never writes a promotional post unless the user asked for one, because promo tolerance is not measurable from a profile export and guessing at it is how a calendar loses a creator's audience.
- Never schedules. Drafts only. The human posts.
