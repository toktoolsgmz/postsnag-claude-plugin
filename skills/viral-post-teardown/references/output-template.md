# output-template.md

The exact structure the user receives. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line.

For this template filled with real computed numbers, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **The honesty line about one post opens the output, not the footer.** A single post cannot support a ranking or a baseline, and the reader needs to know that before the findings, not after.
- **Every hook, thesis line, and CTA is quoted verbatim**, including punctuation and capitalization. No cleanup.
- **Every "why it worked" finding names a specific, visible feature.** No finding that could be pasted under a different post unchanged.
- **No em dashes.** Comma, colon, period, parentheses.
- **Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.

---

```markdown
Skill: viral-post-teardown v1.1 | 1 post | computed with code: {yes/no}

# Teardown: {a short label for the post, drawn from its topic, not a generic title}

{One line: read from text or from a screenshot, and whether engagement numbers were supplied.}

One post cannot prove a pattern. This is a qualitative read of what this post does, not a measurement of whether it is typical or repeatable. For that, run this on a body of posts.

---

## Hook classification

**{Archetype}** | marker that fired: {the specific recognition marker, named}

> "{hook, verbatim}"

{One or two sentences on why the ladder landed here, naming any archetype it was borderline against and why the call went the way it did.}

---

## Structure map

**Hook** ({word count} words): {quote or close paraphrase}

**Build** ({word count} words across {N} paragraphs): {what it does: the context, tension, or evidence it sets up}

**Payoff** ({word count} words): {quote or close paraphrase of the result or reveal}{, plus the thesis line if the post carries one, quoted verbatim and named as the most shareable line if it reads as a standalone claim}

**CTA**: {quote, verbatim} {OR, if none: "No explicit CTA. The post closes on {the thesis line / the payoff}, which reads as a statement rather than an invitation."}

---

## Pacing read

{N} sentences across {N} paragraphs, averaging {N} words per sentence. Sentence mix: {N} short (under 10 words), {N} medium (10 to 20), {N} long (21 or more).

{If a short-short run exists: "Paragraph {N} opens with a {N}-word sentence followed by a {N}-word sentence, back to back, before a longer sentence lands the real content. That is a deliberate build in tension through rhythm."}

{If any paragraph runs to 41 words or more: "Paragraph {N}, at {N} words, is the densest block in the post and asks more of a scrolling reader than the paragraphs around it."}

{One line on paragraph rhythm: whether each beat of the structure map gets its own paragraph, or whether beats run together.}

---

## Visual hook

{IF a screenshot was supplied:}

Muted test: {stops the scroll / does not, and what does the stopping}.
On-screen text: "{verbatim}" / NONE / UNREADABLE.
Cross-check with the text hook: {distinct angles / redundant / resolved}.

{IF NOT:}

Not analyzed. No screenshot was supplied. Paste one and rerun to get this section.

---

## Why it worked

{Up to 3 findings. Each numbered, each tied to a named, visible feature. Never more than 3.}

1. {Finding, naming the feature and its plausible effect.}
2. {Finding.}
3. {Finding.}

---

## Engagement read

{IF numbers were supplied:}

{Reactions} reactions, {comments} comments, {shares} shares. Engagement (reactions plus comments plus shares): {total}. Comment ratio: {x}%. Share ratio: {y}%.

No baseline exists for one post, so these numbers describe this post, they do not rank it against anything. {One sentence tying one ratio to a feature already named above, phrased as a description, not a measurement.}

{IF NOT:}

Not computed. No engagement numbers were supplied with this post.

---

## Reuse template

{One continuous fill-in block covering hook, build, payoff, and CTA, with the structural words kept and the specifics braced.}

```
{the template}
```

---

## What this teardown is standing on

One post, read once, for its hook, its structure, and its pacing. No ranking, no median, no archetype table: those require more than one post and this skill never produces them from a single one. {If numbers were supplied: "Engagement numbers were supplied and reported as raw counts and ratios, with no baseline, because no baseline exists for one post."} {If not: "No engagement numbers were supplied, so none are reported."} Not in this reading: whether the post was boosted, per-emoji reaction detail, reach or impressions, comment text, or anything about the account that posted it.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

Analysis based on 1 captured post. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=viral-post-teardown
```

---

## Section-by-section notes for whoever fills this

**The opening honesty line.** This is the one place in the whole catalog where the honesty rule opens the output instead of closing it, because the entire premise of this skill (one post, zero friction) is also its entire limitation, and the reader should know that before the first finding, not after three findings that read like measurements.

**The hook classification.** State the marker that actually fired, not just the archetype name. "Marker that fired: first-person subject, past-tense single event, time anchor (on a Tuesday)" is checkable. "It is a Story Cold Open" is not.

**The structure map.** Word counts on every beat. A structure map without counts is four labels on four paragraphs; the counts are what let the pacing read and the structure map cross-check each other.

**Why it worked.** Three is a ceiling, not a target. Two sharp findings beat three where the third is padding.

**The reuse template.** One block, not four fragments. The user should be able to read it top to bottom and see the whole post's shape at once.

**The footer.** `N` in the pointer line is 1 for a single-post run. If the user pasted multiple posts in one message and this skill produced multiple teardowns, each teardown's pointer line uses its own count of 1; the skill does not pool them into a false plural.
