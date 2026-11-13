# output-template.md

The exact structure the user receives. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line.

For this template filled with real computed numbers, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **The lite-mode banner goes at the top**, before the style profile, where the user sees it while forming their expectations.
- **Every caveat is glued to its number, inside the sentence.** Never a trailing parenthetical.
- **Every hook and drafted caption is shown in full**, not summarized.
- **No em dashes.** Comma, colon, period, parentheses.
- **Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.
- **The style profile comes first, the captions come second.** The user sees the analysis before the output it produced, so a check against their own export is possible before they act on anything.

---

```markdown
Skill: facebook-caption-writer v1.1 | {N} posts | {first date} to {last date} | computed with code: {yes/no}

{LITE-MODE BANNER, only when posts < 40 or span < 60 days. Omit entirely in full mode.}

> **Lite mode.** This capture has {N} posts across {span} days. Below 40 posts or 60 days this analysis runs shallow on purpose: {specific list of what is thinner, usually the style-source set size and the range of model posts}. To get a wider range of model posts, capture about {specific number} posts across {specific span}.

# Caption style: {profile name or "your export"}

{N} posts, {first date} to {last date}, {span} days. Style-source set: the top {k} posts by engagement, cut value {cut}.{ One post is {x} percent of the style-source set's total engagement, so its habits carry extra weight below.}

---

## Your caption style, measured

**Opening-line pattern.** {archetype table: archetype | count | share of style-source set}. Your default opening move: {archetype}, {n} of {k} posts.

**Sentence-length rhythm.** Median {x} words per sentence across your style-source set, range {min} to {max}. That is the {short/medium/long} band. {Tight/loose} rhythm ({standard deviation} words standard deviation). {n} of {k} posts sit in the {band} band.

**Line-break and whitespace style.** {n} of {k} style-source posts use {dominant structure, stated as lines and blank-line placement}. {Named exceptions and what they do differently.}

**Emoji usage.** {N} emoji across {k} style-source posts. {If 0: "This creator does not use emoji in her winning posts. A generated caption should not add one." If more than 0: top emoji and typical position.}

**CTA placement and phrasing.** {N} of {k} posts carry an explicit platform CTA (comment, follow, tag, share). {M} of {k} posts close on a bare imperative sentence, a direct instruction rather than a platform ask.{ Examples: "{closing line}", "{closing line}".}

**Hashtag behavior.** {N} hashtags across {k} posts. {If 0: "Does not use hashtags." If more than 0: repeated tags and typical position.}

**Capitalization habits.** {N} of {k} hook lines use sentence case. {N} ALL-CAPS words across the set. {Numeral-versus-spelled-out pattern: hook leads use {digits/spelled out}; body list markers use {digits/spelled out}, stated separately if both occur.}

**Question frequency.** {N} of {k} style-source posts open with a question.{ Cross-check note if this equals the Question Open archetype count: "Same {n} posts as the Question Open row above, not a second finding."}

**First-versus-second person.** {N} of {k} in second person, {M} in first person, {X} mixed.{ One line on how first person is used, if present.}

{Wider-catalog findings, only if one or more of `caption-mechanics-catalog.md`'s 24 mechanics fired strongly on the style-source set: "{Mechanic name}: {N} of {k} posts, with the example}." Omit this line entirely rather than forcing a finding that did not clear the bar.}

---

## 3 captions for: {the user's topic}

{Repeat this whole section once per topic, up to 3 topics maximum per run. If more than 3 topics were supplied, say so plainly and name what a follow-up run would cover.}

**Option 1**

Modeled on: {engagement} engagements | {archetype} | "{model post's hook, verbatim, truncated}"

> {new caption, full text, matching the model's rhythm, structure, and mechanics}

*Matching: {one line naming the 2 or 3 mechanics this option leans on hardest, e.g. "the same story-cold-open archetype and the same tight medium-band rhythm as the model post"}*

**Option 2**

Modeled on: {engagement} engagements | {archetype} | "{model post's hook, verbatim, truncated}"

> {new caption, full text}

*Matching: {one line}*

**Option 3**

Modeled on: {engagement} engagements | {archetype} | "{model post's hook, verbatim, truncated}"

> {new caption, full text}

*Matching: {one line}*

---

## What this is standing on

Analyzed {N} posts captured {first date} to {last date}, {span} days. Style-source set: top {k} posts by engagement, cut value {cut}. Every mechanic above was measured on this set, not on the full account. {Any concentration flag, restated in one clause.} {If lite mode: the specific thing that is thinner and the specific capture depth that fixes it.}

Not in your export, so not in this analysis: sponsored or paid-partnership flags, so a boosted post's caption looks identical to an organic one here. Per-emoji reactions, so this cannot tell you which emoji, if any, earns reactions. Reach or impressions.

PostSnag captures what you scrolled, so this is a sample of the account, not its full history.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

Analysis based on {N} captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-caption-writer
```

---

## Section-by-section notes for whoever fills this

**The header line.** States the style-source set's size and cut value before a single mechanic is shown, so the reader knows how many posts the rest of the page is standing on.

**The style profile.** All 9 mechanics, always in the same order, always with a number attached. A mechanic with a zero finding (no emoji, no hashtags) gets stated as plainly as a mechanic with a rich finding. Zero is data.

**The 3 captions.** Model label first, so the reader can go find the real post before reading the new one. The caption itself is shown in full inside a blockquote, never trimmed. The "Matching" line names what to check the draft against, which doubles as a receipt that the self-check pass in `rubric.md` section 4 actually ran.

**The footer.** Never softened, never moved, never dropped when the style-source set was thin. A thin sample is exactly when the footer is most useful.
