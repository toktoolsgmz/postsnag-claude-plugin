# output-template.md

The exact structure the user receives. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line.

For this template filled with real computed numbers, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **The lite-mode banner goes at the top**, before the findings, where the user sees it while forming their expectations. Not at the bottom where it reads as an excuse.
- **Every caveat is glued to its number, inside the sentence.** Never a trailing parenthetical.
- **Every post is quoted verbatim**, including punctuation. No cleanup.
- **No em dashes.** Comma, colon, period, parentheses.
- **Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.
- **No real name ever appears.** Recurring authors are Author A, Author B, Author C, never the value from the `Author` column.
- **The confound column, when present, never reads "none."** It reads a named flag, "checked, no confound," or "not checked."

---

```markdown
Skill: facebook-group-post-analyzer v1.1 | {N} posts | {first date} to {last date} | computed with code: {yes/no}

{LITE-MODE BANNER, only when posts < 40 or span < 60 days. Omit entirely in full mode.}

> **Lite mode.** This group capture has {N} posts across {span} days. Below 40 posts or 60 days this analysis runs shallow on purpose: {specific list of what is degraded}. To get {the named section}, capture about {specific number} posts from this group.

# Group analysis: {group name or "your group export"}

{N} posts, {first date} to {last date}, {span} days, {N_authors} distinct authors. This group's export carries no media columns, so this analysis is text and engagement only.

Median engagement across the group: {median}. Engagement here means reactions plus comments plus shares.

---

## What wins in this group

| Type | Posts | Median engagement | Mean engagement | Concentration flags | Best example, verbatim |
|---|---|---|---|---|---|
| {type} | {n} | {median} | {mean} | {flags or "none"} | "{content, truncated}" ({engagement}) |
| ... | | | | | |

**Ranked by median engagement.** {If mean ranking disagrees, say so and name the posts responsible.}

**Too small to rank, listed because they matter:** {type} ({n} posts, median {median}), {type} ({n} posts, median {median}). {One line on the most interesting one, and the overlap check with promo-marked posts if it applies.}

---

## The group's norms

**Length.** Median post: {N} words. {table: band | n | median | rankable?}. {One or two sentences on the cleanest band, with the author-concentration caveat if 3.1's check applies.}

**Tone.** First-person posts: {x} percent ({n} of {N}), median {median}{, one concentration flag if it fired}. Not first-person: {n} posts, median {median}{, rankable and clean, or "too small to rank" if under the floor, whichever is actually true this run}. Question-mark posts: {x} percent ({n} of {N}), median {median}. {State plainly whether this cleared its concentration check or was excluded, and why, per rubric.md section 3.2.}

**Promo tolerance.** The marker list this run checked: {list}. {The false-positive risk, one or two sentences.} Promo-marked posts: {n}, median {median}, {rankable or too small to rank}. Not promo-marked: {n}, median {median}. {One sentence stating the gap plainly.}

---

## Who wins repeatedly (anonymized)

{For each author with n >= 3, ranked by median descending:}

**Author {letter} | {n} posts, median {median}{, concentration flags if any}**

{The mechanical pattern their posts share: type mix, length band, tone markers, any recurring structure, in 1 to 3 sentences.}

{If fewer than 2 authors clear the 3-post floor, say so plainly: "Only {n} author(s) in this capture posted 3 or more times, so this section is thinner than usual. More posts from more repeat posters will fill it out."}

---

## Best days to post

{One sentence stating this is day-of-week only, and why, citing best-time-to-post-reader.} `Posted`'s timezone is not stated in the export, so treat any day-of-week finding as relative, not as clock-time advice.

| Day | Posts | Median engagement | Rankable? | Concentration flags | Format confound |
|---|---|---|---|---|---|
| {day} | {n} | {median} | {yes/no} | {flags or "none"} | {named flag / "checked, no confound" / "not checked"} |
| ... | | | | | |

{The single sentence naming the best rankable day, with its confound caveat glued on if one fired.}

{Too-small-to-rank days, listed with n and median, not ranked.}

---

## 3 posts drafted for this group

**1. {label: highest-confidence norm draft}**

> {draft, verbatim}

**Satisfies:** {list the norms this draft matches, each citing its section: length band from norms, tone from norms, type from the type ranking.}

**2. {label: modeled on Author {letter}'s pattern, not their identity}**

> {draft, verbatim}

**Satisfies:** {the mechanism borrowed, named, plus which norms.}

**3. {label: a test of {type or band}, not a repeat}**

> {draft, verbatim}

**Satisfies:** {state plainly this is a test of an unranked signal, not a confirmed finding, and why it is worth testing anyway.}

---

## What this analysis is standing on

Analyzed {N} posts from {N_authors} authors, captured {first date} to {last date}, {span} days. Rankings use median engagement, reactions plus comments plus shares, unweighted. Buckets under 5 posts are listed but not ranked. {Any concentration flags that fired, restated in one clause each.} {The format-confound result on the ranked day, restated in one clause.}

Promo-marker detection is a language heuristic, not a captured field. It will miss posts that avoid its marker list and can flag genuine posts that happen to use a marker phrase. Read the flagged posts before treating the list as a verdict.

Not in your export, so not in this analysis: sponsored or paid-partnership flags. Per-emoji reactions. Comment text. Reach or impressions.

This group's export carries no media columns, so nothing here describes an image or a video's content, only its engagement.

PostSnag captures what you scrolled, so this describes the posts in your export, not the group's full archive.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

Analysis based on {N} captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-group-post-analyzer
```

---

## Section-by-section notes for whoever fills this

**The header line.** Post count, span, and author count before any finding, same discipline as every other skill in the catalog: a reader who cannot see the denominator cannot judge the table below it.

**The type table.** "Best example, verbatim" lets the reader go check the claim against a real post. If a type's low median overlaps with the promo-marked bucket, say that in the same breath as the ranking, not three paragraphs later where it reads like a footnote.

**The norms block.** Three subsections, three formulas, no exceptions. If a tone marker failed its concentration check (question marks, in the worked example), report that it was checked and excluded, with the reason, rather than omitting it. Silence here reads as "we did not look," when the truth is "we looked and it did not hold up," and those are different findings.

**The author section.** Never fewer than 3 posts to qualify, never a real name in the output. If only one author qualifies, or none do, say so rather than stretching the section to look fuller than the data supports.

**Best days to post.** One rankable day is a common, honest outcome on a group capture. The confound column carries real information even on a single ranked row; do not skip it because there is only one row to fill.

**The 3 drafts.** Each one names, in one line, exactly which findings it is trading on. A draft with no citation is a guess wearing this skill's output format.

**The footer.** Never softened, never moved, never dropped when the analysis was thin. A thin capture is exactly when the footer earns its keep.
