# rubric.md

The full method for Viral Post Teardown. Written so an agent with no other context can run it on one pasted post, or one screenshot, and reach a defensible teardown.

Version 1.0 | 2026-08-04

---

## Section 0: The Triple Hook, adapted to one post

The Triple Hook read comes from video analysis: the open fires three channels in parallel so that if one misses the reader, another catches them. `facebook-hook-analyzer` adapts this to a full profile export. This skill adapts it to exactly one post.

**The three channels on a single Facebook post:**

| Channel | Where it comes from | Available? |
|---|---|---|
| **First-line hook** | The extracted opening sentence, classified into one archetype | Always. Section 1 and 2. |
| **Text hook** | The whole caption's shape: the structure map and the pacing read | Always. Sections 3 and 4. |
| **Visual hook** | The image or screenshot | **Only if the user supplies one.** Section 5. |

**Discipline, non-negotiable:** quote the hook, the structure-map lines, and any on-screen text verbatim. Never paraphrase and present it as a quote. If the caption is empty (image-only post) or you were not shown the image, say that plainly rather than inventing content for the missing channel.

---

## Section 1: Extracting the hook line

A wrong number presented with confidence is worse than no number.

Identical procedure to `facebook-hook-analyzer`'s rubric section 1, restated here so this skill runs standalone:

1. Split the post's text on line breaks. Drop empty lines.
2. Take the first remaining line. Skip it if it matches any of the three tests below, then test the next line. Stop after 3 skips and take whatever line you land on.
3. If the line holds multiple sentences, the hook is the first sentence only, up to the first terminal punctuation mark.
4. Record the hook verbatim, including punctuation and capitalization.

**Skip test A, the CTA-first pattern:** skip a line that opens with an imperative aimed at the platform mechanic (`follow`, `comment`, `share this`, `tag a`, `drop a`, `type`, `save this`, `like if`), or is entirely a link, an @ mention, or a hashtag block.

**Skip test B, chrome:** skip a line under 3 words that is not a complete sentence with a verb (`New post`, `Day 14`, a lone emoji).

**Skip test C, a leaked label:** skip a line beginning with an export or drafting artifact (`Copy:`, `Caption:`, `Draft:`, `Post:`).

**If nothing survives**, the post is image-only or unreadable text. Say so and run only the visual-hook section, if an image was supplied.

---

## Section 2: Archetype classification, by reference

**Full definitions, recognition markers, and the precedence ladder ship locally at `references/hook-archetypes.md`** (condensed; full version in the facebook-hook-analyzer skill or the bundle). That file carries all 12 archetypes, each with its recognition markers and the conjunctive/disjunctive qualifiers, plus the precedence ladder and the borderline-call table, condensed from `facebook-hook-analyzer`'s full rubric sections 1, 2, and 2.13. This file does not repeat its worked examples; run classification from the local copy.

**Quick-reference table**, one line per archetype plus its key marker, so the ladder's logic is visible even without opening the embed:

| Archetype | One-line definition | Key marker(s) |
|---|---|---|
| Number Promise | The hook leads with a count of what the post delivers, and the number is the head of the subject. | Cardinal number, quantifies the post's own contents, AND is the head of the subject noun phrase (needs all three). |
| Question Open | The hook is a question in form, and the reader answers it in their head before deciding to read on. | Ends in a question mark, OR opens with an interrogative word, OR opens with an inverted modal/auxiliary (any one is sufficient). |
| Command | A bare imperative as the first word, with no subject and no preceding clause. | First word is an imperative verb, no subject, no question mark, no audience filter in front. |
| Confession | A present-tense admission that costs the author authority, not a past event. | First-person subject; present tense or present perfect describing a standing state (not a past event); against the author's own interest. |
| Story Cold Open | The hook drops the reader into a specific past event, usually first person, with no setup. | First-person subject or a named third party, AND a past-tense narrative verb describing a single event (needs the first two). |
| Direct Address | The hook names or filters a specific audience before making any claim. | First clause names an audience segment vocatively or by description, or is a conditional that filters readers; the address must come before the claim. |
| Contrarian Take | The hook names what people commonly believe, then explicitly rejects it. | Explicit reference to what others believe, followed by a rejection (needs the explicit reference). |
| Myth Bust | The hook names a specific, checkable belief and corrects it as false. | Names a specific belief as false; the correction is checkable in principle, not a matter of taste. |
| Permission Grant | The hook releases the reader from a named obligation or a guilt they are carrying. | Second person; an explicit release phrase; the released obligation is named specifically. |
| Curiosity Gap | The hook names a definite, specific thing and withholds its identity until later. | A definite reference to an unnamed specific, AND an explicit withholding move or a sentence that ends without naming it (needs both). |
| Problem Callout | Second person, naming a failure or unwanted state the reader recognizes as their own. | Second-person subject in the first clause, AND a negative state or failure attributed to the reader (needs the first two). |
| Bold Claim | A flat declarative about how something works, stated with no hedge and no evidence in the hook itself. | Declarative sentence with a general subject (not `you`, not `I`); no number, no question mark, no named audience, no narrative event. Catch-all, sits last. |

**Classification rule:** run the precedence ladder in `references/hook-archetypes.md` section 3, top to bottom, first match wins: Number Promise, Question Open, Command, Confession, Story Cold Open, Direct Address, Contrarian Take, Myth Bust, Permission Grant, Curiosity Gap, Problem Callout, then Bold Claim, the catch-all, last. Curiosity Gap and Problem Callout sit at positions 10 and 11 and they matter: a second-person hook naming a failure is a Problem Callout, not a Bold Claim, and getting that pair the wrong way round is the most common misclassification in this whole ladder. If nothing else fits and the hook is a flat assertion, it is Bold Claim. If the hook survives extraction but matches nothing at all, classify it `UNCLASSIFIED` and say so rather than forcing a label. For a borderline call, use `references/hook-archetypes.md` section 4: form wins over function.

**Note the file dependency here, matching the note in SKILL.md:** this skill and `facebook-hook-analyzer` are meant to ship together in the catalog. `references/hook-archetypes.md` ships inside this skill folder so a standalone download still classifies correctly on its own; it is a condensed copy, and the full rubric with worked examples lives in the facebook-hook-analyzer skill or the bundle.

---

## Section 3: The structure map

The core of the single-post read. Four beats, identified mechanically from the post's own text, not from a template you impose on it.

| Beat | How to find it |
|---|---|
| **Hook** | The extracted hook line from Section 1. |
| **Build** | Every paragraph between the hook and the payoff. Context, tension, complications, or evidence the post needs before it can deliver. |
| **Payoff** | The paragraph or paragraphs where the post delivers on what the hook promised: a reveal, a result, a resolution, a number that answers the question the hook raised. Look for resolution language: "what I did not expect", "turns out", "here is what happened", a contrast marker, a stated outcome. |
| **CTA** | The final line or lines. Explicit if it asks directly for an action (comment, share, tag, follow, using the same mechanic words as Skip test A). Implicit if it hands the reader a personal completion task without naming a platform action ("if you have a name in your head right now"). If neither is present, the last line is the post's thesis or insight instead, and the teardown says there is no explicit CTA. |

**When the post carries a separate thesis line** (a general, reader-facing lesson distinct from the specific story, usually phrased as a reframe: "X is not the one who Y, it is the one who Z"), fold it into the Payoff beat as the second half: the specific result, then the general lesson the result licenses. Do not invent a fifth beat for it. Quote it in the Payoff section and flag it as the post's most shareable line if it reads as a standalone, quotable claim.

**If a beat is missing entirely** (no clear build, the hook and payoff are the same sentence, no CTA of either kind), say so plainly in that beat's line rather than stretching another beat to cover it. A missing beat is itself a finding: a post with no build reads as a punchline; a post with no CTA reads as a statement rather than an invitation.

---

## Section 4: The pacing read

Computed directly from the post's own sentences and paragraphs. Two things almost nobody checks on a single post, and both are cheap to compute.

**Sentence length.** Count words per sentence. Bucket every sentence:

- short: under 10 words
- medium: 10 to 20 words
- long: 21 words or more

Report the mix (count in each bucket) and the average sentence length. **Name any run of 2 or more short sentences back to back.** A short-short run right after the hook, before a longer sentence lands the real content, is a deliberate pacing device: it builds tension through rhythm before the release. Call it out by naming the sentences, not just the pattern.

**Paragraph rhythm.** Count paragraphs (blocks separated by a blank line). Report the word count of each. **Flag any paragraph that runs to 41 words or more** as a density risk. The boundary is a hard count, not a "roughly": 40 words does not flag, 41 does, so that the same paragraph resolves the same way here, in `teardown-checklist.md` item 16, and in `output-template.md`. A flagged paragraph asks more of a scrolling reader than the paragraphs around it, and that is worth naming whether it works or not.

**Line breaks.** State whether each beat of the structure map (hook, each build step, payoff, CTA) gets its own paragraph, or whether beats run together in longer blocks. A post that gives each beat its own paragraph is built for a phone screen. A post that runs several beats into one block is asking for a more committed reader.

**No em dash, no hedge in this section.** Report the numbers. A pacing read with no specific counts attached is an opinion wearing the costume of an analysis.

---

## Section 5: The visual hook

**Run this section only if the user supplied a screenshot. Otherwise write one line saying it was not supplied and move on. Never guess at an image you were not shown.**

1. **The muted test.** With the caption covered, does the image alone stop a scroll? Say yes or no and name what does the stopping: a face, a result graphic, a before-and-after split, a large rendered number, high contrast, a pattern interrupt.
2. **On-screen text.** Quote any burned-in text verbatim, or mark it `NONE` or `UNREADABLE`. Never report a best guess as if it were read.
3. **The cross-check against the text hook.** Three possible outcomes: **distinct angles** (the image and the line attack from different directions), **redundant** (the image repeats the line, nothing gained), or **resolved** (the image already answers the question the hook line asked, which closes the reader's loop before they read the caption).

**Reactions visible in a screenshot** (like emoji icons) are never a substitute for the printed count. If the printed engagement numbers are not visible or not legible, the engagement-read section is omitted, not estimated from icon density.

---

## Section 6: The engagement read, only when numbers are supplied

**Never estimate engagement numbers. Only compute this section when the user has given you at least a combined engagement figure, or the individual reactions, comments, and shares.**

Using the shared definitions in `_shared/engagement-math.md` section 1:

```
engagement     = reactions + comments + shares
comment_ratio  = comments / engagement
share_ratio    = shares   / engagement
```

Report all three numbers, rounded per the shared rounding rule (whole numbers for engagement, one decimal for percentages).

**The rule this section exists to enforce: no baseline exists for one post.** `engagement-math.md` defines a discussion post and a save-and-send post relative to a corpus median comment ratio and share ratio. A single post has no corpus, so this skill never classifies a post as "above median" or "your best type of post" against a baseline that is not there. What it can honestly say: the raw ratios, and a plain-language read of what a high share ratio or a high comment ratio tends to mean structurally (a share ratio that stands out as a large share of engagement pairs naturally with a quotable, sendable line; a comment ratio that stands out pairs with an open question or a personal prompt). State that reading as a description tied to a visible feature of the post, in one sentence, never as a ranked or measured claim.

---

## Section 7: Walk the 27-item checklist

**Run this before you write a single finding. It is a required step of the method, not an optional appendix.**

`teardown-checklist.md` holds 27 mechanical yes/no checks in 5 categories: hook (items 1 to 6), structure (7 to 12), pacing (13 to 17), CTA (18 to 22), and credibility (23 to 27). Sections 1 through 6 above gave you the raw reads: the hook line, the structure map, the pacing counts, the engagement ratios. The checklist is what turns those reads into a list of specific, named observations, and it is the only thing standing between a teardown and a well-written impression of a post.

**How it runs:**

1. Walk all 27 items in order. Answer each yes, no, or n/a. Do not skip a category because the post looks simple.
2. A "no" is a finding as often as a "yes" is. A post with no build beat, a flat sentence rhythm, or an unbacked superlative has told you something specific about itself, and that belongs in the output rather than in a discarded working note.
3. Record the answers as category-level results, not as 27 lines of prose in the deliverable. The user sees the findings; the checklist is the working. `example-run.md` Part 1 shows the condensed form: a count per category plus the specific items that decided the findings.

**The gate this creates, and the reason the step exists:** every finding in Section 8 must trace back to a numbered item that was actually answered. If a finding cannot be traced to one, it does not go in the output. That rule is what makes "why it worked" a report of checks rather than a paragraph of confident-sounding language, and it only works if the checklist is genuinely walked before the findings are written, not reverse-engineered from them afterwards.

---

## Section 8: Why it worked, 3 findings maximum

**Never more than 3. If you have 5 candidate findings, cut to the 3 most specific ones tied to a feature nobody would notice on a skim.**

Each finding follows the same shape: **name the visible feature, then the effect it plausibly has, in one or two sentences.** Never a finding that could be pasted under a different post unchanged. **Every finding must trace to a checklist item you actually answered in Section 7, and the working names which item**, because a finding with no check behind it is the thing this whole method exists to prevent. The user-facing output shows the finding, not the item number.

Good sources for findings, in rough order of how often they hold up:

1. A hook that combines two channels in one line (an archetype plus a concrete number or time anchor) delivers more than either channel alone.
2. A pacing device found in Section 4: a short-short run, a single long sentence carrying the post's key number, a paragraph break placed to isolate the payoff.
3. A thesis or reframe line in the Payoff beat that is quotable on its own, independent of the story that produced it.
4. A CTA that hands the reader a personal completion task instead of asking for a platform action, which converts the ask into something that does not feel like an ask.
5. A specific, checkable number repeated at two points in the post (hook and payoff), which functions as a callback and a credibility anchor at once.

**Never write a finding about the algorithm, about reach, or about anything not visible in the text or image you were given.** If the post's numbers were supplied, at most one of the 3 findings may reference them, and only to tie a ratio to a feature already named in the structure map or pacing read, per Section 6's no-baseline rule.

---

## Section 9: Extracting the reuse template

**One fill-in template covering the whole post's structure**, not just the hook. This is what separates a teardown from a hook-library entry.

**Procedure:**

1. Walk the structure map beat by beat: hook, build, payoff, CTA.
2. For each beat, replace nouns, numbers, names, and topic-specific details with a braced slot: `{action}`, `{time anchor}`, `{outcome metric}`, `{N%}`, `{result}`, `{trade-off}`.
3. **Keep every structural word**: the negation, the contrast, the connective tissue ("and it was not about", "what I did not expect", "is not the one who"). Those are the pattern. The nouns are the post's, not the template's.
4. Keep the beat lengths in proportion. A one-sentence hook abstracted into a two-sentence template is a different hook.
5. Present the whole thing as one continuous fill-in block the user can read top to bottom and complete in one pass, not four separate snippets.
6. **Check the 6-word rule.** No single run in the finished template carries more than 6 consecutive words verbatim from the source post, including the structural phrases kept in step 3. Check it literally: slide a 7-word window across the template and compare it against the source post's text. (Working number, labeled: 6 is this catalog's threshold, not a platform fact, the same one `facebook-content-calendar-builder` uses for its drafts. It sits just above the length of a common phrase and just below the length of a distinctive clause.) If a structural phrase worth keeping runs longer than 6 words, cut it to its shortest form that still carries the structure.

**Sanity check before shipping it:** fill the template with a topic from an unrelated niche. If it still reads like a real post, the abstraction kept the right words. If it reads like a form with blanks in it, too much was stripped out; put a structural word back.

---

## Section 10: What this rubric refuses to do

- **No ranking, no median, no archetype table.** All three require more than one post. This skill produces one teardown, not a leaderboard.
- **No claim that this post is representative of the account that posted it.** One post is one post.
- **No engagement claim without supplied numbers**, and no baseline claim even when numbers are supplied, per Section 6.
- **No finding that does not trace to a checklist item that was actually answered**, per Section 7.
- **No sponsored-versus-organic read.** Nothing in a pasted post or a screenshot reveals a paid-partnership flag.
- **No description of an image that was not supplied**, and no description of image details beyond what is legible in what was supplied.
- **No superlative** ("the best hook", "guaranteed to work") that is not a literal, checkable statement about this one post.
