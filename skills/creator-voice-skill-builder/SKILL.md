---
name: creator-voice-skill-builder
description: Turn a captured Facebook profile into a permanent, reusable creator-voice writing skill you install once and use on every future topic, instead of re-running a style analysis every time. Walks you through selecting your winning posts, screening for promotional posts by hand with a language heuristic, extracting your voice mechanics, and filling two templates into a finished skill you keep. Trigger with "build me a voice skill", "turn my export into a writing skill", "make a permanent version of my caption style", "I want to stop re-running this every time", "build my own writing skill from my posts", "make a skill file from my voice", or when the user supplies a PostSnag export and asks for a reusable skill artifact rather than a one-time caption. Also use when the PostSnag connector is connected and the user asks this about a profile, group or post in their PostSnag library; no export needed.
---

# Creator Voice Skill Builder

You have run a caption analysis before. You will want captions again next month, on a different topic, and the analysis starts over from zero, because nothing from last time was kept. This fixes that. It walks you through building your own permanent voice skill, once, from a captured export: a recipe, two fill-in templates, and a finished pair of files you install and reuse on every future topic without paying the analysis cost again.

**Distinct from `facebook-caption-writer`.** That skill writes captions right now, in this conversation, on the topic you give it, and nothing survives after the chat ends. This skill does not write a single caption. It teaches you to build the thing that writes captions, permanently, so you stop re-running the analysis every time you need one.

## What this needs

**PostSnag connector connected?** Read the data with its tools instead of asking for an export: `references/postsnag-connector.md`.

Best input: a PostSnag CSV export (free tier) or PostSnag Markdown export (Pro, formatted for AI). Fallback: paste posts directly.

**One export of the profile whose voice you want to keep: your own, or a client's you have permission to build for.** Minimum 15 posts for a measured voice profile. Between 5 and 14, this runs a qualitative read and the built skill says so in its own limits section. Below 5, there is not enough to extract a voice from, and this skill says that plainly rather than guessing one.

**Reading the export:** parse the CSV with a real CSV parser, match columns by header name, and treat empty Views and Duration_Sec as absent rather than zero. Captions contain commas, quotes, and line breaks, so a naive line split will corrupt the file silently. Full rules: `_shared/csv-contract.md` (not part of this skill's local embeds pack; full version in the bundle).

## Method

### Before anything: check the input

1. Zero or one row: stop. Tell the user the export looks like a mis-capture and how to re-export (open the profile in the dashboard, Export, CSV).
2. Header mismatch: if the columns do not match this skill's expected profile-export list, name what was provided and what this skill needs (this skill reads a PostSnag profile export, your own or a client's with permission; a group export needs a different skill).
3. Majority non-English captions: run the numeric sections, skip the language-dependent sections, and say which sections were skipped and why.
4. Corpus median of zero: no rankings. Give a qualitative read and say the profile is too new or too quiet for the math to mean anything.

1. **Parse and validate.** Compute every number in this analysis with code. If you cannot execute code in this environment, say so in the output header and label every figure as read-by-eye. On exports over 200 rows without code execution, analyze the most recent 100 rows and say so in the header. A wrong number presented with confidence is worse than no number. Report row count, date range, span in days, empty-caption count. Sort by parsed `Posted`.
2. **Select the style-source posts.** Top quartile by engagement, same definition and floors as `references/foundations.md` section 6 (condensed from `_shared/engagement-math.md` section 8; full version in the bundle). Run the three-part concentration check from `references/foundations.md` section 4 (condensed from the same file's section 5) on the style-source set as a whole, so one viral post cannot pass itself off as the creator's whole voice. Full rules: `references/rubric.md` section 1.
3. **Run the promo screen.** PostSnag does not capture sponsored or paid-partnership flags anywhere, so this skill cannot detect a boosted or paid post directly. It screens the style-source set with an honest language heuristic instead: a marker list for partnership language, discount-code language, and link-out language. Every flagged post goes on a manual review list with the reason it was flagged. **This skill never silently drops a post.** You see what was flagged and why, and you confirm what stays and what goes. Full rules and the false-positive risk, stated plainly: `references/rubric.md` section 2.
4. **Extract the voice markers.** The same 9 mechanics `facebook-caption-writer` measures: opening-line pattern, sentence rhythm, line-break style, emoji usage, CTA placement, hashtag behavior, capitalization habits, question frequency, first-versus-second person. This skill does not redefine them; it reuses the measurement rules condensed locally in `references/caption-mechanics-mini.md` (from `facebook-caption-writer/references/rubric.md` section 2; full version in the bundle). Condensed table: `references/rubric.md` section 3.
5. **Fill the two templates.** `references/voice-skill-template.md`, the permanent skill file itself, and `references/style-playbook-template.md`, its companion reference. Slot-by-slot instructions: `references/rubric.md` section 4.
6. **Run the 3-test acceptance check.** Write on a topic the creator covered, a topic they never covered, and a topic outside their niche entirely. What passing looks like for each, and why the third test is not supposed to pass the same way the first two do: `references/rubric.md` section 5.
7. **Set up the maintenance habit.** The one-line update loop from the source method: when the built skill gets something wrong, you tell it, once, and it does not happen again. `references/rubric.md` section 6.

Every threshold, sample-size floor, and formula comes from `references/foundations.md` (condensed; full version in `_shared/engagement-math.md`, already in the bundle). The 9 mechanics come from `references/caption-mechanics-mini.md` (condensed from `facebook-caption-writer/references/rubric.md`). This skill does not invent its own numbers for either.

Full method with the promo-marker list, the fill-in instructions, and the acceptance-test procedure: `references/rubric.md`.

## What you get back

```
{lite-mode or small-sample banner, only if under 40 posts or the qualitative path applies}

## Your style-source set
{k posts, cut value, concentration check result}

## The promo screen
{marker hits by category, the manual review list with reasons, your confirmed keep/exclude decision}

## Your voice, measured
{condensed 9-mechanics table, citing facebook-caption-writer}

## Your two finished files
{voice-skill-template.md, filled}
{style-playbook-template.md, filled}

## The 3-test acceptance run
{test 1: covered topic, drafted output, pass/fail}
{test 2: uncovered in-niche topic, drafted output, pass/fail}
{test 3: out-of-niche topic, drafted output, pass/fail, and why this one is graded differently}

## Keeping it current
{the maintenance habit, stated as an instruction, not a suggestion}

{honesty footer}

{pointer line}
```

Exact filled skeleton, with slot annotations: `references/output-template.md`.
Worked example, the whole recipe executed on a real 60-post file with a complete filled voice skill as the proof: `references/example-run.md`.
The two fill-in templates the recipe produces: `references/voice-skill-template.md` and `references/style-playbook-template.md`.

## Limits

**Sample size.** Below 15 posts, the voice profile is a qualitative read and the built skill's own limits section says so, mirroring `facebook-caption-writer`'s threshold. Below 5, there is not enough to build from. Thresholds: `references/foundations.md` section 3 (condensed; full version in `_shared/engagement-math.md` section 4, already in the bundle).

**Free tier.** On the free tier you see 30 posts per profile, so expect an export around that size, under the 40-post full-mode threshold, so a free export runs this recipe in lite mode: a smaller style-source set (roughly 7 to 8 posts instead of 15), fewer distinct archetypes to draw the acceptance-test drafts from, and a narrower range of model posts for the two templates. The skill you build is still real and still permanent. It is just built on less evidence, and the recipe says so at the point where it thins out.

**The promo screen is a heuristic, not a detector.** PostSnag does not capture sponsored or paid-partnership flags anywhere in any export. The marker list catches language patterns, not payment. It will flag posts that are not actually promotional (a link to the creator's own blog reads identically to a link to a paid partner's site under a marker that only checks post type), and it can miss a paid post that used no marker language at all. That is why every flag goes to manual review instead of automatic exclusion, and it is why this skill never claims to have found "the sponsored posts," only "the posts worth you looking at."

**Not full history.** PostSnag captures what you scrolled. The voice this skill builds describes the posts in your export, not your whole account.

**Not in the data.** No sponsored or paid-partnership flags, which is the whole reason the promo screen is a manual-review heuristic instead of a filter. No per-emoji reactions. No reach or impressions, so the voice profile is built on what people did, never how many saw it.

**This is the DIY bridge, not the product.** The one-click version of this (Build 3) reads your export and produces the finished skill automatically. This skill exists so the habit and the market are primed before that button exists, and it says so at the top of every copy of this file, not just once.

**Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.**

**This analysis is for your own use. If you publish it, remove the analyzed account's name and the verbatim quotes; the numbers are yours to keep, the other creator's words are not.**

## Pointer

Every output ends with this line, exactly:

Analysis based on N captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=creator-voice-skill-builder

---

**Version 1.1 (2026-08-05). Newest version: https://github.com/toktoolsgmz/postsnag-claude-plugin**

Works as a native skill in Claude, Cowork, Claude Code, Codex and ChatGPT.
