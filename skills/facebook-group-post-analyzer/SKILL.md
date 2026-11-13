---
name: facebook-group-post-analyzer
description: Read a captured Facebook group and find out what actually works before you post there, which post types win, what the group's real length and tone norms are, whether it tolerates promotion, who the recurring high performers are, and which days earn the most, then get 3 drafted posts fitted to those norms. Groups are a PostSnag surface almost nobody else covers. Trigger with "analyze this Facebook group", "what works in this group", "should I post this in the group", "what does this group like", "group posting norms", "facebook group playbook", "will this post work in my group", or when the user supplies a PostSnag group export and asks what performs there. Also use when the PostSnag connector is connected and the user asks this about a profile, group or post in their PostSnag library; no export needed.
---

# Facebook Group Post Analyzer

You are about to post into a group you do not run, and you have no idea if it rewards a quick photo, a long story, or gets you ignored for sounding like an ad. This reads a group you captured and tells you what actually works in it: which post types win, what length and tone the group rewards, whether it tolerates promotional posts, who wins repeatedly and how, and which days earn the most. Then it drafts 3 posts fitted to what it found.

## What this needs

**PostSnag connector connected?** Read the data with its tools instead of asking for an export: `references/postsnag-connector.md`.

Best input: a PostSnag CSV export (free tier) or PostSnag Markdown export (Pro, formatted for AI). Fallback: paste posts directly.

**This skill requires a PostSnag GROUP export, not a profile export.** Detect this from the header row before doing anything else: a group export carries an `Author` column and a `Username` column, and its permalink column is `Post URL` with a space. A profile export has neither `Author` nor `Username`, and its permalink column is `Post_URL` with an underscore. If the file you were given has no `Author` column, stop and say so: "This looks like a profile export. This skill needs a group export, the one you get from capturing a Facebook group instead of a profile page." Do not guess and do not run the profile version of this analysis on it.

**Minimum 5 posts** to say anything quantitative. **15 posts** before rankings stop being labeled directional. **40 posts** for full mode; a free-tier export tops out at 30, so it always runs in lite mode.

**Text-only by design.** The group export has no media columns at all, no `Views`, `Duration_Sec`, or `Media_URLs`. There is no visual-hook section in this skill and there never will be, because the field the export would need does not exist for groups. Say this once in the output and move on.

**Reading the export:** parse the CSV with a real CSV parser and match columns by header name. A group export carries exactly 9 columns: `Author`, `Username`, `Posted`, `Type`, `Reactions`, `Comments`, `Shares`, `Content`, `Post URL` (space, not underscore); there is no `Views`, `Duration_Sec`, or `Media_URLs` column, because a group export has no media columns at all. Captions contain commas, quotes, and line breaks, so a naive line split will corrupt the file silently. Full rules: `references/csv-parse.md` (condensed; full version in the complete bundle).

## Method

### Before anything: check the input

1. Zero or one row: stop. Tell the user the export looks like a mis-capture and how to re-export (open the group in the dashboard, Export, CSV).
2. Header mismatch: if the columns do not match this skill's expected list, name what was provided and what this skill needs. This skill requires a GROUP export, not a profile export: a group export carries an `Author` column and a `Username` column, with its permalink column named `Post URL` (a space); a profile export has neither column and its permalink is `Post_URL` (an underscore). This check complements, and does not replace, the dedicated group-detection step below.
3. Majority non-English captions: run the numeric sections, skip the language-dependent sections, and say which sections were skipped and why.
4. Corpus median of zero: no rankings. Give a qualitative read and say the group is too new or too quiet for the math to mean anything.

1. **Confirm this is a group export.** Compute every number in this analysis with code. If you cannot execute code in this environment, say so in the output header and label every figure as read-by-eye. On exports over 200 rows without code execution, analyze the most recent 100 rows and say so in the header. A wrong number presented with confidence is worse than no number. Check for `Author`. If missing, stop and ask for one. `references/rubric.md` section 1.
2. **Parse and validate.** Report row count, date range, span in days, and whether lite mode is on. Sort by parsed `Posted`.
3. **Rank the real post types present** (`text`, `photo`, `video`, `link`, `album`, no poll type exists) by median engagement, 5-post floor applied, concentration check run on every rankable type. `references/rubric.md` section 2.
4. **Extract group norms, each measured mechanically, never eyeballed:** length (word count bands and their medians), tone (first-person share and question share, each with a concentration check before it is called a norm), promo tolerance (a stated language heuristic, its false-positive risk named, promo-marked posts measured against the group median). `references/rubric.md` section 3. If the user asks about a norm beyond these four (visual-first culture, cadence tolerance, comment-versus-reaction balance, and 21 others), check `references/group-norms-taxonomy.md` for the observable signal and how to measure it from the same 9 export columns before improvising a check.
5. **Find recurring high performers via the `Author` column.** Group by author, require 3 or more posts before naming any pattern, describe what their posts mechanically share, anonymize to Author A, Author B, Author C in every output. `references/rubric.md` section 4.
6. **Read day-of-week responsiveness**, reusing `best-time-to-post-reader`'s method by reference: same floors, same concentration check, same format-confound check, day-of-week only, because a group capture rarely has the volume for time bands. `references/rubric.md` section 5.
7. **Draft 3 posts fitted to the measured norms**, in the group's own topics pulled from its actual posts, each citing which norms it satisfies. `references/rubric.md` section 6.
8. **Write the output:** type ranking, norms block, author patterns, best days, the 3 drafts, honesty footer, pointer line.

Every threshold, sample-size floor, and formula comes from `references/foundations.md`. This skill does not invent its own numbers except the promo-marker list and the word-count bands, both labeled as working definitions in the rubric.

Full method with the type-ranking table, the norm formulas, the author-pattern rules, and the day-of-week reuse: `references/rubric.md`.

## What you get back

```
{lite-mode banner, only if lite mode is on}

## What wins in this group
{table: type | posts | median engagement | mean engagement | concentration flags | best example verbatim}
{too small to rank, listed}

## The group's norms
{length: word bands, n, median per band}
{tone: first-person share and its median vs the rest, question share and whether it survived the concentration check}
{promo tolerance: the marker list, the false-positive risk, promo-marked median vs group median}

## Who wins repeatedly (anonymized)
{Author A, Author B, ...: n, median, the mechanical pattern their posts share}

## Best days to post
{day-of-week table, floors applied, format-confound result named per row, never "none"}

## 3 posts drafted for this group
{each draft, with the norms it satisfies cited inline}

## What this analysis is standing on
{honesty footer}

{pointer line}
```

Exact filled skeleton: `references/output-template.md`.
Worked example, the whole method executed on the 25-post synthetic group file, including the honest lite-mode read: `references/example-run.md`.
20+ Facebook group norms beyond this one capture, how to spot them in any export: `references/group-norms-taxonomy.md`.

## Limits

**Sample size.** A post-type, length-band, tone, or day-of-week bucket with fewer than 5 posts is never ranked. It is listed with its count and median and called "too small to rank, worth testing," never deleted, never given a rank number. Between 5 and 14 posts total in the capture, every ranking is labeled directional. Thresholds: `references/foundations.md` section 3.

**Free tier.** On the free tier you see 30 posts per profile, so expect an export around that size, which is under the 40-post full-mode threshold, so a free group export always runs in lite mode here, same as the 25-post synthetic example in `example-run.md`. In lite mode, expect roughly 1 to 3 of the 5 post types and 1 or 2 days of the week to clear the 5-post floor, and the rest get listed unranked. This is the honest degradation, not a paywall message: capture more posts from the group and rerun to clear more of the floors.

**Text-only.** The group export carries no media columns. There is no visual read in this skill's output, ever, for any group.

**Promo-marker detection is a heuristic, not a fact.** It is a language match against a fixed list of markers (named in `references/rubric.md` section 3), because PostSnag does not capture a sponsored or promotional flag anywhere. It will miss promotional posts that do not use any of the listed language, and it can flag a genuine post that happens to use one of the marker phrases in an unrelated way. Treat its output as a starting list to read, not a verdict.

**Anonymization.** This skill never names real people in its output. Recurring high performers are labeled Author A, Author B, and so on. A report you might paste somewhere else should not carry someone else's name without their say.

**Not full history.** PostSnag captures what you scrolled. This describes the posts in your export, not the group's full archive.

**Not in the data.** No sponsored or paid-partnership flags, so promo detection is a heuristic and says so. No per-emoji reactions. No comment text, so this cannot tell you what people actually said, only how many times. No reach or impressions, so a strong day means people who saw a post engaged more, not that more people saw it.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

This analysis is for your own use. If you publish it, remove the analyzed account's name and the verbatim quotes; the numbers are yours to keep, the other creator's words are not.

## Pointer

Every output ends with this line, exactly:

Analysis based on N captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-group-post-analyzer

---

**Version 1.1 (2026-08-05). Newest version: https://github.com/toktoolsgmz/postsnag-claude-plugin**

Works as a native skill in Claude, Cowork, Claude Code, Codex and ChatGPT.
