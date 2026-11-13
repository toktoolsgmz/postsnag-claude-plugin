# output-template.md

The exact structure the user receives. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line.

For this template filled with real computed numbers, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **The depth banner goes at the top**, before the findings, whenever the capture does not clear the 90-day span needed for a real shortlist. Not at the bottom where it reads as an excuse.
- **Every score names its own denominator**, inline, in the sentence: "era-adjusted score 2.76, its own 10-post neighborhood median was 378.5" or "1.71x the corpus median of 458.5," never a bare multiplier with no base stated.
- **Every caveat is glued to its number**, inside the sentence, never a trailing parenthetical.
- **Every post is quoted verbatim**, including punctuation and capitalization. No cleanup.
- **No em dashes.** Comma, colon, period, parentheses.
- **Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.

---

```markdown
Skill: evergreen-repost-finder v1.1 | {N} posts | {first date} to {last date} | computed with code: {yes/no}

{DEPTH BANNER, only when span_days < 90 or the file cannot clear the 90-day reuse-safety gate for any post. Omit entirely when the shortlist has at least one entry.}

> **Depth needed.** This capture spans {span} days. This skill needs posts at least 90 days old before it will recommend reposting them, so it needs a capture spanning at least 90 days, ideally more. {If applicable: "The oldest post in this export is {age} days old, {N} days short of the gate."} Capture more with PostSnag and widen the window. Nothing below is fabricated to look useful; this is the honest list.

# Evergreen repost finder: {profile name or "your export"}

{N} posts, {first date} to {last date}, {span} days. {Era-adjusted scoring is active for this run, because the file clears N >= 21 and span >= 90 days. / Era-adjusted scoring is not active for this run, because {which precondition failed}; every score below is a multiple of the corpus median instead, and is labeled that way.}

Of these {N} posts: {X} clear the evergreen filter (not dated). Of those, {Y} are reuse-safe (90 days old or more). Of those, {Z} clear the 1.5x score floor. **{Z} posts make the shortlist.**

---

## Your evergreen shortlist

| Post, verbatim (truncated) | Score (denominator named) | Age | Evergreen class | Repost or remake | Why |
|---|---|---|---|---|---|
| "{hook}..." | {score}x era-adjusted, its 10-post neighborhood median was {era_median} | {age} days | CLEAN EVERGREEN | REPOST AS-IS | {one line} |
| "{hook}..." | {score}x era-adjusted, neighborhood median {era_median} | {age} days | CLEAN EVERGREEN | REMAKE | format-upgrade: {this type} median {x} is {ratio}x below {best type} median {y} |
| ... | | | | | |

{If any post excluded as DATED-BODY: "{N} more posts scored above the floor and are old enough, but were excluded: their body, not just the hook, makes a claim tied to when they were posted. The highest-scoring one: '{post}' ({date}), excluded because {the specific dated claim}."}

{Sanctioned optional paragraph, near-miss: a post that is reuse-safe and evergreen-clean but misses the 1.5x raw-value score floor by a narrow margin, and therefore belongs on neither the shortlist nor the watch list. Named rather than dropped: "One near-miss, named rather than dropped: '{post}' ({date}, {age} days old) clears the evergreen filter and the age gate cleanly. Its score displays as {rounded}x, but the unrounded value is {raw}x, {gap} under this skill's 1.5x floor. It is not on the shortlist and not on the watch list either, since the watch list is for posts that are not yet reuse-safe and this one already is. It is simply short on evidence, not on time; a stronger performance on a future post would be what moves it, not the calendar."}

---

## The refreshed drafts

{For every REMAKE entry, in shortlist order:}

**{rank}. {score}x | {evergreen class} | trigger: {which trigger(s) fired, named}**

Original, posted {date}:
> {full caption, verbatim}

Refreshed:
> {the refreshed draft}

**What changed and why:** {one to two sentences, naming the specific trigger and the specific fix}

{For REPOST AS-IS entries, one line: "No refresh needed. Repost this one exactly as it is."}

{Sanctioned optional paragraph, one per near-miss named in the shortlist section above: "No draft for '{post}'. It is a near-miss, not a shortlist member: it clears the evergreen filter and the age gate, but its raw score, {raw}x, is {gap} under the 1.5x floor even though it displays as {rounded}x. This skill does not draft refreshes for posts that did not clear the shortlist."}

---

## Watch list: high scores that are not reuse-safe yet

{Posts scoring >= 1.5x but under the 90-day gate, soonest-available first.}

| Post, verbatim (truncated) | Score | Age | Clears on |
|---|---|---|---|
| "{hook}..." | {score}x | {age} days | {exact date} |
| ... | | | |

{One line on the sharpest example: "Your single highest-scoring post in this file, at {score}x, is {age} days old and needs {N} more day(s). It is not on the shortlist above for exactly that reason."}

---

## What this analysis is standing on

Analyzed {N} posts captured {first date} to {last date}, {span} days. {If era-adjusted: "Scores are era-adjusted, each post against the median of its own 10 nearest neighbors by publish order, per this skill's rubric." / If corpus-multiple: "This capture does not clear the 90-day span era adjustment needs, so scores are each post's multiple of the corpus median of {corpus_median}, not an era score."} The reuse-safety age gate is 90 days, a working number, not a platform fact. {N_excluded} posts excluded as dated in the body, not just the hook. {N_watch} posts score high enough but are not old enough yet, listed on the watch list with the exact date each one clears the gate.

Not in your export, so not in this analysis: sponsored or paid-partnership flags, so this cannot tell you if a recommended post was originally boosted. Per-emoji reactions. Reach or impressions. Follower history, so era adjustment reduces but does not remove the confound between an old audience size and a new one.

PostSnag captures what you scrolled, so this is a sample of the account, not its full history.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

This analysis is for your own use. If you publish it, remove the analyzed account's name and the verbatim quotes; the numbers are yours to keep, the other creator's words are not.

Analysis based on {N} captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=evergreen-repost-finder
```

---

## Section-by-section notes for whoever fills this

**The gate-funnel line ("Of these N posts...").** This single sentence is the most important line in the whole output on a thin file. It tells the user exactly which gate is throwing posts out, evergreen filter, age, or score, rather than leaving them to guess why the shortlist is short.

**The shortlist table.** Score always carries its denominator in the same cell, not just in prose above the table, because a table gets copied out of context more often than the paragraph around it.

**The refreshed drafts section.** Original and refreshed are always shown together. Never the refreshed draft alone; the user cannot judge a fix they cannot compare against the thing being fixed.

**The watch list.** This is not a consolation section. On most real captures it will be longer and more interesting than the shortlist, especially early on, and it is where the single sharpest "your best post needs N more days" line usually lives. Always compute and state that line when the watch list is non-empty.

**The footer.** Never softened, never moved, never dropped when the shortlist was thin or empty. A thin or empty shortlist is exactly when the footer is doing the most work.
