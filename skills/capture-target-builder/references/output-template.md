# output-template.md

The exact structure the user receives. Fill the braces. Do not reorder the sections, do not add sections, do not drop the footer or the pointer line. **No row in the scored candidate table or either plan ever carries a real name.** Every row is a placeholder the user fills in themselves.

For this template filled with real computed numbers, see `example-run.md`.

Version 1.0 | 2026-08-04

---

## Rules that apply to the whole output

- **Placeholders only, everywhere a candidate is named.** `Candidate 1`, `Candidate 2`, and so on. Never a guessed real name.
- **Every caveat is glued to its number, inside the sentence.** No trailing parentheticals.
- **No em dashes.** Comma, colon, period, parentheses.
- **Approved vocabulary only:** capture, extract, collect, export, analyze, save, pull.
- **The gap-analysis note appears only if an export was supplied.** If not, one line says so plainly and the scoring table shows 4 dimensions, not 5.

---

```markdown
Skill: capture-target-builder v1.1 | method run | own-export gap-fill: {used/not used} | computed with code: {yes/no/not applicable}

# Capture targets for {niche label}

Goal: {the classified goal archetype}, {one line on why that changes what gets emphasized below}.

{If the goal was defaulted: "You did not name a goal, so this run defaults to Grow reach and says so here."}

---

## Your niche map

| Category | Your niche's version |
|---|---|
| A. Direct peers | {one sentence, no names} |
| B. Aspirational leaders | {one sentence, no names} |
| C. Adjacent niches | {one sentence, no names} |
| D. Format innovators | {one sentence, no names} |
| E. Complementary-audience niches | {one sentence, no names} |
| F. Topic-support groups | {one sentence, no names} |
| G. Challenge or accountability groups | {one sentence, no names} |
| H. Local or regional groups | {one sentence, no names} |
| I. Marketplace or swap groups | {one sentence, no names} |

---

## Your search-term sheet

**{N} queries**, grouped by category. Run the Pages-tab queries under Facebook's Pages search and the Groups-tab queries under Groups search.

| Query | Category | Search tab |
|---|---|---|
| "{instantiated query}" | {A-I} | Pages / Groups |
| ... | | |

---

## Scored candidates

{One row per candidate that cleared the qualifying gate. Candidates that did not clear the gate are not listed by name; state the count that did not clear it in one line.}

| Candidate | Type | Category | Gate | Recency | Engagement | Caption | Format | {Gap-fill, only column if export supplied} | Total | Band |
|---|---|---|---|---|---|---|---|---|---|---|
| Candidate 1 | profile | {A-E} | {n}/4 | {0-3} | {0-3} | {0-3} | {0-3} | {0-3 or omit column} | {total} | Capture now / Watch / Skip |
| ... | | | | | | | | | | |

{Gap-analysis note, only if an export was supplied:}

> Your export shows {type} at {x} percent of your own posts, the lowest share of any format {and below the 10 percent gap threshold / labeled directional because your export has under 15 posts}. Candidates whose visible content leans on {type} score higher on gap-fill, which is why {candidate} moved from {band without the dimension} to {band with it}.

{If no export was supplied:}

> No export was supplied, so scoring ran on the 4 base dimensions. Supply your own PostSnag export and rerun this to add the gap-fill dimension.

---

## This week: your 3 profiles and 2 groups

{Table: rank, candidate, band, weighted score.}
{One line per any fallback or tie-break that fired, naming which rule and why.}

---

## Your four-week Pro plan

| Week | Profiles | Groups |
|---|---|---|
| 1 (repeats this week) | {3 candidates} | {2 candidates} |
| 2 | {3 candidates} | {2 candidates} |
| 3 | {3 candidates} | {2 candidates} |
| 4 | {3 candidates, or fewer with the shortfall stated} | {2 candidates, or fewer with the shortfall stated} |

{Shortfall note, only if the qualifying pool ran short:}

> The qualifying pool ran {n} profile slots and {n} group slots short of a full 4-week plan. {Category} produced {n} qualifying candidates in this run; generate more queries from that category's prompt in `rubric.md` section 1 and rerun the search-term sheet before filling the open slots.

**Pro's exact weekly scan allowance is unverified.** This plan paces at the same 3-profile-plus-2-group cadence as the free tier, as a conservative default. If your Pro plan allows faster capture, compress the 4 weeks.

---

## What this plan is standing on

{Honesty footer: how many candidates were found, how many cleared the gate, how many were scored, how many landed in each band, whether an export was supplied and what the gap analysis found or did not find, and the tie-breaks or fallbacks that fired.}

PostSnag captures what you scroll. This skill never captures anything itself; it tells you who is worth pointing your own scans at next.

Pairs with Bookmarks in the dashboard: once you have run the searches and scored your candidates, bookmark the capture-now tier there so next week's scans are one click instead of a re-search.

Rerunning this skill on the same file reproduces every number exactly; if it does not, the run was not computed with code.

Analysis based on {N} captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=capture-target-builder
```

---

## Section-by-section notes for whoever fills this

**The niche map.** 9 rows, always, even for a narrow goal. A row that reads like a name in disguise ("a big organizing page with a huge following") is still a description, not a name, and that is the line: describe the shape of the target, never claim to have found the target itself.

**The search-term sheet.** Every query is something the user actually types. If a query would not plausibly return results ("home organizing but better"), it does not belong here.

**The scored candidates table.** This is where the no-real-names rule is easiest to violate by accident, because a filled-in example run needs *some* label per row. `Candidate 1` through `Candidate N` is the only acceptable labeling in the live skill output. Invented, banner-flagged illustration names are permitted in `example-run.md` specifically because that file opens with a SYNTHETIC banner naming every invented profile and group up front; names pulled from a real user's export never appear anywhere, in any file, under any labeling.

**The weekly plan and the 4-week plan.** Reference candidates only by the same placeholder used in the scored table above, so the user can trace every pick back to its row and its score.

**The footer.** Never softened, never moved, never dropped when the plan came up short. A short plan is exactly when the honesty line matters most.
