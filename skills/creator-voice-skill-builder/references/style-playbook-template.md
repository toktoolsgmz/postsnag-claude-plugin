# style-playbook-template.md

The companion fill-in file to `voice-skill-template.md`. Where the voice skill is what a future agent reads to write a caption, this playbook is what a human reads to understand why the voice skill writes that way. The voice skill points here for anyone who wants the reasoning, not just the rules.

Version 1.0 | 2026-08-04

---

## How to fill this

Four sections, each pulling from a different part of `rubric.md` section 3's measurements. Write every section as instructions a future draft should follow, not as a restatement of the numbers. The numbers already live in `voice-skill-template.md`. This file is where they become rules.

---

```markdown
# {Creator name}'s style playbook

Companion to `{creator-name}-voice-writer`. Read this once to understand the voice profile. The voice skill itself is what actually gets used on every future topic.

## Hook patterns

{This creator's used archetypes, named for reference. Their full definitions were used during the build (`facebook-hook-analyzer/references/rubric.md` sections 2 and 2.13, condensed in `references/hook-archetypes.md`); this playbook does not need to re-derive them, and it must not cite that file or any other sibling skill by path, because a user who installed only this skill will not have it. Name the archetypes and say when to reach for each one.}

**Default opening move:** {archetype}, {count} of {k} style-source posts.

{For each archetype used 2 or more times: name it, its count, and one instruction for when to reach for it. "{Archetype}: {count} posts. Use when {the kind of topic or moment that calls for it}."}

**Used once, worth testing again:** {archetype list with counts of 1, if any, and one line on why each is still worth a second attempt rather than being dropped from consideration.}

**Never used:** {archetypes with zero instances. State plainly that a future draft should not reach for these without new evidence, per the out-of-niche guardrail in `voice-skill-template.md`.}

## Rhythm and structure

**Sentence rhythm:** {tight or loose call, standard deviation, median words per sentence, the band it falls in}. Write every draft to land in this band. {One instruction: what a draft outside this band should do about it, i.e. cut sentences or combine them.}

**Caption length:** {observed word-count range}. Do not draft meaningfully shorter or longer than this range without a structural reason (a numbered list needs more room; a one-line reaction needs less), and name the reason when you do.

**Line structure:** {dominant line count and pattern}. {Named exceptions and what specifically earns the exception, so a future draft does not default to the exception just because it is more interesting to write.}

**Hook length:** {observed hook word-count range}. A hook outside this range is a signal to tighten or expand it before shipping, not a hard rule, but check it every time.

## Vocabulary and mechanics

**Emoji:** {the rule, stated as a rule: "none, ever" or "{typical emoji}, used {where}."}

**Hashtags:** {the rule, same treatment.}

**Capitalization:** {sentence case or whatever was found}, {ALL-CAPS rule}, {numerals-versus-spelled-out rule for hook leads and, separately, for list markers, if the creator's habit differs between the two}.

**CTA behavior:** {platform CTA rule} and {closing-imperative rule}, stated separately, because a creator can have zero of one and several of the other and that is a real, distinct habit, not noise.

**Person voice:** {the dominant person, the share, and how first person specifically gets used when it appears: as a story the creator was present for, as a confession about their own standing state, or some other pattern found in the measurements.}

## Never do

{The inverse of every measured habit. This is the section that keeps future drafts from drifting toward generic AI-caption defaults the creator's own posts never show. List every applicable line, do not thin this list to save space:}

- {If emoji is 0: "Never add an emoji, even where it would look natural. This creator's winning posts have none."}
- {If hashtags is 0: "Never add a hashtag block. This creator's winning posts have none."}
- {If platform CTAs are 0: "Never add a comment-bait or follow-request line. This creator earns engagement without asking for it mechanically."}
- {If a specific archetype never appears: "Never lead with {archetype} without new evidence it works for this creator; it does not appear anywhere in the measured posts."}
- {If third-person-about-someone-else never appears: "Never write a fully third-person caption with the creator absent from it. Even their story posts keep them present as narrator."}
- {Any other zero-count or never-observed finding from the voice profile, restated here as an instruction.}

## When a draft gets something wrong

Per the maintenance habit in `creator-voice-skill-builder/references/rubric.md` section 6: the first time a generated draft misses this creator's voice in a way the checks above did not catch, add a line to this file, in the relevant section, describing exactly what went wrong. Do not just remember it. The correction only compounds if it lives here.

---

**Version 1.0 | {build date}**
```
