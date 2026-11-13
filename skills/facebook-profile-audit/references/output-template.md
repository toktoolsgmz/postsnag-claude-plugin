# output-template.md

The exact structure the user receives. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line.

For this template filled with real computed numbers, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **The lite-mode banner goes at the top**, before any finding, where the user sees it while forming their expectations. Omit entirely in full mode.
- **Every caveat is glued to its number, inside the sentence.** Never a trailing parenthetical.
- **Every ranked bucket's check columns are filled in, every time, even when nothing flagged.** A bucket that was never rankable (n<5) gets `not checked` in every check column, never `none`, because `none` claims a result that was never computed.
- **No em dashes.** Comma, colon, period, parentheses.
- **Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.
- **Topics are additive, formats are exclusive.** Say this once, in the topic section, because a reader who sees topic percentages that do not sum to 100 needs to know why.

---

```markdown
Skill: facebook-profile-audit v1.1 | {N} posts | {first date} to {last date} | computed with code: {yes/no}

{LITE-MODE BANNER, only when posts < 40 or span < 60 days. Omit entirely in full mode.}

> **Lite mode.** This capture has {N} posts across {span} days. Below 40 posts or 60 days this analysis runs shallow on purpose. Degraded here: {specific list, e.g. "the topic table has only 1 of {C} clusters clearing the ranking floor, and there is no trajectory section"}. To unlock {the named section}, capture about {specific number} posts across {specific span}.

# Profile audit: {profile name or "your export"}

{N} posts, {first date} to {last date}, {span} days. Format mix: {type}: {n} ({x}%), {type}: {n} ({x}%), ... Corpus median engagement: {median}. Engagement here means reactions plus comments plus shares.

---

## What works

**1. {Finding name}**

{Bucket}, {n} posts, median {median} against your corpus median of {corpus_median}.{ Glued caveat if a flag fired.} {One or two sentences on why this is worth acting on, citing a specific example post verbatim.}

**2. {Finding name}**

{Same structure.}

**3. {Finding name}**

{Same structure. If this is a thin-but-real finding (n below 5, "too small to rank"), label it explicitly as untested rather than proven.}

---

## What does not work

**1. {Finding name}**

{Bucket}, {n} posts, median {median}, {x} percent of your top {k} despite {y} percent of your total posts. {One or two sentences on the gap.}

**2. {Finding name}**

{A clean, unflagged, ranked bucket sitting below the corpus median, or a genuine absence from the top quartile.}

**3. {Finding name}**

{If nothing in the file is a dramatic failure, this is a stated null result: a ranked, unflagged bucket sitting within a small margin of the corpus median. Say it is tested and flat, not hidden.}

---

## Format distribution

| Type | Posts | Median | Mean | Share of corpus | Share of top {k} | Median after top removed | Change | Top post's share | Mean / median | Rankable |
|---|---|---|---|---|---|---|---|---|---|---|
| {type} | {n} | {median} | {mean} | {x}% | {c} of {k} | {value or "not checked"} | {value or "not checked"} | {value or "not checked"} | {value or "not checked"} | yes / **no, n<5** |
| ... | | | | | | | | | | |

---

## Topic clusters

Topics are extracted mechanically from `Content` and are additive: a post can belong to more than one cluster, unlike format, which is exactly one value per post. Full extraction method: `references/rubric.md` section 2.

| Topic | Posts | Median | Mean | Median after top removed | Change | Top post's share | Mean / median | Rankable |
|---|---|---|---|---|---|---|---|---|
| {topic} | {n} | {median} | {mean} | {value or "not checked"} | {value or "not checked"} | {value or "not checked"} | {value or "not checked"} | yes / **no, n<5** |
| ... | | | | | | | | |

{N_discarded} candidate topic heads were discarded as non-topics (verbs, time words, generic pronouns) before this table was built.

---

## Cadence

{N} posts across {span} days, {posts_per_week} posts per week. Gap between posts: median {median_gap} days, minimum {min_gap}, maximum {max_gap} (between {date} and {date}).{ Same-day doubling: {date} carried {n} posts.}

Posting days: {day}: {n}, {day}: {n}, ... {One line noting which days carry little or no volume, described as untested, never as underperforming: that read belongs to Best Time to Post Reader.}

---

## Video: views and duration

{IF video rows with populated Views exist:}

{n} of your {n_video} video posts carry `Views`. Raw engagement across them spans {min} to {max} ({x}x). Engagement per view spans {min}% to {max}% ({y}x). {One sentence on what a flat rate against a wide raw spread means, or the reverse.}

| Duration band | Posts | Median | Mean / median | Top post's share | Rankable |
|---|---|---|---|---|---|
| Short (<=40s) | {n} | {median} | {value or "not checked"} | {value or "not checked"} | yes / **no, n<5** |
| Medium (41-70s) | {n} | {median} | {value or "not checked"} | {value or "not checked"} | yes |
| Long (71s+) | {n} | {median} | {value or "not checked"} | {value or "not checked"} | yes |

{If a band flags 2 or more checks: state plainly that it does not become a recommendation, and name the specific post(s) driving it instead.}

{IF NOT:}

Not analyzed. No video rows in this export carry a populated `Views` value.

---

## 5 patterns worth stealing

{For each, in evidence-tier order (real ranked bucket with a caveat, first; thin or single-post evidence, last):}

**{n}. {Pattern name}**

{The signal, instantiated with this profile's real numbers.} {The recommendation the pattern generates, one sentence, something the reader could start on tonight.}

---

## Your 30-day list

{Numbered. Every item names the finding it traces back to.}

1. {Action.} ({Traces to: "What works" finding 1 / "What does not work" finding 2 / steal-worthy pattern 3, etc.})
2. ...

---

{TRAJECTORY SECTION, only if span >= 90 days and not lite mode. Omit entirely otherwise, with one line in the honesty footer explaining why it is absent.}

## Trajectory

Your earlier half ({first date} to {mid date}, {n} posts) sits at a median of {median}. Your later half ({mid date} to {last date}, {n} posts) sits at {median}, a ratio of {ratio}, which this audit calls **{rising / falling / flat}**.{ Concentration check on both halves: {result}.}

**PostSnag does not capture follower history.** The Markdown export carries a single point-in-time follower count and nothing else. This trajectory read cannot separate "the content got better" from "the audience got bigger" in the same window, and it does not claim to.

---

## What this audit is standing on

Analyzed {N} posts captured {first date} to {last date}, {span} days. Format and topic buckets under 5 posts are listed but not ranked. {Any concentration flags that fired, restated in one clause each.} {If no trajectory section ran, say why in one clause: "span was under 90 days" or "this capture ran in lite mode."}

Not in your export, so not in this audit: sponsored or paid-partnership flags, so a boosted post looks identical to an organic one here. Per-emoji reactions. Reach or impressions. Comment text. Follower history over time.

PostSnag captures what you scrolled, so this is a sample of the account, not its full history.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

Analysis based on {N} captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-profile-audit
```

---

## Section-by-section notes for whoever fills this

**The snapshot header.** Format mix in one line so the reader has the shape of the account before any finding lands. No finding in this output should surprise someone who just read the header.

**What works / what does not.** Three each, always. If the file genuinely does not hand you a dramatic failure, the third "does not work" slot is a stated null result, not a stretch.

**The format and topic tables.** Every rankable bucket's check columns are filled with real numbers. Every unrankable bucket's check columns say `not checked`, in every column, because the check was never run and `none` would claim otherwise.

**The video section.** Omitted cleanly, in one line, when no video rows carry `Views`. Never padded with a guess.

**The steal-worthy patterns.** Pulled from `findings-pattern-library.md`, always instantiated with this profile's actual numbers. A pattern description with no numbers attached is not a finding, it is the pattern library's blurb copied and pasted.

**The 30-day list.** Every line traces to a named finding. If a recommendation cannot be traced, it does not belong on the list.

**Trajectory.** Present only when it earns its place. Its confound sentence is never trimmed, softened, or moved.

**The footer.** Never softened, never moved, never dropped when the analysis was thin. A thin analysis is exactly when it is most honest.
