# output-template.md

The exact structure the user receives. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line.

For this template filled with real computed numbers, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **The timezone question comes first, before any other text, if it has not already been answered this run.** Nothing below it renders with a clock time until it is answered or explicitly declined.
- **The lite-mode and date-only banners go at the top**, before the findings, where the user sees them while forming their expectations, not at the bottom where they read as an excuse.
- **Every caveat is glued to its number, inside the sentence.** A concentration flag or a format-confound flag never sits in a trailing parenthetical.
- **No em dashes.** Comma, colon, period, parentheses.
- **Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.
- **The heat grid shows every day**, even the ones with too few posts to rank. A grid with rows missing looks like a bug, not like honesty.

---

```markdown
Skill: best-time-to-post-reader v1.1 | {N} posts | {first date} to {last date} | computed with code: {yes/no}

{TIMEZONE QUESTION, only if not already answered this run:}

Your Posted timestamps have no timezone attached. Are they in your local time, and if so which timezone? I need this before I can tell you what hour to post. Without it, I will describe your windows in relative terms only (evenings versus mornings) rather than clock times.

{DATE-ONLY BANNER, only if midnight_share > 0.5:}

> **Date-only capture.** More than half of your timestamps carry no time-of-day information, only a date. This is common on older posts. Every section below runs on day-of-week only. No time-of-day claim appears anywhere in this output.

{LITE-MODE BANNER, only when posts < 40 or span < 60 days. Omit entirely in full mode.}

> **Lite mode.** This capture has {N} posts across {span} days. Below 40 posts or 60 days this analysis runs shallow on purpose. Your day-of-week floor clears on {x} of your 7 days. Your day-by-time floor clears on {y} of 28 possible windows. To get a time-of-day answer worth trusting, capture about 60 posts across at least 60 days, so a thin weekday still lands 5 posts in one of four time bands.

# Best time to post: {profile name or "your export"}

{N} posts, {first date} to {last date}, {span} days. {If timezone confirmed: "Times below are in {timezone}, which you confirmed." If not: "Times below are relative only. No timezone was confirmed this run, so no clock time appears anywhere in this output."}

Engagement here means reactions plus comments plus shares. Corpus median: {median}.

---

## Your weekly heat grid

Each cell shows post count and median engagement. Cells below the 5-post floor show the count only and are not ranked.

| Day | Morning (5-11am) | Midday (11am-5pm) | Evening (5-9pm) | Night (9pm-5am) |
|---|---|---|---|---|
| Monday | {n}: {median or "n<5"} | {n}: {median or "n<5"} | {n}: {median or "n<5"} | {n}: {median or "n<5"} |
| Tuesday | ... | ... | ... | ... |
| Wednesday | ... | ... | ... | ... |
| Thursday | ... | ... | ... | ... |
| Friday | ... | ... | ... | ... |
| Saturday | ... | ... | ... | ... |
| Sunday | ... | ... | ... | ... |

{x} of 28 possible day-by-time windows clear the 5-post floor. The rest are shown with their count only.

---

## Your best days

{Rankable day-of-week buckets only, ranked by median.}

| Rank | Day | Posts | Median engagement | Flags |
|---|---|---|---|---|
| 1 | {day} | {n} | {median} | {concentration and/or confound flags, inline; if both checks ran and neither fired: "Concentration checked, clean. Format checked, no confound."; if a check did not run: "not checked"} |
| ... | | | | |

**The Flags column in the user-facing tables never says "none".** Every ranked row here has had both checks run on it, so the honest cell is either a named flag or an explicit statement that the check ran and cleared: "Concentration checked, clean. Format checked, no confound." "None" reads as clean whether or not anything was examined, and on a ranked row that the user is about to act on, that is the one ambiguity this column cannot afford. "Not checked" is the only acceptable way to say a check did not happen, and on a ranked row it should never be needed. (Inside the analyst's working tables in `example-run.md` Part 1 and the worksheet, the concentration column may read "none", because those tables list only rankable buckets and the check ran on all of them. The confound column has no such guarantee and always spells out its state.)

**Too small to rank:** {day} ({n} posts, median {median}), {day} ({n} posts, median {median}). {One sentence on the most interesting one if there is one.}

{If the top-3 median and mean rankings disagree: "Ranked by average instead, {A} would be first and {B} third. {post description} is the entire difference. The median ranking above is the one shipped, because it describes what a normal post on that day does."}

---

## Your best windows (day and time)

{Rendered ONLY in full mode, and only if at least one day x band cell clears n>=5. If none clear, this section is replaced with one paragraph: "No day-by-time window in this capture reaches 5 posts. The day-of-week ranking above is as fine-grained as this capture supports. Capture more and this section activates."}

{**In lite mode this table is not rendered at all**, per `references/foundations.md` section 5 (condensed; full version in the bundle). Lite mode does not report time-of-day windows. The one carve-out: one cell that clears the n>=5 floor (or the better of two, by median, if two cleared) may be reported below this section as one labeled "Early signal", never inside this table and never with a rank number on it. If two or more cells clear the floor in lite mode, report the better one as the early signal and say in one line that another cell also cleared. Do not rank them.}

| Rank | Window | Posts | Median engagement | Flags |
|---|---|---|---|---|
| 1 | {day}, {band} | {n} | {median} | {concentration flag(s), then the format-confound result; if both checks ran and neither fired: "Concentration checked, clean. Format checked, no confound."; never "none"} |
| ... | | | | |

{Any bucket excluded from ranking for carrying 2 or more concentration flags: named here as "one post did something worth studying" with the post identified, not turned into a recommendation.}

{Format-confound note, glued to the window it applies to, in the row above and restated in one sentence here if it changes the read: "{window}'s median leans partly on {type}, which is {x} times its normal share of your posts in that window and is itself your strongest format corpus-wide at {type_median} against your {corpus_median} overall. Test the window and the format separately before you commit to either." When the flagged post is not the bucket's top post, say where it actually sits, because the flag measures representation, not direction, and telling a user their window is inflated when the over-represented post is near the bottom of it is a false statement made out of a true flag.}

## Early signal (one window, not a ranking)

{LITE MODE ONLY, and only when one or more day x band cells clear the n>=5 floor. Report one cell (or the better of two, by median, if two cleared). Omit the whole section otherwise.}

**{day}, {band} band. {n} posts, median {median}.** {One line saying it is the only cell in the capture that reached the floor, and by how much.}

It is reported on its own, because a cell that cleared the floor is real evidence. It is not a rank, not a "best window", and not comparable to anything, because the other 27 cells never produced enough posts to compare it against.

{Its caveats, one clause each: concentration flags, and the format-confound result.} Treat it as one thing worth testing on purpose, not as an answer.

---

## Where you post versus where you win

{The schedule-gap paragraph, day-of-week level: most-posted rankable day, best-median rankable day, the percentage gap, and what moving volume would do. If they are the same day, say so plainly instead.}

{One sentence on the day x band layer: either the finer gap if that layer is usable, or a note that the layer is too thin to name a single dominant slot yet.}

---

## What this analysis is standing on

Analyzed {N} posts captured {first date} to {last date}, {span} days. Rankings use median engagement, which is reactions plus comments plus shares, unweighted. Buckets under 5 posts are listed but not ranked, in both the day-of-week and day-by-time layers. {Any concentration flags that fired, restated in one clause each.} {Any format-confound flags that fired, restated in one clause each.} {If timezone unconfirmed: "No timezone was confirmed this run, so every time-of-day finding above is relative, not a clock time."} A timezone offset can shift a late-night post into the next calendar day, which affects day-of-week counts by at most one slot.

{If lite mode or date-only: the specific missing thing and the specific capture depth that fixes it, restated once.}

Not in your export, so not in this analysis: sponsored or paid-partnership flags, so a boosted post's timing looks identical to an organic one here. Reach or impressions, so a strong window means people who saw it engaged more, not that more people saw it.

PostSnag captures what you scrolled, so this is a sample of your account, not its full history.

Rerunning this skill on the same file reproduces every number exactly; if it does not, the run was not computed with code.

Analysis based on {N} captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=best-time-to-post-reader
```

---

## Section-by-section notes for whoever fills this

**The timezone question.** This is the one gate in the whole catalog that blocks output rather than degrading it gracefully mid-run. Ask it before doing anything else with clock time. If the user answers later in the same conversation, do not re-ask, just use the answer from that point on and say so ("Using the timezone you gave me, {tz}.").

**The heat grid.** Every one of the 28 cells appears, even the empty ones. A grid that only shows populated cells hides exactly the information a user needs to judge how much they should trust the finer layer: how sparse it actually is.

**Your best days versus your best windows.** These are two different tables because they are two different confidence tiers. Never merge them into one ranked list. A user should be able to act on the day-of-week table alone and treat the window table as supplementary evidence, not the other way around.

**The schedule gap.** This is the section most likely to get screenshotted. Keep it to the one clean comparison (most-posted versus best-median) rather than trying to narrate every day's story.

**The confound note.** State it once, plainly, glued to the window. Do not turn it into a lecture about causation. One sentence naming the type, the ratio, and the type's own corpus median is enough for the user to decide whether to trust the window as-is or test the format separately.

**The footer.** Never softened, never moved, never dropped when the analysis was thin. A thin analysis, especially on this skill, is exactly when the footer is doing the most work, because it is the difference between a real finding and a coincidence dressed as one.
