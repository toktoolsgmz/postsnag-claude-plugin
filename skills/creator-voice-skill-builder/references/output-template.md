# output-template.md

The exact structure the user receives when this skill runs, and, inside it, the exact shape of the two finished files it produces. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line.

This file shows the shape with slot annotations. It is not a worked example: no real numbers below are computed from a real file. For the same structure filled with real computed numbers from the shared synthetic dataset, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **The lite-mode or small-sample banner goes at the top**, before anything else, where the user sees it before forming expectations about what they are about to get.
- **The promo screen's manual review list is shown in full**, every flagged post, never summarized to "N posts flagged, all cleared." A summary is exactly the silent exclusion this skill's own rubric forbids.
- **Every caveat is glued to its number, inside the sentence.** Never a trailing parenthetical.
- **No em dashes. Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.

---

```markdown
Skill: creator-voice-skill-builder v1.1 | {N} posts | {first date} to {last date} | computed with code: {yes/no}

{SMALL-SAMPLE OR LITE-MODE BANNER, only when the style-source set is qualitative (under 15 posts) or the export is under 40 posts / 60 days. Omit entirely otherwise.}

> {If qualitative: "Under 15 posts, so this is a reading of a small sample, not a measurement. The voice profile below describes {N} posts you gave me, not a statistically ranked style."}
> {If lite mode: "This capture has {N} posts across {span} days. Below 40 posts or 60 days, your style-source set is smaller than full mode: roughly {n} posts instead of 15. The voice profile below is real, built on less evidence, and the recipe says so at every section where it thins out."}

# Building {creator name}'s voice skill

{N} posts, {first date} to {last date}, {span} days.

---

## Your style-source set

Top {k} posts by engagement, cut value {cut}. {Concentration check result, all three parts named, flag or no flag stated with the actual numbers.}

---

## The promo screen

{Marker hits by category, with counts: "{n} posts matched a partnership or sponsorship marker. {n} posts matched a discount-code marker. {n} posts matched a link-out marker ({n} structural, by post type; {n} by phrasing)."}

**Manual review list** ({n} posts, every one shown, none summarized away):

| Date | Type | Engagement | Marker matched | Excerpt or Link_URL domain |
|---|---|---|---|---|
| {date} | {type} | {engagement} | {category and exact trigger} | {excerpt or domain} |
| ... | | | | |

**Your decision, recorded:** {which posts, if any, were excluded as promotional, and which were confirmed as legitimate style-source posts despite the flag, with the one-line reason for each}.

{If zero posts were flagged: "No posts in the style-source set matched any marker. That does not prove none of your posts were ever promotional, only that none in your top {k} used the language this screen checks for."}

---

## Your voice, measured

{Condensed 9-mechanics table or list, one line per mechanic, cited to `facebook-caption-writer/references/rubric.md` section 2, with the measured number for each.}

---

## Your two finished files

### File 1: `{creator-name}-voice-writer/SKILL.md` (from `voice-skill-template.md`)

{The filled template, shown in full: frontmatter, voice profile, example posts with evidence, the "how to write a new caption" steps, the three fixed guardrails, the self-check list.}

### File 2: `{creator-name}-voice-writer/references/style-playbook.md` (from `style-playbook-template.md`)

{The filled companion: hook patterns, rhythm and structure, vocabulary and mechanics, the never-do list, the maintenance instruction.}

---

## The 3-test acceptance run

**Test 1: {a covered topic}.** {Drafted output.} {Self-check result, item by item or summarized as "N of 11 checks passed."} **{PASS or FAIL, one word, then the one-line reason.}**

**Test 2: {an uncovered, in-niche topic}.** {Drafted output.} {Self-check result.} **{PASS or FAIL, one-line reason.}**

**Test 3: {an out-of-niche topic}.** {Drafted output.} {Self-check result on the 11 mechanical items, separately from whether the out-of-niche disclosure fired.} **{PASS or FAIL, graded on the disclosure firing, not just the mechanical checks, per `rubric.md` section 5.}**

---

## Keeping it current

{The maintenance habit, stated as an instruction: the first correction goes into the file, not into memory. Name which of the two files a given kind of correction belongs in.}

---

## What this build is standing on

{Honesty footer: N posts, date range, span, style-source set size and cut value, concentration check result restated, promo screen result restated, what is not in the export, PostSnag captures what you scrolled.}

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

This analysis is for your own use. If you publish it, remove the analyzed account's name and the verbatim quotes; the numbers are yours to keep, the other creator's words are not.

Analysis based on {N} captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=creator-voice-skill-builder
```

---

## Section-by-section notes for whoever fills this

**The promo screen table.** This is the section most likely to get compressed under time pressure. Do not compress it. Every flagged post gets its own row, even when the answer is obviously "this is fine," because the review list existing in full is the entire honesty mechanism this section relies on.

**The two finished files.** Shown here in full, not linked or summarized, because the user's actual deliverable is these two files, not a description of them. If the output makes the user go dig for the real templates, the recipe did not finish its job.

**The acceptance run.** Three tests, three explicit pass or fail calls. Test 3's grading criterion is different from the other two and the output has to say so in the same sentence as its verdict, not leave the reader to infer it from the rubric.

**The footer.** Never softened, never moved, never dropped when the build ran on a thin sample. A thin sample is exactly when the footer is most honest.
