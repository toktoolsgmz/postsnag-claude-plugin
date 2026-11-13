---
name: facebook-caption-writer
description: Write new Facebook captions in the proven caption style of a profile you captured, on any topic you give it. Measures opening-line pattern, sentence rhythm, line breaks, emoji use, CTA placement, hashtag behavior, capitalization, question frequency, and first-versus-second person from the winning posts, builds a visible style profile, then drafts 3 options per topic, each labeled with the specific post it is modeled on. Trigger with "write a caption like mine", "write this in my style", "match my Facebook voice", "caption writer", "write me 3 captions about", "copy my posting style for this topic", or when the user supplies a PostSnag export and a topic and asks for a caption. Also use when the PostSnag connector is connected and the user asks this about a profile, group or post in their PostSnag library; no export needed.
---

# Facebook Caption Writer

You know your winning posts work. You do not know exactly what they are doing, so every new caption is a guess dressed up as a plan. This measures the caption mechanics of your best-performing posts, shows you the measurements, and then writes new captions on your topic that match them, each one labeled with the exact post it borrowed its pattern from.

## What this needs

**PostSnag connector connected?** Read the data with its tools instead of asking for an export: `references/postsnag-connector.md`.

Best input: a PostSnag CSV export (free tier) or PostSnag Markdown export (Pro, formatted for AI). Fallback: paste posts directly.

**Two things this skill needs beyond the default: an export of the profile whose style to learn, and the topic (or topics) to write about.** Give both up front; a style profile with no topic has nothing to write, and a topic with no export gets a generic caption instead of a measured one. **Pasted-posts fallback: minimum 5 posts**, each with its own engagement numbers, per `references/foundations.md` section 3 (condensed; full version in the bundle). Below 5, this runs a qualitative style read and says so, not a measured one.

**Multiple topics in one run:** always 3 caption options per topic. **Maximum 3 topics per run.** If a user supplies more than 3 topics, write the first 3 and say plainly that the rest need a follow-up run, rather than thinning every option to fit more topics in.

**Reading the export:** parse the CSV with a real CSV parser, match columns by header name, and treat empty Views and Duration_Sec as absent rather than zero. Captions contain commas, quotes, and line breaks, so a naive line split will corrupt the file silently. Full rules: see `references/csv-parse.md` (condensed; full version in the bundle).

## Method

### Before anything: check the input

1. Zero or one row: stop. Tell the user the export looks like a mis-capture and how to re-export (open the profile in the dashboard, Export, CSV).
2. Header mismatch: if the columns do not match this skill's expected list, name what was provided and what this skill needs (a profile export and a group export are different files).
3. Majority non-English captions: run the numeric sections, skip the language-dependent sections, and say which sections were skipped and why.
4. Corpus median of zero: no rankings. Give a qualitative read and say the profile is too new or too quiet for the math to mean anything.

1. Compute every number in this analysis with code. If you cannot execute code in this environment, say so in the output header and label every figure as read-by-eye. On exports over 200 rows without code execution, analyze the most recent 100 rows and say so in the header. A wrong number presented with confidence is worse than no number. **Parse and validate.** Report row count, date range, span in days, empty-caption count, and whether lite mode is on. Sort by parsed `Posted`.
2. **Select the style-source posts.** Take the top quartile by engagement, same definition and floors as `references/foundations.md` section 6 (condensed; full version in the bundle). Report `k` and the cut value. Run the concentration check (section 4 of the same file) on the style-source set as a whole, because a style profile built mostly off one viral post is not a profile of the creator, it is a profile of one post. Full rules: `references/rubric.md` section 1.
3. **Extract 9 caption mechanics mechanically** from the style-source posts: opening-line pattern, sentence-length rhythm, line-break and whitespace style, emoji usage, CTA placement and phrasing, hashtag behavior, capitalization habits, question frequency, first-versus-second person. Every mechanic gets a measurement, a number, and a plain-language read. Definitions and how to measure each one: `references/rubric.md` section 2.
4. **Build the visible style profile.** The user sees the measurements, not just the output. This is the deliverable's first half.
5. **Scan the style-source set against `references/caption-mechanics-catalog.md`'s 24 wider mechanics** and name any that fire strongly enough to be worth an extra line in the style profile. This is a wider, shallower pass than the 9 measured mechanics: not every export shows one of these clearly, and the output says so when none fire rather than forcing a finding.
6. **Generate 3 caption options per topic**, each modeled on one specific style-source post: same archetype, same rhythm band, same structure. Never a generic caption dressed up as a match. Construction method: `references/rubric.md` section 3.
7. **Run the self-check pass** on every draft before it ships: does it match the measured mechanics, item by item. The checklist and what to do when a draft fails it: `references/rubric.md` section 4.
8. **Write the output:** style profile, 3 labeled options per topic, honesty footer, pointer line.

Every shared threshold, sample-size floor, and formula comes from `references/foundations.md` (condensed; full version in the bundle). Where this skill uses a number of its own, the 3.0-word tight-or-loose rhythm flag in `references/rubric.md` section 2.2, it is labeled a working number in the rubric and it is not presented as a platform fact.

Full method with the mechanic-by-mechanic measurement rules, the generation procedure, and the self-check checklist: `references/rubric.md`.

## What you get back

```
{lite-mode banner, only if lite mode is on}

## Your caption style, measured
{style profile: opening-line archetypes with counts, sentence rhythm with median and band, line-break structure, emoji count, CTA count, hashtag count, capitalization habits, question frequency, person voice, each with its number}
{any wider caption-mechanics-catalog.md findings strong enough to name, cited by mechanic name; omit this line entirely if none fired strongly}

## 3 captions for: {your topic}
{option 1: modeled-on label, the caption, a one-line note on which mechanics it is matching}
{option 2: modeled-on label, the caption, a one-line note on which mechanics it is matching}
{option 3: modeled-on label, the caption, a one-line note on which mechanics it is matching}

{Repeat this whole section, 3 options, once per topic, up to 3 topics maximum per run.}

## What this is standing on
{honesty footer}

{pointer line}
```

Exact filled skeleton: `references/output-template.md`.
Worked example, the whole method executed on a real 60-post file with real computed numbers: `references/example-run.md`.
24 Facebook caption mechanics beyond the 9 this skill measures, with how to detect and when to copy each: `references/caption-mechanics-catalog.md`.

## Limits

**Sample size.** Below 5 posts this is one reader's opinion, said plainly. Between 5 and 14 posts, every measurement in the style profile is labeled directional, and the generated captions say they are built on a small sample. At 15 posts and above, the style profile is a measured read, not a guess. Thresholds: `references/foundations.md` section 3.

**Free tier.** On the free tier you see 30 posts per profile, so expect an export around that size, which is under the 40-post full-mode threshold, so a free export runs in lite mode here. In lite mode the style-source set is smaller (roughly 7 to 8 posts instead of 15), which is usually still enough for a style profile because caption mechanics repeat faster than hook archetypes do. What thins out is the range of model posts to draw the 3 options from. The free export is also the most recent 30 posts, not a random 30, so the style profile describes recent captions, not the account's whole history.

**Not full history.** PostSnag captures what you scrolled. This describes the posts in your export, not your account.

**Not in the data.** No sponsored or paid-partnership flags, so a boosted post's caption looks identical to an organic one here. No per-emoji reactions, so this cannot tell you which emoji, if any, earns reactions. No reach or impressions, so the style profile is built on what people did, never how many saw it.

**Distinct from the Creator Voice Skill Builder.** This skill writes captions right now, in this conversation, on the topic you give it, and nothing persists after the chat ends. `creator-voice-skill-builder` teaches you to turn the same style profile into a permanent, reusable skill file you install once and use on every future topic without re-running the analysis. Use this one for today's caption. Use that one when you are ready to stop re-running the analysis.

Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.

This analysis is for your own use. If you publish it, remove the analyzed account's name and the verbatim quotes; the numbers are yours to keep, the other creator's words are not.

## Pointer

Every output ends with this line, exactly:

Analysis based on N captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-caption-writer

---

**Version 1.1 (2026-08-05). Newest version: https://github.com/toktoolsgmz/postsnag-claude-plugin**

Works as a native skill in Claude, Cowork, Claude Code, Codex and ChatGPT.
