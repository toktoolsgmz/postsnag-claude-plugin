# output-template.md

The exact structure the user receives. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line.

For this template filled with real computed numbers, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **The lite-mode banner goes at the top**, before the findings, where the user sees it while forming their expectations. Not at the bottom where it reads as an excuse.
- **Every caveat is glued to its number, inside the sentence.** Never a trailing parenthetical, because a trailing parenthetical gets trimmed downstream and the caveated claim ships flat.
- **Every hook is quoted verbatim**, including its punctuation and capitalization. No cleanup.
- **No em dashes.** Comma, colon, period, parentheses.
- **Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.

---

```markdown
Skill: facebook-hook-analyzer v1.1 | {N} posts | {first date} to {last date} | computed with code: {yes/no}

{LITE-MODE BANNER, only when posts < 40 or span < 60 days. Omit entirely in full mode.}

> **Lite mode.** This capture has {N} posts across {span} days. Below 40 posts or 60 days this analysis runs shallow on purpose. Degraded here: {specific list of sections}. To get {the named section}, capture about {specific number} posts across {specific span}.

# Hook analysis: {profile name or "your export"}

{N} posts, {first date} to {last date}, {span} days. {N_hooks} posts had captions and were classified. {N_nocaption} had none and are counted in the engagement totals only.{ Skipped {N_cta} leading call-to-action lines to reach the real hook.}

Median engagement across the whole capture: {median}. Engagement here means reactions plus comments plus shares.

---

## Your hook patterns

| Archetype | Posts | Median engagement | Share of your top {k} | Best example, verbatim |
|---|---|---|---|---|
| {archetype} | {n} | {median} | {x} of {k} | "{hook}" ({engagement}) |
| ... | | | | |

**Ranked by median engagement.** {If the mean-based ranking differs in the top 3: "Ranked by average instead, {A} would be first and {B} third. {post description} and {post description} are the entire difference. The median ranking is the one above, because it describes what happens when you write a normal post."}

**Too small to rank, listed because they matter:** {archetype} ({n} posts, median {median}), {archetype} ({n} posts, median {median}). {One sentence on the most interesting one. An archetype used 4 times that won 4 times is the most actionable line on this page and it does not get a rank number because 4 posts is not a measurement.}

{Concentration flags, one line each, written inline with the number:}
{"{Archetype} sits at a median of {median} across {n} posts, but one post accounts for {x} percent of that archetype's total engagement. Treat the median as the honest number and the average as noise."}

{If any UNCLASSIFIED: "{n} hooks matched no archetype and are excluded from the table."}

---

## What you over-invest in and what you under-invest in

| Archetype | Share of your posts | Share of your top {k} |
|---|---|---|
| {archetype} | {x} percent ({n} of {N}) | {y} percent ({c} of {k}) |
| ... | | |

{One or two sentences naming the biggest divergence in each direction. This is the recommendation. It should be quotable and it should be checkable from the table directly above it.}

**Top 10 versus bottom 10:** {archetype breakdown of each set, then the single sharpest contrast in one sentence.}

---

## The structural read

{Only buckets with 5 or more posts are ranked. Under-5 buckets are shown with their numbers and marked unranked.}

| Feature | Bucket | Posts | Median engagement |
|---|---|---|---|
| Hook length | 0-50 chars | {n} | {median} |
| Hook length | 51-75 chars | {n} | {median} |
| Hook length | 76-100 chars | {n} | {median} {unranked if n<5} |
| Hook length | 101+ chars | {n} | {median} {unranked if n<5} |
| Caption length | 0-250 chars | {n} | {median} |
| Caption length | 251-400 chars | {n} | {median} |
| Caption length | 401+ chars | {n} | {median} {unranked if n<5} |
| Question mark in hook | yes | {n} | {median} |
| Question mark in hook | no | {n} | {median} |

{Any feature with no variance in this capture gets one line saying so, rather than being dropped: "Every caption here uses the same paragraph structure, so there is no signal to read on paragraphing."}

{No character limit is asserted anywhere in this section. Facebook's truncation point varies by surface and changes without notice. Hooks over 120 characters are flagged as at risk of needing a second rendered line, and 120 is this skill's working flag, not a platform fact.}

---

## Visual hooks

{IF the user supplied screenshots or the media zip:}

Read the {n} images you supplied.

| Post | Muted test | On-screen text | Cross-check with the text hook |
|---|---|---|---|
| "{hook, truncated}" | {stops the scroll / does not, and what does the stopping} | "{verbatim}" / NONE / UNREADABLE | distinct / redundant / resolved |

{One paragraph on the pattern across the images you saw, scoped to that count.}

{IF NOT:}

Not analyzed. Your export carries `Media_URLs`, but those are expiring Facebook links and this skill never fetches them. Paste screenshots or supply the media zip from your capture and rerun to get this section.

---

## Your top 10 hooks, as templates

{For each of the 10, in engagement order:}

**{rank}. {engagement} engagements | {archetype}**

> {hook, verbatim}

**Template:** `{the abstracted fill-in pattern}`
**Use it for:** {one line: what kind of post this opens}

---

## 5 archetypes to test next

{For each, in tier order. Label the tier with the word UNDERUSED or UNEXPLORED.}

**{n}. {Archetype} | {UNDERUSED: {n} posts, median {median}, which is {x}x your corpus median / UNEXPLORED: never used as an opening line}**

{Why it fits this creator, in one or two sentences, citing something from their actual posts. For an unexplored archetype found by the latent-fit test, say so directly: "You already write this. It appears in the body of {n} of your posts and has never once been your first line."}

**Drafted for you:** "{a hook in the creator's own topics, not a generic example}"

---

## What this analysis is standing on

Analyzed {N} posts captured {first date} to {last date}, {span} days. {N_nocaption} posts excluded from hook analysis for empty captions, still counted in engagement totals. Rankings use median engagement, which is reactions plus comments plus shares, unweighted. Archetypes with fewer than 5 posts are listed but not ranked. {Any concentration flags that fired, restated in one clause each.}

{If lite mode: the specific missing thing and the specific capture depth that fixes it.}

Not in your export, so not in this analysis: sponsored or paid-partnership flags, so a boosted post looks identical to an organic one here. Per-emoji reactions. Reach or impressions. Comment text. Follower history.

PostSnag captures what you scrolled, so this is a sample of the account, not its full history.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

Analysis based on {N} captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-hook-analyzer
```

---

## Section-by-section notes for whoever fills this

**The header line.** Three numbers before any finding: how many posts, over how long, how many had captions. A reader who cannot see the denominator cannot judge anything below it.

**The pattern table.** Best example is quoted verbatim with its engagement attached, so the reader can go look at the post. A pattern table without examples is a spreadsheet.

**The over-invest / under-invest table.** This is the section the user acts on. Keep it to the archetypes where the two shares actually diverge; listing all 12 rows when 8 of them match buries the two that do not.

**The structural read.** Short. Two or three real findings. If the buckets are too thin to say anything, say that in one line and move on rather than padding.

**The top 10 templates.** Verbatim first, template second, always in that order. The verbatim line is the proof; the template is the product.

**The gap list.** Every drafted hook uses the creator's own subject matter. If a draft would work unchanged for any creator in any niche, it is wrong and it tells the reader the analysis did not read their file.

**The footer.** Never softened, never moved, never dropped when the analysis was thin. A thin analysis is exactly when it is most honest.
