# chain-input-map.md

The field-by-field contract between this skill and the three skills that feed it. One row per consumed field: which upstream skill, which section of its output, which field, what that field drives here, what happens when it is absent, and what happens when it carries a flag.

This is the file that makes the chain real. If you are wiring these four skills together, in an agent, in a script, or by hand in a chat window, this is the document you work from. If you are auditing a calendar that looks wrong, start here and walk backwards.

Version 1.0 | 2026-08-04

---

## How to read this file

**Section names are the upstream output-template headings, verbatim.** They are stable strings. Match on them.

**"Drives" means an allocation rule fires on this field.** The rule numbers refer to `rubric.md`.

**"When absent" is one of three behaviors** defined in `rubric.md` section 1.3:

| Code | Behavior |
|---|---|
| **A** | Degrade with a named fallback, printed on the slot |
| **B** | Mark the axis untested, count it against the confound budget |
| **C** | Refuse the run and name what is missing |

**"When flagged"** describes what happens when the upstream attached a caveat, an exclusion, or a "not checked" to this field. The governing principle is `rubric.md` section 1.5: a flagged finding is used and its caveat travels, an excluded finding is never used, and a flag that identifies a bad pairing moves a slot instead of caveating it.

**Bold rows are load-bearing.** Removing one changes what the calendar can honestly claim.

---

## Part 1: from `facebook-profile-audit`

| # | Section | Field consumed | Drives | When absent | When flagged |
|---|---|---|---|---|---|
| 1 | Header line | N, first date, last date, span | The three-way cross-check (1.1), the pointer-line N | **C.** Without N the cross-check cannot run and two artifacts could be from different captures. Ask for the header. | n/a |
| 2 | Header line | corpus median engagement | Every "above / below your median" comparison on the calendar | **A.** Take it from the hook analyzer's header, which prints the same number, and say which artifact it came from. | Must match the other two artifacts. Mismatch stops the run (1.6). |
| 3 | Header line | format mix percentages | Cross-check against the format distribution table (1.6), and the "against your capture's mix" line in the week summary | **A.** Recompute from the format table's own n column. | n/a |
| 4 | Lite-mode banner | presence, and its named degraded sections | Forces day-level slots, caps the week at ranked days, marks most topic axes untested (1.4) | Absent means full mode, but verify against N and span rather than trusting the absence. | The banner **is** the flag. Reprinted at the top of the calendar with the upstream skill named. |
| 5 | **Cadence** | posts per week | **The base slot count (2.1)** | **A.** Default base to 3 and print "the slot count was defaulted, not derived from your cadence." | n/a |
| 6 | **Cadence** | posting-day counts | The day-count cross-check against the time read (1.6) | **A.** Skip the cross-check and say it was skipped. | A mismatch with the time read's day counts stops the run, even when the headers agreed. |
| 7 | Cadence | gap median, minimum, maximum | Nothing in v1.0 | Nothing. | n/a |
| 8 | Cadence | same-day doubling | Nothing in v1.0. Printed as a note on the week summary when present. | No note. | n/a |
| 9 | **Format distribution** | per-type n | Rankability (Tier D assignment, 2.2) | **C.** No format evidence means every format is a guess, and format is the axis that costs the most to get wrong. | n/a |
| 10 | **Format distribution** | per-type median | Tie-break 1 in 2.2, and the format evidence line on every slot | **A.** Fall back to top-quartile share alone and say the tiering is thinner. | n/a |
| 11 | **Format distribution** | share of corpus AND share of top quartile | **The lift calculation, which produces Tiers A / B / C / D (2.2)** | **A.** Fall back to median-against-corpus-median tiering, and print the substitution on every slot. | n/a |
| 12 | Format distribution | check columns (median after top removed, change, top post's share, mean / median) | The caveat printed on the format evidence line | **B.** The format is used; the slot says the concentration check result was not supplied. | Any flag: the format is still used, and the slot carries "use the median, {n} posts are carrying the mean". |
| 13 | Format distribution | Rankable column | Tier D assignment: an unrankable format never holds a proven slot (2.2) | **A.** Compute rankability from n at or above 5. | A cell reading `not checked` is treated as unrankable. Never as clean. |
| 14 | Format distribution (the "Top 10 versus bottom 10 by format" line within it; the audit's output template has no separate heading for this, it is one sentence inside the Format distribution section) | per-format counts in each set | **Tie-break 3 in 2.2**, which is the tie-break that usually resolves a lift tie | **A.** Fall through to alphabetical, and say the tie was broken arbitrarily. | n/a |
| 15 | **Topic clusters** | per-topic n, median, Rankable | **The topic assigned to every slot (2.4)** | **B.** Ask the user for 3 to 5 topics and mark every topic axis untested. This is solo mode's permanent state. | One flag: topic used, caveat travels. Two flags: never a proven slot. |
| 16 | Topic clusters | the tested-and-flat null result | That topic is skipped, with one printed line saying it is measured and flat rather than failing (2.4) | No skip. | n/a |
| 17 | Topic clusters | the additive-topics note | Reprinted once on the calendar if topic percentages appear, so a reader who sees them not summing to 100 knows why | No note needed if no percentages are printed. | n/a |
| 18 | **Video: views and duration** | duration bands with n, median, check columns | **The duration instruction on every video slot (2.2)** | **A.** Video slots carry no duration instruction and the slot says so. | Two flags on a band: usable as an experiment, never as a proven instruction, and the slot names the specific posts driving it. |
| 19 | Video: views and duration | the views-versus-rate finding | Nothing in v1.0 | Nothing. | n/a |
| 20 | **What works / What does not work** | the three findings each | The exclusion list (a format or topic named as absent from the top quartile gets zero slots), and the promotion of an untested standout into the experimental slot | **A.** Derive both from the tables alone and say the findings section was not supplied. | These findings arrive with their caveats already glued in. Copy them verbatim in substance, never trimmed. |
| 21 | 5 patterns worth stealing | the named patterns | Nothing directly. Cross-referenced in the consumed-recommendations checklist. | Nothing. | n/a |
| 22 | **Your 30-day list** | the numbered items | **The experimental slot's content, and the consumed-recommendations checklist in the week summary** | **A.** The experimental slot falls to the highest-lift unrankable format and the highest-median unrankable topic. | n/a. Note: an item this calendar declines (usually on the confound budget) is printed as declined with its reason and its item number, never dropped. |
| 23 | Trajectory | rising / falling / flat, and the follower-history confound sentence | One line on the week summary. **It does not change the slot count.** | No line. Absent below 90 days of span or in lite mode, which is normal, not a gap. | The confound sentence travels with it, uncut. A rising median cannot be separated from a growing audience and the calendar does not pretend otherwise. |

---

## Part 2: from `facebook-hook-analyzer`

| # | Section | Field consumed | Drives | When absent | When flagged |
|---|---|---|---|---|---|
| 24 | Header line | N, dates, span, caption counts | The three-way cross-check (1.1) | **A.** Skip that leg of the cross-check and say it was skipped. | Mismatch with the other two artifacts stops the run. |
| 25 | **Your hook patterns** | archetype, posts, median, share of top quartile | **Pool 1 (2.3), and the hook evidence line on every slot** | **C.** With no archetype ranking there is no hook to assign and no template to draft from. Refuse. | Two concentration flags on an archetype: never a proven slot. It may hold an experimental slot, and that slot states the archetype is standing on one post and names it. |
| 26 | Your hook patterns | the median-versus-mean ranking note | The week summary's one line on why the ranking is what it is | No line. | n/a |
| 27 | **Too small to rank** line | archetype, posts, median | **Pool 2 (2.3)**: n between 3 and 4, zero flags, median above the corpus median | **A.** Pool 2 is empty and the calendar says so, which usually pushes a proven slot into the hook-experimental state. | A flagged entry never enters Pool 2. It drops to Pool 3. |
| 28 | **What you over-invest in and what you under-invest in** | share of posts against share of top quartile | **The Pool 1 lift screen (2.3)**, and the "stop writing this one" line in the week summary | **A.** Pool 1 falls back to "ranked, and median above the corpus median", and the calendar says the screen was weakened. | n/a |
| 29 | The structural read | hook-length and caption-length buckets with n and median | **The character targets written onto every draft (4.3)** | **A.** Drafts carry no character target and say so. | A bucket under the 5-post floor is never used as a target, even when its median is the highest. |
| 30 | **Your top 10 hooks, as templates** | the verbatim hook, its archetype, its post's format, and the abstracted Template line | **The fill-in template every draft is written from (4.2), and the format co-occurrence override (2.5)** | **A.** Templates come from `references/hook-template-mini.md` instead (condensed; full 44-template library in `../../facebook-hook-analyzer/references/hook-template-library.md` and the bundle), and the slot says the template is a library pattern rather than one of the creator's own winners. | n/a |
| 31 | **5 archetypes to test next** | the ordered list, the UNDERUSED / UNEXPLORED labels, and the latent-fit evidence | **Pool 3 (2.3), in the analyzer's own order.** This skill does not reorder it. | **A.** Pool 3 falls back to the too-small-to-rank line sorted by median, which is a weaker list and the calendar says so. | An entry whose only evidence is a bucket with two concentration flags is skipped, unless Pool 3 is otherwise exhausted. |
| 32 | Visual hooks | present or omitted | Nothing. The calendar never writes a visual instruction it cannot evidence. | No visual line anywhere. | n/a |
| 33 | What this analysis is standing on | the concentration flags restated | Copied into this calendar's flag ledger | **A.** Rebuild the ledger from the tables. | Every flag in the footer gets a ledger row, including the ones this calendar did not use, marked not used. |

---

## Part 3: from `best-time-to-post-reader`

| # | Section | Field consumed | Drives | When absent | When flagged |
|---|---|---|---|---|---|
| 34 | Header line | N, dates, span | The three-way cross-check (1.1) | **A.** Skip that leg and say so. | Mismatch stops the run. |
| 35 | **Header line** | the timezone sentence | **Whether any slot can carry a clock time at all (2.6)** | Treat as unconfirmed. Every slot is day-level. | "Relative only" is the flag. Every slot is day-level and the calendar prints why in one line. |
| 36 | Date-only banner | presence | Forces every slot to day-level | Absent, proceed. | The banner **is** the flag, reprinted at the top of the calendar. |
| 37 | Lite-mode banner | presence, plus "clears on x of 7 days" and "y of 28 windows" | Forces day-level slots and caps the week at the number of ranked days (1.4, 2.1 step 5) | Absent, full mode. | The banner is reprinted at the top of the calendar with the upstream skill named. |
| 38 | **Your best days** | day, posts, median | **The slot days, in rank order (2.6)** | **C.** With no ranked day there is no defensible date for anything, and a calendar whose dates are arbitrary is a list. Refuse. | n/a |
| 39 | **Your best days** | the Flags column | **The confidence tier on every slot (2.6), and the caveat printed on it** | **B.** The day is used at Tier 3 and the slot says the checks were not supplied. | One flag: day used at Tier 3, caveat travels with its direction. Two flags: the day is Tier 4 and is never scheduled. `not checked` is copied through as `not checked`, never as clean. |
| 40 | Your best days | "Too small to rank" line | The Tier 4 day list. Never a slot time. May be named once as a deliberate future test. | No Tier 4 list, and the calendar says untested days were not identified. | n/a |
| 41 | **Your best windows (day and time)** | window, posts, median, Flags | **The clock time on a slot, Tier 1 when both checks cleared and Tier 3 when one flag fired (2.6)** | Absent, or replaced by the upstream's "no window reaches 5 posts" paragraph: every slot is day-level. This is normal, not a gap. | One flag: clock time used at Tier 3, caveat travels. A format-confound flag here additionally feeds row 44. |
| 42 | Your best windows (day and time) | the excluded-window note (2 or more concentration flags) | Tier 4. Never a slot time. Named once on the calendar so the user knows why the higher-median band was skipped. | No exclusion note. | This is an exclusion, not a caveat. The calendar does not relitigate it. |
| 43 | Early signal (one window, not a ranking) | the one cell that cleared the floor in lite mode | May be named once, on an experimental slot, as a thing to test on purpose. **Never becomes a scheduled clock time.** | Nothing. | Its caveats travel with it. |
| 44 | **Format-confound flags, anywhere in either table** | the type named, its representation ratio, its median ratio against the corpus median, and where the over-represented post sits in the bucket | **The double-cite rule (2.7): a slot's format may not be the format that fired a confound on that slot's day or window.** This is the one flag that moves a slot rather than caveating it. | **B, loudly.** The rule cannot run. Every slot prints "the format-confound check did not run on this bucket upstream, so this pairing is unchecked. Unchecked is not the same as clean." | Fires the move. Preference is to relocate the format; keeping the pairing is permitted only on an experimental slot, labeled a deliberate confound test. |
| 45 | **Where you post versus where you win** | most-posted day, best-median day, the percentage gap | **The schedule-gap rule (2.6): at most one slot on the over-posted day**, and the gap line in the week summary | **A.** No gap line, and the one-slot cap is not applied. | n/a |
| 46 | What this analysis is standing on | the flag roll-up | The flag ledger in the week summary | **A.** Rebuild from the tables. | Every flag gets a ledger row with a disposition. A flag with no disposition is a bug. |

---

## Part 4: the cross-artifact rules

These are not fields. They are checks across artifacts, and they run before allocation.

| Check | What must match | On mismatch |
|---|---|---|
| **Header identity** | N, first date, last date, and span, across all three artifacts | **STOP.** Print all three headers, name the odd one out, ask for a rerun on one export. |
| **Corpus median** | the same number in all three headers | **STOP.** Same reason: it means the artifacts came from different files. |
| **Posting-day counts** | the audit's Cadence day counts against the time read's best-days table plus its too-small-to-rank line | **STOP.** This one catches a mismatch the headers can miss, because two exports of the same account at different depths can share a date range. |
| **Format inventory** | the audit's header format mix against its own format distribution table | **STOP.** Usually a truncated paste rather than a real mismatch, and one line of the table missing silently changes every lift on the page. |
| **Lite-mode consistency** | if any artifact is in lite mode, the calendar is in lite mode | No mismatch possible, but state it: there is no partial version of lite mode here. |

---

## Part 5: what this calendar sends back upstream

Nothing automatic, but two things worth doing by hand, because they close the loop:

1. **The consumed-recommendations checklist** in the week summary maps every item on the audit's 30-day list and the hook analyzer's test list to a slot, a decline with a reason, or a named future week. Keep it. Next month, run the three skills again and check the items you consumed against what actually happened.
2. **The flag ledger** names every caveat that made it onto a slot. When you recapture and rerun, the flags that cleared are the ones your week actually resolved. A flag that fired again after you tested it on purpose is a real finding, not a caveat, and it belongs in the next calendar as a constraint rather than a note.

---

## Part 6: a worked absence, so the behaviors are not abstract

Say a user pastes the full audit, the full time read, and only the top half of the hook analysis: the header, the pattern table, and the too-small-to-rank line. Missing: the over-invest table, the top-10 templates, the structural read, and the test list.

What the calendar does, row by row:

| Missing | Row | Behavior | Printed consequence |
|---|---|---|---|
| Over-invest table | 28 | **A** | Pool 1 falls back to "ranked, and median above the corpus median". Printed on every proven slot: "Pool 1 was built without the top-quartile screen, which is weaker." |
| Top 10 templates | 30 | **A** | Templates come from the hook template library. Printed on every slot: "library pattern, not one of your own winners." Also disables the co-occurrence override in 2.5, so pairing falls entirely to the evidence score. |
| Structural read | 29 | **A** | Drafts ship with no character target. Printed once in the week summary. |
| Test list | 31 | **A** | Pool 3 rebuilt from the too-small-to-rank line, sorted by median. Printed on every experimental slot: "your test list was not supplied, so this archetype was chosen by median rather than by the analyzer's tiering, and the latent-fit finding is not available." |

The calendar still ships. It ships four printed admissions and it is visibly thinner than a full chain run, which is the correct outcome: a user who sees four admissions goes and pastes the rest of the report, and a user who sees none never learns what they gave up.
