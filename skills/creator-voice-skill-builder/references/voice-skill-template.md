# voice-skill-template.md

The fill-in template that becomes the permanent voice skill. Complete every bracketed slot using the measurements from `rubric.md` sections 1 through 3. Do not leave a slot with a placeholder in it when you hand this over: an unfilled bracket in a shipped skill is a tell that the recipe was not finished.

This file, once filled, is the artifact the user installs and keeps. It is written in the same frontmatter-plus-body shape as every other skill in this catalog because it needs to install the same way.

Version 1.0 | 2026-08-04

---

## How to fill this

1. Work top to bottom. The frontmatter first, then the voice profile, then the examples, then the guardrails.
2. Every voice-profile slot takes a **measured number from Section 3 of `rubric.md`**, not a description of one. "0 emoji across 15 style-source posts" is a fill. "Does not use many emoji" is not.
3. The three guardrail slots at the end are fixed text, not fill-in slots. They ship in every voice skill this recipe produces, unedited, because they are the guardrails `rubric.md` section 4.3 requires.
4. When you are done, this file plus a filled `style-playbook-template.md` are the two files the user keeps.

---

```markdown
---
name: {creator-name}-voice-writer
description: Write new {platform} captions in {creator name}'s measured voice, on any topic, using a voice profile built from their own top-performing posts. Trigger with "write this like {creator name}", "give me a caption in my voice", "{n} options on {topic} in my style", "write me something for {topic}", or when the user gives a topic and wants a caption that matches this profile.
---

# {Creator name}'s voice

Built from {N} captured posts, {first date} to {last date}, {span} days. Style-source set: the top {k} posts by engagement, cut value {cut}. {If the concentration check flagged: state which post and how much extra weight it carries. If not: "No single post carries this profile; the highest post is {top_share} percent of the style-source set's total engagement, under the 40 percent flag."}

## Voice profile

**Opening-line pattern.** {Archetype table: name, count, share. Name the default opening move in one sentence. Archetype names are descriptive labels assigned during the build; this file must not cite `facebook-hook-analyzer` or any other sibling skill by path, because a user who downloaded only this skill will not have that file, and this skill does not need to re-classify anything to use the labels below.}

**Sentence-length rhythm.** {Median words per sentence, range, tight-or-loose call with its standard deviation, band counts. State the observed word-count range and hook word-count range as two separate numbers.}

**Line-break and whitespace style.** {Dominant line count and its share. Named exceptions and what makes them different.}

**Emoji usage.** {Count across the style-source set. If zero, the plain statement that this creator does not use emoji and a draft should not add one.}

**CTA placement and phrasing.** {Count of explicit platform CTAs, separately from the count of closing-imperative sentences. Both can be zero; report both regardless.}

**Hashtag behavior.** {Count, repeats if any, typical position. If zero, say so plainly.}

**Capitalization habits.** {Hook-line case, ALL-CAPS word count, numerals-versus-spelled-out-numbers in both roles: hook lead and list marker, stated separately if they differ.}

**Question frequency.** {Share of hooks with a question mark. Cross-referenced against the opening-line pattern table, not presented as independent evidence.}

**First-versus-second person.** {Distribution across 1st, 2nd, mixed, and true third-person if present. One sentence on how first person specifically gets used, when it appears.}

## Example posts, with the evidence attached

{3 to 5 style-source posts, selected the same way `facebook-caption-writer/references/rubric.md` section 3.1 selects model posts: highest engagement, then highest engagement with a different archetype, then highest remaining with a third distinct archetype and a different rhythm band where possible.}

**{rank}. {engagement} engagements | {archetype} | {rhythm band}**

> {caption, verbatim}

{One line: why this post is included as a model, what pattern it demonstrates that the others do not.}

{Repeat for each example post.}

## How to write a new caption with this profile

1. Pick the example post above whose archetype and structure best fit the new topic. If none fit well, use the highest-engagement example and adapt its structure rather than inventing a new one.
2. Match the voice profile above on every mechanic: rhythm band, line structure, emoji and hashtag behavior (none, if the profile says none), CTA behavior, capitalization, person voice.
3. Never reuse the model post's actual sentences, objects, or numbers. The pattern transfers. The content does not.
4. Run the self-check below before shipping any draft.

## Guardrails (fixed, do not edit)

**No literal sentence reuse.** Before shipping any draft, tokenize it and every example post above, lowercase, strip punctuation, and compare every three-word sequence in the draft against every three-word sequence in each example. Any match means rewrite that phrase before shipping. Do this mechanically. Do not eyeball it; a draft that reads like a fresh caption on a skim can still share whole phrases with its model, and only the sequence comparison catches that reliably.

**The out-of-niche disclosure.** Before drafting on a topic with no example post behind it and no plausible connection to this creator's covered subjects, say so first: "None of the example posts above cover {topic}. This draft applies the measured structure with no content authority behind it. Treat it as untested until you have read it the way {creator name} would." Then draft it, labeled, rather than either refusing outright or shipping it with the same confidence as a topic the examples do support.

**The 6-word originality guardrail.** No draft reuses more than 6 consecutive words from any example post above. Check it literally, sliding a 7-word window across the draft against every example post. The template is the structure; the nouns are new. This sits alongside the sentence-reuse guardrail above, not in place of it, and it is the coarser, catalog-wide floor every drafting skill in this catalog shares.

## Self-check before shipping any draft

1. Word count within the observed range from the sentence-rhythm section.
2. Sentence count and words-per-sentence in the same band as the model post used.
3. Hook-line word count within the observed hook-length range.
4. Line count and blank-line placement match the dominant structure, or intentionally match a named exception.
5. Emoji count matches the profile (0 if the profile found 0).
6. Hashtag count matches the profile (0 if the profile found 0).
7. CTA behavior matches: no platform CTA if the profile found none; a closing imperative only if the model post specifically had one.
8. Capitalization matches: hook-line case, no stray ALL-CAPS, numerals versus spelled-out numbers assigned to the correct role.
9. Person voice matches the model post specifically.
10. Question-mark presence in the hook matches whether the model post was a Question Open.
11. No literal reuse, checked mechanically per the guardrail above.
12. If this topic triggered the out-of-niche guardrail, the disclosure is present and it ran before the draft, not after.
13. No 6-consecutive-word run shared with any example post, checked mechanically per the 6-word originality guardrail above.

**If a draft fails 2 or more checks, rewrite it before it ships.** A single narrow miss is worth a one-line note. Two or more means the draft is not actually modeled on the profile above.

---

**Version 1.0 | {build date}**

Built by the PostSnag Creator Voice Skill Builder from a captured export. Not PostSnag's one-click voice skill; this one was built by hand, following a recipe, and it stays accurate only as long as you update it per the maintenance habit in `creator-voice-skill-builder/references/rubric.md` section 6.
```
