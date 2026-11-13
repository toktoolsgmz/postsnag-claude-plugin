# rubric.md

The full method for Capture Target Builder. Written so an agent with no other context can execute it and reach the same categories, queries, and scores as anyone else running it on the same niche and the same candidate's visible profile.

**The one rule that overrides every step below: never write a real profile, group, or creator name into the output.** Every candidate in this skill's deliverable is a placeholder (`Candidate 1`, `Candidate 2`, ...) that the user fills in from their own Facebook search. This skill does not browse Facebook and cannot verify a name it might produce, so producing one would be a guess wearing the costume of a fact. That is the one failure mode this whole rubric is built to prevent.

Version 1.0 | 2026-08-04

---

## Section 0: The niche and the goal

**The niche.** Take the user's stated niche and compress it to a short label: 2 to 5 words, specific enough to type into a search box. "Residential home organizing" is a label. "Helping people get their life together" is not, because it will not return relevant Facebook results. If the stated niche is too broad to search on, ask one clarifying question before proceeding rather than guessing a narrower version.

**The goal.** Every user capturing targets is optimizing for something, and the something changes which niche-map categories (Section 1) matter most. Classify the stated goal into exactly one of these 5 archetypes. If the user's words do not map cleanly, ask once; if they decline to choose, default to **Grow reach** and say so in the output.

| Goal archetype | What the user is actually trying to do | Categories to emphasize |
|---|---|---|
| **Grow reach** | Get bigger: more followers, more views, more shares. | B (aspirational leaders), D (format innovators) |
| **Generate leads or sales** | Convert an audience into paying clients or customers. | A (direct peers), H (local and regional groups) |
| **Build authority** | Be seen as the person who knows this topic. | B (aspirational leaders), F (topic-support groups) |
| **Find content ideas** | Break out of repeating the same 5 topics. | C (adjacent niches), E (complementary-audience niches) |
| **Build a community** | Grow an owned space around the user's own brand, not just a following. | F, G, H (all 3 group categories), plus A |

**Emphasis means priority order for search-query generation and, when scores tie, which category wins the tie**, not an exclusion of the other categories. A user optimizing for leads still benefits from seeing an aspirational leader's format choices. The niche map in Section 1 always produces all 9 categories; the goal only decides which ones get searched first and get more queries.

---

## Section 1: The niche map

9 categories. 5 describe profiles, 4 describe groups. Each has a **prompt**, which the user (or the agent, on the user's behalf) answers in one sentence to produce a **descriptive slot**: a sentence describing the kind of account to look for, never a name, because no name exists yet at this step.

### Profile categories

**A. Direct peers.** Creators covering the same core topic to an audience at a similar size or stage as the user's own.
*Prompt:* "Who else is teaching or showing [niche] to an audience that looks like my own, at a similar size?"

**B. Aspirational leaders.** Same core topic, clearly larger or more established. The account a beginner in this niche would name first if asked who to follow.
*Prompt:* "Who is the account in [niche] that people new to this topic get pointed toward?"

**C. Adjacent niches.** A different core topic, but the same audience segment. The reader who follows the user for [niche] plausibly also has this other problem.
*Prompt:* "What other problem does my audience have, that is not my core topic, but shares my audience's demographic and daily life?"

**D. Format innovators.** Same or adjacent topic, but known primarily for one distinct content format rather than for a topic angle: short-form video, before-and-after reveals, carousel checklists.
*Prompt:* "Who does my topic in a format I barely use?"

**E. Complementary-audience niches.** A different niche whose audience would plausibly also want the user's content, used mainly for content-idea cross-pollination rather than direct competitive tracking.
*Prompt:* "Whose audience already trusts someone else for a related problem, and would want my angle on it too?"

### Group categories

**F. Topic-support groups.** Advice-and-help exchange framed around the niche's core problem.
*Prompt:* "Where do people go to ask for help with [niche] specifically, rather than to follow a single creator?"

**G. Challenge or accountability groups.** A time-boxed group activity structured around the niche: a 30-day format, a weekly check-in, a before-and-after cycle.
*Prompt:* "What structured, repeating activity would my audience do together around [niche]?"

**H. Local or regional groups.** The niche crossed with geography.
*Prompt:* "Where does my niche show up filtered by city, region, or neighborhood?"

**I. Marketplace or swap groups.** Buy-sell-trade activity adjacent to the niche.
*Prompt:* "What do people in my niche buy, sell, or trade with each other?"

**Output of this step:** a 9-row table, one descriptive sentence per category, no names, ordered with the goal's emphasized categories first (Section 0).

---

## Section 2: The search-term sheet

20 slotted query patterns: 12 for profiles, 8 for groups. Fill the braced slots with the niche label and, where marked, the goal-relevant niche-map category. Produce **at least 15 instantiated queries**, weighted toward the goal's emphasized categories, but touching every category at least once so the map's whole point, coverage, is not lost to the goal's priority.

### Profile query patterns (Pages search)

1. `{niche} tips`
2. `{niche} hacks`
3. `{niche} for beginners`
4. `{niche} coach`
5. `{niche} before and after`
6. `{niche} on a budget`
7. `{audience descriptor} {niche}`, a life-stage or living-situation word placed before the niche term
8. `{adjacent niche} {niche}`, pulls category C candidates
9. `{niche} mistakes`
10. `{niche} system` or `{niche} method`
11. `{niche} reels` or `{niche} transformation`, format-suggestive wording, pulls category D candidates
12. `{niche} for {audience segment}`

### Group query patterns (Groups search)

13. `{niche} community`
14. `{niche} support group`
15. `{niche} tips and tricks`
16. `{city or region} {niche}`, pulls category H candidates
17. `{niche} challenge`
18. `{niche} accountability`
19. `{niche} swap` or `buy sell trade {niche}`, pulls category I candidates
20. `{niche} for {audience segment}`

**Instantiate at least 15**, group them by the category they target, and mark each `Pages search` or `Groups search` so the user knows which tab to use. A search-term sheet with fewer than 15 queries under-covers the map; a sheet that only fills the goal's 2 emphasized categories over-optimizes for one part of the niche and leaves 7 categories unsearched.

---

## Section 3: The qualifying checklist (the fast gate)

Run this before scoring anyone. It is deliberately cheap: 4 yes/no questions, answerable by looking at a profile or group's visible recent activity for under a minute. Its job is to filter out dead or empty accounts before spending time on the numeric sheet, not to rank anyone.

1. **Posting recency.** Has this profile or group posted within the last 14 days?
2. **Visible engagement.** Do the most recent 3 visible posts each show a reaction or comment count greater than zero?
3. **Caption depth.** Do at least half of the visible recent posts carry a caption longer than one short line, rather than an image with no real writing?
4. **Format mix.** Does the profile or group use more than one post format among what is visible, rather than 100 percent a single type?

**The gate: 2 or more yes advances the candidate to numeric scoring (Section 4). Fewer than 2 stops here.** Do not record the name of a candidate that fails the gate; note only that a search result did not qualify, so the working notes stay short and the output never carries a name that never earned a score.

**A candidate that clears the gate at exactly 2 yes is a real pass, not a weak one, and it still gets fully scored.** The gate exists to save time on obvious dead accounts, not to pre-judge quality; quality is what Section 4 measures.

**Private groups.** Many Facebook groups show almost nothing to a non-member: no visible post feed, sometimes not even a member count. The 4 gate questions above assume visible recent posts, which a private group frequently does not offer before you join. When that is the case, do not guess at answers you cannot see and do not silently skip the candidate. Score what IS observable pre-join instead: the About page description, the member count, and the group's activity line ("X posts a day," "active a few hours ago"), and mark the remaining gate questions **not observable pre-join** rather than answering them as no. A group that is otherwise promising on the visible signals is worth joining first, then re-running the gate from the inside with real visibility, rather than being scored down or dropped for a limitation of the outside view.

---

## Section 4: The numeric scoring sheet

Every candidate that clears the gate gets scored on 4 dimensions (5 if the user supplied their own export, Section 5). Each dimension is scored 0 to 3 against fixed observable anchors, full versions in `scoring-worksheet.md`. Multiply each score by its weight and sum.

| Dimension | Weight | What it measures |
|---|---|---|
| Posting recency | 3 | How current the account's activity is |
| Visible engagement | 3 | Whether an audience is visibly responding |
| Caption depth | 2 | Whether there is real writing to learn from, not just images |
| Format mix | 1 | Whether the account gives PostSnag's format-dependent skills (video Views, structural hooks) something to work with |
| Gap-fill relevance | 3 (only if export supplied) | Whether this candidate covers the format the user's own export is weakest in |

**Weights are working numbers**, stated as such here and in `scoring-worksheet.md`, not derived from the catalog's shared engagement thresholds. Recency and engagement carry the heaviest weight because a candidate who is not currently active or not currently earning any visible response has nothing to capture regardless of anything else about them. Caption depth outweighs format mix because most of this catalog's other skills (hook analysis, caption writing) need caption text to work with, while format mix is a secondary, nice-to-have signal.

**Score bands, without an export supplied (max 27):**

| Band | Score |
|---|---|
| Capture now | 18 or higher |
| Watch | 9 to 17 |
| Skip | 8 or lower |

**Score bands, with an export supplied and the gap-fill dimension applied (max 36):**

| Band | Score |
|---|---|
| Capture now | 24 or higher |
| Watch | 12 to 23 |
| Skip | 11 or lower |

Both band sets sit at the same proportions of their max (roughly two-thirds for capture-now, roughly one-third for the watch floor), so a candidate's tier means the same thing whether or not the gap dimension ran.

---

## Section 5: The gap-fill dimension (only when the user supplies their own export)

This is the only section of this rubric that touches a data file, so it is the only place the compute-integrity rule applies: compute every number in this analysis with code.

**Step 1: parse.** Read the user's own CSV with a real CSV parser, matching columns by header name, never by position. Address the `Type` column by name.

**Step 2: compute format share.** `share(type) = count(type) / total posts`, for each of the 5 possible types (text, photo, video, link, album).

**Step 3: find the gap.** Any type with `share < 10 percent` is a format gap. **10 percent is a working number**, stated as one, not derived from the catalog's shared engagement thresholds. If more than one type qualifies as a gap (share under 10 percent), the gap is the single lowest-share type; ties broken alphabetically by type name, and the output says a tie was broken that way.

**Step 4: check the evidence floor.** If the user's export has fewer than 15 posts, a corpus this small is too thin to call a finding measured rather than directional, the same corpus-minimum framing this catalog applies everywhere: format shares are labeled **directional**, and the gap-fill dimension still runs, but the output says the gap is based on thin evidence.

**Step 5: if no type clears the gap threshold**, say so plainly: "No format in your export sits under 10 percent, so there is no clear format gap. Scoring runs on the 4 base dimensions." Do not force a 5th dimension onto an even distribution.

**Step 6: score gap-fill relevance (0 to 3) for every candidate**, using the anchors in `scoring-worksheet.md`, based on how much of the candidate's visible content is in the gap format. A candidate dominated by the user's gap format scores highest here even if it scores modestly elsewhere, because filling a real hole in the user's own capture history is worth more than a marginally better all-around candidate who teaches the user nothing new.

---

## Section 6: Allocation

**Rank.** Split gated-in, scored candidates into two lists, profiles and groups. Sort each descending by weighted total.

**Tie-breaks**, in order, stated in the output when one fires:
1. Higher qualifying-checklist yes-count wins.
2. A candidate from a niche-map category not yet represented among that week's other picks wins over one from an already-represented category.
3. First-observed order: whichever candidate was found and scored first, in the order the searches turned them up, wins. Placeholder labels are assigned in this same order, so this is not alphabetical by label; the label follows the order, the order does not follow the label.

**Tie-break 2 is a week-allocation rule, not a ranking-time rule.** It depends on which categories are already represented among a given week's picks, a fact that only exists once allocation starts. At the plain descending-sort ranking step, only tie-breaks 1 and 3 apply; tie-break 2 fires later, during the diversity-rule swap described below.

**Diversity rule.** No more than 2 of the week's 3 profile picks come from the same niche-map category. Apply this after ranking, using tie-break 2 above if a swap is needed. This keeps a strong-but-narrow niche map from producing 3 near-identical picks in one week.

**The one-week free plan.** Take the top 3 profiles and top 2 groups from the capture-now tier. If capture-now does not have enough candidates of a type, fill the remainder from watch, ranked highest first, and name exactly how many slots were backfilled this way. Skip-tier candidates are never allocated, no exception, even if a week would otherwise go unfilled.

**The four-week Pro plan.** Continue down the same two ranked lists, 3 profiles and 2 groups per week, for weeks 2 through 4 (week 1 repeats the free-tier picks exactly, so upgrading does not waste the first week's work). If the qualifying pool (capture-now plus watch) runs out before all 4 weeks are filled, stop and say so: name the exact shortfall (how many profile or group slots are open) and name which niche-map categories produced zero or few qualifying candidates in this run, as the concrete next step, rather than padding the plan with skip-tier picks to make it look complete.

**Pro's exact weekly scan allowance is unverified.** Pace the four-week plan at the same 3-profile-plus-2-group weekly cadence as the free tier, state that this is a conservative default, and say the plan compresses if the user's actual Pro allowance is higher.

---

## Section 7: What this rubric refuses to do

- **No real name, ever, under any circumstance**, including a name the user themselves mentioned earlier in the conversation. If the user names a real account, acknowledge it in conversation but do not fold it into this skill's output tables as if it had been found by the method; the output stays placeholder-only so the artifact is safe to reuse or share on its own.
- **No score for a candidate that has not cleared the qualifying gate.** Scoring an unqualified candidate would produce a number that looks like evidence and is not.
- **No claim about a candidate's actual engagement rate, growth, or history.** Everything scored here is a momentary, outside view. It is a targeting signal, not an analysis, and the two are not the same job.
- **No assumption about Pro's weekly scan allowance beyond what is verified.** Free tier's 3 plus 2 a week is confirmed; Pro's specific number is not, and this rubric never states one it has not verified.
