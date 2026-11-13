# output-template.md

The exact structure the user receives. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line.

For this template filled with real numbers, chained off the actual outputs of the three upstream skills, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **The drafts-only line is the first line of the output.** Above the banners, above the title. A user reading a schedule needs to know before they read it that nothing here is connected to anything.
- **The diagnostic header is the second line, immediately after the drafts-only line.** It is still above every banner and the title; only the drafts-only disclaimer outranks it.
- **Inherited banners go next**, before any slot. A lite-mode banner from any upstream is reprinted here with the upstream skill named. Not at the bottom where it reads as an excuse.
- **Every caveat is glued to its number, inside the sentence.** A caveat that survives three skills and dies in a trailing parenthetical on a calendar has died in the worst possible place, because a calendar is the artifact people screenshot.
- **A format-confound caveat carries its DIRECTION**, not just its existence. Say where the over-represented post sits in the bucket, or say the upstream did not state it.
- **A slot's check line never says "none".** It says what cleared ("Concentration checked, clean. Format checked, no confound.") or it says "not checked". On a row a user is about to act on, silence and clean look identical.
- **Every allocated value carries its evidence line.** Four per slot: time, format, hook, topic. Written as `because: {upstream citation}` with the upstream sentence or number quoted closely enough to find.
- **No em dashes.** Comma, colon, period, parentheses.
- **Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.

---

```markdown
**Drafts only.** Nothing here is scheduled, connected, or published. This skill does not touch your Facebook account. It writes text and puts dates next to it. You post it.

Skill: facebook-content-calendar-builder v1.1 | {N} posts | {first date} to {last date} | computed with code: {yes/no}

{INHERITED BANNERS, one per upstream artifact that carried one. Omit entirely if all three ran in full mode.}

> **Lite mode, inherited from {skill name}.** {The upstream banner, restated.} Here that means: {the specific consequences on this calendar, from rubric section 1.4}.

{SOLO-MODE BANNER, only in solo mode. Never appears in chain mode.}

> **Solo mode.** This ran lighter versions of three skills inside one pass. Every slot below is day-level, no slot's format was checked against a confound, and the hook list is missing the test that finds archetypes you already write and have never led with. Run facebook-profile-audit, facebook-hook-analyzer, and best-time-to-post-reader on this same export and feed their outputs back here, and this calendar gains {the specific list}.

# Content calendar: {profile name}, {Monday date} to {Sunday date}

Built from {chain mode: "your profile audit, hook analysis, and best-time read, all three on the same {N}-post capture, {first date} to {last date}" / solo mode: "one {N}-post export plus the {k} topics you gave me"}.

{slot count} slots across 7 days. {How the count was derived, in one sentence with both numbers: "Your cadence supports {total}. Your time evidence supports {days} ranked days. This week is {final}."}

---

## The week

| Day | Date | Slot | Format | Hook archetype | Confidence |
|---|---|---|---|---|---|
| Monday | {date} | {slot number or "no slot"} | {type} | {archetype} | {Tier N} |
| Tuesday | {date} | ... | | | |
| Wednesday | {date} | no slot | | | |
| Thursday | {date} | ... | | | |
| Friday | {date} | no slot | | | |
| Saturday | {date} | ... | | | |
| Sunday | {date} | no slot | | | |

{One line naming the empty days and why they are empty. Never leave a blank day unexplained: a reader assumes an omission is an oversight.}

---

## Slot {n}: {Day}, {date}

**Time:** {clock window and timezone / "day-level slot, no clock time"} | **Confidence: Tier {1-4}**
**Checks:** {"Concentration checked, clean. Format checked, no confound." / the named flags, with direction / "not checked" and what that means}
**Format:** {type}{, duration band on video} | **Hook:** {archetype} | **Topic:** {topic}
**Untested axes:** {n} of 4 {(3 in solo mode, and say so)}

**Template used:** `{the verbatim template string}`

---

{THE FULL DRAFT. Not a brief. Not a summary. The post, ready to paste.}

{On video slots, two labeled parts:}

**Caption ({n} characters, target {band}):**

{the caption}

**On-camera script (target {duration band}):**

{the script}

---

**because: {time}** {the upstream citation, quoted closely: the table row, the median, the flag, the direction}
**because: {format}** {the upstream citation: the format's n, median, lift, tier, and the audit finding that named it}
**because: {hook}** {the upstream citation: the archetype's n, median, pool, and the top-10 post the template came from}
**because: {topic}** {the upstream citation: the cluster's n, median, flags, rankable state}

{Any rule that fired on this slot and changed it: the double-cite move, the confound-budget drop, the Tier-2-over-Tier-3 preference, a Pool-dry conversion. One line each, naming the rule.}

---

{Repeat the slot block for every slot, in chronological order.}

---

## Week summary

**Slot arithmetic.** {base} from your cadence of {posts_per_week} posts per week, plus {n} experimental, capped at {days} by the days your time read could rank. Final: {n} slots.

**Format mix.** {type} {n}, {type} {n}, ... against your capture's {type} {x}%, {type} {y}%, ... {One line on the biggest deliberate divergence and the finding behind it, including any format given zero slots and why.}

**Hook rotation.** {n} distinct archetypes across {n} slots. {n} proven, {n} experimental. {If the proven pools ran dry: one line saying how many proven archetypes the file supports and that the remainder are experimental by arithmetic, not by choice.}

**Time tiers.** {n} at Tier 1 (clock time, both checks clean), {n} at Tier 2 (day-level, clean), {n} at Tier 3 (carrying a flag). {n} Tier 4 values were named and not scheduled.

**Flags this week inherited.** {Numbered. Every flag read from any upstream artifact, with its source, the slot that inherited it, and how it appears: caveat line, moved the slot, or excluded the value. A flag with no disposition is a bug, so every flag gets a line.}

1. {flag} | from {artifact}, {section} | inherited by slot {n} as {disposition}
2. ...

**Cut this one first.** {If the week goes sideways and you only get {n-1} posts out, drop slot {n}, and here is why in one sentence with its number.}

**Upstream recommendations this week consumed.** {A checklist against the audit's 30-day list and the hook analyzer's test list. Every item: consumed by slot {n}, or declined with a stated reason, or deferred to a named future week. Nothing silently dropped.}

**What to do after.** Post them. Capture the profile again in {specific number} days, rerun the three upstream skills, and compare. {The one specific number on this calendar most worth watching, named, with its current value.}

---

## What this calendar is standing on

This calendar measured nothing. It allocated a week from three artifacts that did the measuring, and every number above traces to a line in one of them. Sources: `facebook-profile-audit`, `facebook-hook-analyzer`, and `best-time-to-post-reader`, all three run on the same {N}-post capture, {first date} to {last date}, {span} days.

{The inherited limits, restated in one paragraph each where they bite: sample-size floors, lite mode, the timezone state, any upstream section that was absent and what was marked untested as a result.}

{If any allocation was defaulted rather than derived, say which and why.}

Not in your export, so not in this plan: sponsored or paid-partnership flags, so if an upstream finding is standing on a boosted post, this plan inherited that and cannot see it. Reach or impressions, so no slot here predicts how many people will see anything. Per-emoji reactions. Comment text. Follower history over time.

PostSnag captures what you scrolled, so this plans from a sample of the account, not its full history.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

This analysis is for your own use. If you publish it, remove the analyzed account's name and the verbatim quotes; the numbers are yours to keep, the other creator's words are not.

**Drafts only. You post them.** No publishing, no scheduling, no account access.

Analysis based on {N} captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-content-calendar-builder
```

---

## Section-by-section notes for whoever fills this

**The drafts-only line.** First line, every time, no exceptions, including when the user has run this skill ten times. It is the one sentence in this output that protects both the user and the product, and it costs nine words.

**The week table.** Seven rows always, including the empty days. A calendar that only shows the days with posts hides the most useful decision on the page, which is the decision not to post. The line under the table naming why the empty days are empty is not optional; without it an empty Friday reads as a mistake.

**The slot header block.** Confidence tier goes next to the time, not in a footnote, because the tier is what tells the user how hard to hold the date. The untested-axis count goes here too, for the same reason: it tells the user how readable the result will be before they read the draft.

**The draft.** Complete. Paste-ready. If a draft needs the user to fill a blank, the blank is a slot the skill failed to allocate, and it should have been marked untested instead.

**The four because-lines.** These are the product. A calendar with dates and drafts and no citations is a guess with good formatting. Quote the upstream closely enough that the user can find the line in the report they already have open. Do not paraphrase a number.

**The rule-fired lines.** When the double-cite rule moves a slot, or the confound budget drops an untested day, or a dry pool converts a proven slot, the user should see the machinery. That is the difference between a plan and an oracle, and it is the reason they can argue with it.

**The flag ledger in the week summary.** Every flag from every artifact gets a row, including the ones this calendar did not use, marked as not used. This is the audit trail for the whole propagation rule, and it is the first thing to check when a calendar looks too clean.

**The cut-this-one-first line.** Weeks go sideways. Naming the drop order in advance is worth more than any other single line in the summary, because it is the only advice on the page that survives contact with a bad week.

**The footer.** Never softened, never moved, never dropped. This skill's footer does one extra job the other skills' footers do not: it states plainly that this artifact measured nothing and inherited everything. That is not modesty, it is the accurate description of a chain, and it tells the user which report to go fix when a number looks wrong.
