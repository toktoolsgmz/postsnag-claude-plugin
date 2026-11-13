---
name: facebook-content-calendar-builder
description: Turn the outputs of your PostSnag profile audit, hook analysis, and best-time read into a finished 7-day posting plan with full drafts, where every slot cites the exact upstream line it came from and every upstream caveat travels onto the slot it affects. Also runs on its own from a raw export, lighter, and says out loud what that costs you. Trigger with "build my content calendar", "make me a posting schedule", "plan my week of Facebook posts", "what should I post this week", "turn my audit into a calendar", "chain these skills into a plan", "weekly content plan with drafts", or when the user supplies a PostSnag export or the output of facebook-profile-audit, facebook-hook-analyzer, or best-time-to-post-reader and asks what to post next week. Also use when the PostSnag connector is connected and the user asks this about a profile, group or post in their PostSnag library; no export needed.
---

# Facebook Content Calendar Builder

You ran the audit. You ran the hook analysis. You know your best day. And you still open a blank box on Monday and write whatever comes to mind, because nothing turned those three reports into four specific posts with dates on them.

This is the skill that does the turning. It reads the other three outputs, allocates a week from them, and hands back full drafts with the evidence line attached to every decision: which day, which format, which hook, which topic, and the exact upstream sentence each one came from. When an upstream finding carried a caveat, the caveat rides onto the slot. That is the whole job. A plan that quietly launders a flagged finding into a clean-looking instruction is worse than no plan.

**Drafts only. You post them.** This skill does not connect to Facebook, does not publish, does not schedule, and does not touch your account. It writes text and puts dates next to it. Every word goes out under your hand, after you read it.

**Downloaded just this skill? Solo mode, section 3, is yours; chain mode needs the other skills' outputs pasted in.** Said here, up front, honestly: solo mode is real and installable, and it is also strictly weaker than chain mode in five specific ways, all named in `references/rubric.md` section 3.5. If you have not run the other three skills, keep reading, this file works standalone.

## What this needs

**PostSnag connector connected?** Read the data with its tools instead of asking for an export: `references/postsnag-connector.md`.

Best input: a PostSnag CSV export (free tier) or PostSnag Markdown export (Pro, formatted for AI). Fallback: paste posts directly.

**Chain mode is the real mode.** Paste the finished outputs of all three: `facebook-profile-audit`, `facebook-hook-analyzer`, and `best-time-to-post-reader`, run on the same export. All three must report the same post count, the same date range, and the same span. If they disagree, this skill stops and says so, because a calendar built from two different captures is a calendar built from nothing.

**Solo mode runs on one raw export plus 3 to 5 topics from you.** It executes lighter inline versions of all three upstream reads. It cannot run the format-confound check, cannot run the latent-fit test that finds hook archetypes you already write and have never led with, and cannot produce a clock time on any slot. Section 3 of `references/rubric.md` names every line item it loses.

**Reading the export:** parse the CSV with a real CSV parser, match columns by header name, and treat empty Views and Duration_Sec as absent rather than zero. Captions contain commas, quotes, and line breaks, so a naive line split will corrupt the file silently. Full rules: `references/csv-parse.md` (condensed; full version in `_shared/csv-contract.md` and the complete-bundle download).

## Method

### Before anything: check the input

1. Zero or one row: stop. Tell the user the export looks like a mis-capture and how to re-export (open the profile in the dashboard, Export, CSV).
2. Header mismatch: this skill runs in one of two modes, and they are not interchangeable. Chain mode wants the three pasted upstream outputs, from `facebook-profile-audit`, `facebook-hook-analyzer`, and `best-time-to-post-reader`, run on the same export; if what was pasted does not carry those three headers, name what was provided and which of the three is missing or unrecognized. Solo mode wants one raw PostSnag CSV export plus 3 to 5 topics from the user; if the pasted columns do not match a profile export's expected list, name what was provided and what this skill needs. Say which mode this run is in before allocating anything.
3. Majority non-English captions: run the numeric sections, skip the language-dependent sections, and say which sections were skipped and why.
4. Corpus median of zero: no rankings. Give a qualitative read and say the profile is too new or too quiet for the math to mean anything.

1. **Read the three upstream outputs and cross-check them.** Compute every number in this analysis with code. If you cannot execute code in this environment, say so in the output header and label every figure as read-by-eye. On exports over 200 rows without code execution, analyze the most recent 100 rows and say so in the header. A wrong number presented with confidence is worse than no number. Post count, date range, and span must match across all three. Any mismatch stops the run. Record which upstream sections are present, which are absent, which ran in lite mode, and which carry flags. Section 1 of `references/rubric.md`.
2. **Map every consumed field to what it drives**, using `references/chain-input-map.md`. That file is the contract: 46 rows naming the upstream skill, the output section, the field, what it drives here, what happens when it is absent, and what happens when it carries a flag. Walk it before allocating anything.
3. **Set the slot count** from the audit's Cadence section, then cap it at the number of days the time read actually ranked. A slot with no defensible day is a guess with a date on it.
4. **Allocate formats** from the audit's format distribution, using each format's share of the top quartile against its share of the corpus. Tiers A, B, C, and D, with the tie-breaks written out.
5. **Allocate hooks** from the hook analyzer's ranked archetypes and its test list, with a rotation rule so one archetype cannot fill the week, and a screen that keeps any archetype carried by a single post out of a proven slot.
6. **Allocate topics** from the audit's topic clusters, skipping any topic the audit reported as tested and flat.
7. **Allocate times** from the time read's two tables, honoring its confidence tiers. A window the upstream excluded from ranking never becomes a slot time.
8. **Propagate the flags.** Every caveat on a consumed finding is written onto the slot it affects, including the caveat's direction. Then run the double-cite rule (a slot's format may not be the format that fired a confound on that slot's day) and the confound budget (no slot carries more than two untested axes).
9. **Write the drafts.** Voice from the creator's own winners, hook from the assigned template, length from the analyzer's structural read, duration from the audit's duration bands. Originality guardrail in section 4 of the rubric.
10. **Write the output:** the 7-day calendar with an evidence line per slot, the week-summary block, the honesty footer, the pointer line.

Every threshold, sample-size floor, and formula comes from `references/foundations.md` (condensed; full version in `_shared/engagement-math.md`, already in the bundle). This skill does not invent its own numbers, and it does not recompute the upstream ones. It consumes them.

Full method with the input contract, the allocation rules, solo mode, and the drafting method: `references/rubric.md`.

## What you get back

```
{DRAFTS-ONLY line, at the top}
{lite-mode banner, inherited from any upstream that ran in lite mode}

# Content calendar: {profile}, {Monday date} to {Sunday date}

## The week
{7 rows, one per day. Days with no slot say so and say why.}

## Slot 1 through N
{per slot: day and date, time or day-level slot with its confidence tier and any
inherited flag, format with its duration band on video, hook archetype and the
verbatim template used, topic, the full draft, then the evidence lines:
"because: {upstream citation}" for time, format, hook, and topic}

## Week summary
{slot arithmetic, format mix against the audit's, hook rotation, time tiers used,
the numbered list of flags this week inherited, the days left empty and why,
which slot to cut first if the week goes sideways, which upstream recommendations
this week consumed and which it did not}

## What this calendar is standing on
{honesty footer}

{pointer line}
```

Exact filled skeleton: `references/output-template.md`.
Worked example, chain mode executed on the real outputs of all three upstream skills, with a solo-mode appendix on the free-tier slice: `references/example-run.md`.
The full 46-row field-by-field chain contract: `references/chain-input-map.md`.

## Limits

**This skill measures nothing.** It consumes measurements. Every number on the calendar traces to a line in one of the three upstream outputs, and the calendar prints that line. If an upstream number is wrong, this calendar is wrong in exactly the same way, which is why it cites rather than restates.

**Sample size.** Inherited whole from upstream. A calendar cannot be more confident than the thinnest artifact feeding it. If the hook analyzer labeled its rankings directional, every hook slot here says directional. If the time read cleared the day floor on 3 of 7 days, this week has at most 3 slots. Thresholds: `references/foundations.md` section 3 (condensed; full version in `_shared/engagement-math.md` section 4, already in the bundle).

**Free tier.** On the free tier you see 30 posts per profile, so expect an export around that size, under the 40-post full-mode threshold, so all three upstream artifacts run in lite mode and this calendar inherits it. Concretely, on a free export: no slot carries a clock time, the week is capped at the number of days the time read could rank (typically 3 of 7), the audit's topic table usually clears 1 cluster of 10 so most topic axes are untested, and the trajectory line is absent. You get a real week. You get it with day-level slots and more untested axes than a deeper capture would leave you. Roughly 60 posts across at least 60 days is where clock times become available at all.

**Not full history.** PostSnag captures what you scrolled. This plans from the posts in your export, not from your account.

**Not in the data.** No sponsored or paid-partnership flags, so if any upstream finding is standing on a boosted post, this calendar has inherited that and cannot see it. No reach or impressions, so no slot here predicts how many people will see anything. No comment text. No follower history.

**Drafts only, humans post.** Restated because it is the most important operational fact in this file. No publishing, no scheduling, no account access. The dates are a plan, not an instruction to a machine.

**Rerunning this skill on the same file reproduces the medians, counts, and ratios exactly; cluster names and topic labels can vary between runs because they are language reads, not arithmetic.**

**This analysis is for your own use. If you publish it, remove the analyzed account's name and the verbatim quotes; the numbers are yours to keep, the other creator's words are not.**

## Pointer

Every output ends with this line, exactly:

Analysis based on N captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-content-calendar-builder

`N` is the post count the upstream artifacts were built on. If they disagree, the run has already stopped.

---

**Version 1.1 (2026-08-05). Newest version: https://github.com/toktoolsgmz/postsnag-claude-plugin**

Works as a native skill in Claude, Cowork, Claude Code, Codex and ChatGPT.
