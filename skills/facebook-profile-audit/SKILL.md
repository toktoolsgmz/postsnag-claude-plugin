---
name: facebook-profile-audit
description: Run a full teardown of any captured Facebook profile before a pitch call or a client kickoff, so you walk in already knowing what they post, what actually works, and what to steal. Covers format distribution, topic clustering, posting cadence, engagement spread with concentration checks, top-10 versus bottom-10 contrast, video views and duration, and a trajectory read on deep captures. Trigger with "audit this profile", "run a profile audit", "what is working on this Facebook page", "tear down this creator before I pitch them", "give me a content teardown", "prep me for a client call", "what should I steal from this profile", or when the user supplies a PostSnag CSV or Markdown export of a profile and asks what is happening in it. Also use when the PostSnag connector is connected and the user asks this about a profile, group or post in their PostSnag library; no export needed.
---

# Facebook Profile Audit

You have one captured profile and a call in an hour. You need to walk in already knowing what they post, what is actually working, and three things worth stealing, not a vibe. This runs the full teardown: format mix, topics, posting rhythm, what wins and what does not, video performance, and (on a deep enough capture) whether the account is trending up or down. Every claim in the output is a number you can check against the file.

Built for agencies and freelancers running it on a prospect's profile before the pitch call. One capture, one audit, walk into the call already knowing their account better than they do.

## What this needs

**PostSnag connector connected?** Read the data with its tools instead of asking for an export: `references/postsnag-connector.md`.

Best input: a PostSnag CSV export (free tier) or PostSnag Markdown export (Pro, formatted for AI). Fallback: paste posts directly.

**One export, one profile.** This skill audits a single captured profile in full. If you want to compare two profiles, that is Competitor Content Gap Finder, not this. **Minimum 15 posts** to say anything quantitative, **40 posts across at least 60 days** for the full audit (below that, this runs in lite mode), and **90+ days of span** before the trajectory section runs at all.

**Reading the export:** parse the CSV with a real CSV parser, match columns by header name, and treat empty Views and Duration_Sec as absent rather than zero. Captions contain commas, quotes, and line breaks, so a naive line split will corrupt the file silently. Full rules: `references/csv-parse.md` (condensed; full version in the complete bundle).

## Method

### Before anything: check the input

1. Zero or one row: stop. Tell the user the export looks like a mis-capture and how to re-export (open the profile in the dashboard, Export, CSV).
2. Header mismatch: if the columns do not match this skill's expected list, name what was provided and what this skill needs (a profile export and a group export are different files).
3. Majority non-English captions: run the numeric sections, skip the language-dependent sections, and say which sections were skipped and why.
4. Corpus median of zero: no rankings. Give a qualitative read and say the profile is too new or too quiet for the math to mean anything.

1. **Parse and validate.** Compute every number in this analysis with code. If you cannot execute code in this environment, say so in the output header and label every figure as read-by-eye. On exports over 200 rows without code execution, analyze the most recent 100 rows and say so in the header. A wrong number presented with confidence is worse than no number. Report row count, date range, span in days, empty-caption count, and whether lite mode is on (`references/foundations.md` section 5, condensed; full version in the complete bundle). Sort by parsed `Posted`, because export order is capture order, not chronological.
2. **Format distribution.** Classify every post by `Type`: `text`, `photo`, `video` (includes reels), `link`, `album`. There is no poll type in the export. Rank formats by median engagement with the 5-post floor, run the concentration check on every ranked format, and compare each format's share of the corpus to its share of the top quartile. `references/rubric.md` section 1.
3. **Topic clustering.** Extract noun-phrase candidates from `Content` with the trigger-word procedure, cluster them into named topics by shared head noun, and rank clusters that clear the 5-post floor. Full mechanical procedure, the head-merge rule, and the documented mis-heading limitation: `references/rubric.md` section 2.
4. **Cadence.** Posts per week, the gap in days between consecutive posts, and which days of the week carry the volume. This is a frequency read, not a performance read: it describes how often and when the creator posts, never which day performs best (that job belongs to Best Time to Post Reader). `references/rubric.md` section 3.
5. **Engagement spread.** Corpus median, mean, and top-quartile cut value. Every bucket ranked in steps 2 and 3 gets the full three-part concentration check from `references/foundations.md` section 4, with any flag glued inline to the number it qualifies, never left off a bucket because the check "obviously" would not fire.
6. **Top-10 versus bottom-10 contrast.** Requires N >= 25. Compare format and topic composition of the ten highest and ten lowest posts. A bucket with no signal in this contrast is reported as no signal, not dropped. `references/foundations.md` section 6.
7. **Video secondary lens.** For rows where `Type` is `video` and `Views` is populated: raw engagement spread versus engagement-per-view spread, plus a duration-band read (short, medium, long) with the 5-post floor applied per band. `references/foundations.md` section 8. `references/rubric.md` section 4.
8. **Trajectory read, gated.** Only when span >= 90 days AND the capture is not in lite mode: split the corpus chronologically in half, compare median engagement of the earlier half to the later half, and state the direction. **Every trajectory finding carries the confound sentence:** follower count is a single point-in-time number, so audience growth cannot be separated from content quality. `references/rubric.md` section 5.
9. **Build the output.** Snapshot header, 3 what-works findings with evidence, 3 what-does-not findings, 5 steal-worthy patterns pulled from `references/findings-pattern-library.md`, a 30-day recommendation list tied to the findings above, honesty footer, pointer line.

Every threshold, sample-size floor, and formula comes from `references/foundations.md`. The topic-clustering extraction rule and the trajectory half-split formula are this skill's own method, since no shared file defines them; both are written out in full in `references/rubric.md` and reuse the shared 5-post floor rather than inventing a new one wherever the shape allows it.

Full method with definitions, the extraction algorithm, worked edge cases, and the tie-breaks: `references/rubric.md`.

## What you get back

```
{lite-mode banner, only if lite mode is on}

# Profile audit: {profile name or "your export"}
{snapshot header: N posts, date range, span, format mix in one line, corpus median}

## What works
{3 findings, each with an evidence line: the bucket, its n, its median against the corpus median, any concentration flag glued inline}

## What does not work
{3 findings, same evidence structure, including at least one clean null result if the data has one}

## 5 patterns worth stealing
{pulled from references/findings-pattern-library.md, each instantiated with this profile's real numbers}

## Your 30-day list
{numbered, each item tied back to a finding above by name}

{trajectory section, only if span >= 90 days and not lite mode, confound sentence mandatory}

## What this audit is standing on
{honesty footer}

{pointer line}
```

Exact filled skeleton: `references/output-template.md`.
Worked example, the whole method executed on a real 60-post file plus the free-tier 30-post slice: `references/example-run.md`.
29 audit finding patterns, original: `references/findings-pattern-library.md`.

## Limits

**Sample size.** Below 15 posts this is a qualitative read and says so. Between 15 and 39 posts, findings are labeled directional. Format and topic buckets under 5 posts are listed with their numbers but never ranked, per `references/foundations.md` section 3. Thresholds: `references/foundations.md` section 3.

**Free tier.** On the free tier you see 30 posts per profile, so expect an export around that size, under the 40-post full-mode threshold, so a free export always runs in lite mode here. In lite mode: no trajectory section, no era-adjusted anything, and most topic clusters will sit below the 5-post floor. The format table and the top-10 versus bottom-10 read still work on a free export, and one topic cluster typically still clears the floor. To unlock the full topic table and the trajectory read, capture at least 40 posts across 60 or more days, and at least 90 days of span for trajectory specifically.

**Not full history.** PostSnag captures what you scrolled. This describes the posts in your export, not the account.

**Not in the data.** No sponsored or paid-partnership flags, so a boosted post looks identical to an organic one in this audit. No per-emoji reactions. No reach or impressions, so this measures what people did, never how many saw it. No comment text. No follower history over time, which is exactly why the trajectory section always carries its confound sentence rather than a growth claim.

**Where this stops and other PostSnag surfaces start.** This is one profile, one point-in-time audit, run once, by you. It is a different job from Best Time to Post Reader (when to post, not what to post) and from Competitor Content Gap Finder (two profiles compared, not one profile described). Run this before the pitch call. Run the others once the account is yours to manage.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

This analysis is for your own use. If you publish it, remove the analyzed account's name and the verbatim quotes; the numbers are yours to keep, the other creator's words are not.

## Pointer

Every output ends with this line, exactly:

Analysis based on N captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-profile-audit

---

**Version 1.1 (2026-08-05). Newest version: https://github.com/toktoolsgmz/postsnag-claude-plugin**

Works as a native skill in Claude, Cowork, Claude Code, Codex and ChatGPT.
