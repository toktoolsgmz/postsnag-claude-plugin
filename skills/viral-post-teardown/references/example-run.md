# example-run.md

> **SYNTHETIC.** This post is fictional, invented for this catalog. Source file: `../../_shared/synthetic-data/single-post.md`. The person, the client, the numbers, and the outcome are all invented. Nothing here describes a real business or a real event.

This is the rubric in `rubric.md` executed start to finish, with every count computed from the source text rather than estimated. Anyone can recount the words and check. If a number here disagrees with a recount of the source file, this file is wrong and gets fixed.

Version 1.0 | 2026-08-04

---

## The source post, embedded verbatim

Embedded here, word for word, so every count in this file is checkable standalone, without opening `_shared/synthetic-data/single-post.md`.

> hey can you break this one down, it's been all over my feed
>
> 2.1k reactions, 380 comments, 640 shares

```
I fired my best-performing client on a Tuesday and my revenue went up 22% the next quarter.

She paid on time. She referred people. She was, on paper, the account everyone would tell you to protect.

She also sent 40 messages a week, moved every deadline, and made three other clients wait. I ran the numbers on a Sunday night because I could not sleep: she was 31% of revenue and 60% of my working hours.

So I gave her a 60-day handoff, wrote a referral into the exit, and we ended it well.

What I did not expect: the two clients who had been waiting both expanded. One of them doubled. The quarter came in 22% ahead of the one before it, with one fewer logo on the wall.

Your best client is not the one who pays the most. It's the one whose work you can do again next month without dreading it.

If you have a name in your head right now, that's the post.
```

---

# PART 1: THE WORK

Everything in Part 1 is the analyst's working, shown so the method is auditable. Part 2 is what the user actually receives.

---

## Step 1: Read the post once

Format: pasted text, no screenshot. Engagement numbers were supplied in the paste itself: "2.1k reactions, 380 comments, 640 shares."

The post is 7 paragraphs, no headings, no bullet list, no hashtags, no CTA-mechanic language ("comment", "share this", "tag a friend" do not appear anywhere in the text).

---

## Step 2: Extract the hook line

Line 1 of the content, after dropping the blank framing lines above the caption ("hey can you break this one down..." is the user's own message about the post, not the post itself, so it is excluded from the caption and not run through the skip tests):

```
I fired my best-performing client on a Tuesday and my revenue went up 22% the next quarter.
```

Skip tests A, B, C: none fire. This line is a complete sentence, not chrome, not a leaked label, not a CTA-mechanic opener. It is the hook as written, one sentence, no truncation needed (the sentence has one terminal period, at the end).

---

## Step 3: Classify the hook

Checked against the fallback table in `rubric.md` section 2, in the order that would matter on the full precedence ladder:

- **Number Promise?** No. `22%` appears in the sentence, but the subject of the sentence is `I`, and the number modifies `revenue`, an object, not the head of the subject noun phrase. The full rubric's marker 3 (`the number is the head of the subject noun phrase`) rules this out explicitly.
- **Question Open?** No question mark, no interrogative opener.
- **Command?** First word is `I`, not an imperative verb.
- **Confession?** First-person subject, but the verb `fired` is past tense describing a single completed event, not a present-tense standing state.
- **Story Cold Open?** Yes. First-person subject (`I`), past-tense narrative verb describing one event (`fired`), plus a specific time anchor (`on a Tuesday`).

**Archetype: Story Cold Open.**
**Marker that fired:** first-person subject, past-tense single event, time anchor ("on a Tuesday").

**Worth naming:** this hook does double duty. It is a clean Story Cold Open by the ladder, and it also carries a Number-Promise-flavored stake (`22%`) inside the same sentence, without qualifying as that archetype structurally. That combination, a scene plus an embedded result, is itself one of the findings below.

---

## Step 4: The structure map

| Beat | Paragraph(s) | Word count | Content |
|---|---|---|---|
| Hook | 1 | 17 | The fired-client result, stated as a scene with a number attached. |
| Build | 2, 3, 4 | 19 + 40 + 18 = 77 | Para 2: why she looked like the client to protect. Para 3: the real cost, in specific numbers. Para 4: the resolution action taken. |
| Payoff | 5, 6 | 36 + 25 = 61 | Para 5: the unexpected result, with numbers. Para 6: the reframed, general lesson the result licenses. |
| CTA | 7 | 13 | An implicit, personal completion task, no platform mechanic named. |

Word counts, counted by hand from the source text: 17 + 19 + 40 + 18 + 36 + 25 + 13 = 168 words across 7 paragraphs.

**The Payoff beat carries a distinct thesis line, per rubric section 3's instruction to fold it in rather than invent a fifth beat:**

> "Your best client is not the one who pays the most. It's the one whose work you can do again next month without dreading it."

This is the post's most quotable line: a reframe ("is not X, it is Y") stated as a general rule, detachable from the specific client story that produced it. Flagged as the likely highest-share line in the post.

**The CTA beat:**

> "If you have a name in your head right now, that's the post."

No platform mechanic word appears (no "comment", "tag", "share"). This is an **implicit** CTA: a personal completion task. It reads as an invitation, not an instruction, and it directly addresses the reader in second person without opening as a Direct Address hook, so it is functioning as a closer rather than an opener.

---

## Step 5: The pacing read

Sentence-by-sentence word counts, counted in order:

| Paragraph | Sentences (word count each) | Paragraph total |
|---|---|---|
| 1 | 17 | 17 |
| 2 | 4, 3, 12 | 19 |
| 3 | 16, 24 | 40 |
| 4 | 18 | 18 |
| 5 | 14, 4, 18 | 36 |
| 6 | 11, 14 | 25 |
| 7 | 13 | 13 |

**13 sentences total, 168 words total, average 12.9 words per sentence.**

Bucketed (short under 10, medium 10 to 20, long 21 or more): **3 short, 9 medium, 1 long.** The single long sentence is paragraph 3's second sentence, 24 words, which is also the sentence carrying the post's most specific numbers (`31 percent of revenue and 60 percent of my working hours`).

**The short-short run:** paragraph 2 opens with two short sentences back to back, 4 words then 3 words ("She paid on time. She referred people."), before a 12-word sentence closes the paragraph. That is a deliberate build in tension through rhythm: two flat, easy facts, then a longer sentence that turns them into a setup ("on paper, the account everyone would tell you to protect").

**Density check:** paragraph 3, at 40 words, is the longest paragraph in the post and sits one word under the density flag from `rubric.md` section 4, which fires at 41 words or more. **It does not flag.** That is the whole reason the boundary is a hard count instead of "roughly 40": at exactly 40 words, a soft threshold gets resolved by whoever is reading, and two runs of this method on the same post would disagree. It is still the densest block in the post, and it is also the paragraph carrying the hard numbers, so the density is earning its keep rather than padding.

**Paragraph rhythm:** every beat of the structure map gets its own paragraph. Seven beats, seven paragraphs, each separated by a blank line. Built for a scroll, not a wall of text.

---

## Step 6: The visual hook

**Omitted.** No screenshot was supplied with this pasted post. Nothing about an image appears anywhere in this run.

---

## Step 7: The engagement read

Supplied numbers: 2.1k reactions, 380 comments, 640 shares. Normalized: 2,100 reactions.

```
engagement     = 2,100 + 380 + 640 = 3,120
comment_ratio  = 380 / 3,120  = 12.2%
share_ratio    = 640 / 3,120  = 20.5%
reaction_ratio = 2,100 / 3,120 = 67.3%   (not a defined ratio in engagement-math.md, shown here only to confirm the three percentages sum to 100.0)
```

**No baseline exists for one post.** These numbers describe this post; they are not ranked against a median or a corpus, because none exists here. One thing worth naming, tied to a feature already found above: a 20.5 percent share ratio, one in five engagements being a share rather than a reaction or a comment, is consistent with a post built around a single quotable reframe line (Step 4's thesis line), which is the kind of line people forward rather than react to. That is a description tied to a visible feature, not a measurement.

---

## Step 8: The 27-item checklist walk

All 27 items in `teardown-checklist.md` were answered before any finding was written, per `rubric.md` section 7. Condensed to category-level results plus the items that actually changed the output. Everything here is consistent with the counts in Steps 4 and 5, because it is the same read, walked item by item.

| Category | Items | Result |
|---|---|---|
| Hook | 1 to 6 | 5 clean, 1 split call |
| Structure | 7 to 12 | 6 clean, all four beats present |
| Pacing | 13 to 17 | 4 clean, 1 split call |
| CTA | 18 to 22 | 5 clean, no platform ask anywhere |
| Credibility | 23 to 27 | 4 clean, 1 weak point |

**Hook, items 1 to 6.** The hook is line 1 and no skip test fired (item 1), it carries no CTA-mechanic phrase (item 2), it carries a concrete number and a day anchor (item 4, `22%` and `on a Tuesday`), it runs 91 characters, under the 120-character working flag (item 5), and it stands alone as its own paragraph (item 6). **Item 3 is the split call:** the hook does not match exactly one archetype with no live competitor. Number Promise competes on the `22%` and loses on marker 3, so the runner-up is recorded rather than dropped. That single answer is where finding 1 comes from.

**Structure, items 7 to 12.** All four beats are present and distinct: a 77-word Build across three paragraphs (item 7), a Payoff that closes the same loop the hook opened, same subject and same number (item 8), an explicit turn at "What I did not expect" (item 9), a general reader-facing lesson separate from the story (item 10), and that lesson phrased as a reframe rather than an instruction (item 11). Item 12 answers no: the Build cannot be cut in half, because paragraph 3 carries the two numbers that make the decision legible, and without them paragraph 5's result is a claim instead of a consequence. A "no" on item 12 is a pass, not a miss.

**Pacing, items 13 to 17.** The post mixes 3 short sentences with a 24-word long one (item 13), runs two short sentences back to back in paragraph 2 at 4 words then 3 (item 14), gives every beat its own paragraph (item 15), and has no paragraph at 41 words or more, with paragraph 3 landing on 40 (item 16). **Item 17 is the split call:** the payoff's `22%` arrives early in its clause, but the two hardest numbers in the post do not. In paragraph 3's 24-word sentence, `31%` is the 16th word and `60%` is the 20th, both sitting behind a 13-word setup about not sleeping. That is a real observation about the post and it is deliberately not one of the three findings, because the numbers still land and the setup is doing its own work. The checklist surfaces it; the three-finding cap keeps it out.

**CTA, items 18 to 22.** Item 18 answers no and that no is the finding: no "comment", "share", "tag", or "follow" appears anywhere in the post. Item 19 answers yes, the last line hands the reader a personal completion task instead. Item 20, the close addresses the reader in second person. Item 21, it runs 13 words, under the 15-word short-close mark. Item 22, it references the hook's subject, a specific client, without repeating its number. Finding 3 comes out of items 18 through 21 together.

**Credibility, items 23 to 27.** Specific checkable numbers throughout (item 23), time anchors in three places, "on a Tuesday", "a Sunday night", "60-day" (item 24), and an admitted cost in the payoff itself, "with one fewer logo on the wall" (item 25). Item 27 is a clean yes and it matters: `22%` appears in the hook and again in paragraph 5, identical both times, which is a callback and a credibility anchor at once. **Item 26 is the one weak point in the post.** "my best-performing client" is a superlative with no number backing it in the same sentence; the backing arrives two paragraphs later at "31% of revenue". Delayed backing, not absent backing, which is a milder version of the failure the item is looking for. Paragraph 2's "everyone would tell you to protect" is the other unbacked appeal, and the post is self-aware about that one, since dismantling it is the whole point of the post.

**What the walk changed.** Two of the three findings below trace to items that a skim would not have produced: item 3's split archetype call and item 18's absent platform ask. Item 17 and item 26 both produced real observations that did not make the cap of three, and they are recorded here rather than deleted, because the working is where the checks live and the deliverable is where only the best three go.

---

## Step 9: Why it worked, 3 findings

Each finding names the checklist item it came from, per `rubric.md` section 8. The item numbers stay in this working; the user-facing version in Part 2 shows the finding without them.

1. **The hook fires as a Story Cold Open with a result number embedded in the same sentence.** *(checklist items 3 and 4.)* "I fired my best-performing client on a Tuesday and my revenue went up 22% the next quarter" gives the reader a scene and a stake in one 17-word line, so they know something surprising happened and roughly how big it was before a single detail is explained. That combination is why the hook works harder than a plain story open or a plain number promise would alone.
2. **Paragraph 2 uses a short-short-long pacing pattern to build tension before the real problem is named.** *(checklist items 13 and 14.)* Two 4-and-3-word sentences ("She paid on time. She referred people.") set up the client as obviously worth keeping, then a 12-word sentence turns that setup into a trap ("on paper, the account everyone would tell you to protect"), right before paragraph 3 reveals the actual cost.
3. **The CTA hands the reader a personal completion task instead of asking for a platform action, and the 20.5 percent share ratio lines up with that design.** *(checklist items 18 through 21, plus the Step 7 ratio.)* "If you have a name in your head right now, that's the post" never says "comment" or "tag," but it points the reader at a specific person, which is the kind of prompt that gets forwarded to that person rather than typed into a comment box.

---

## Step 10: The reuse template

Structural words kept, specifics braced, whole post in one continuous block:

```
I {counterintuitive action} on a {day of the week}, and my {outcome metric} went {up/down} {N%} the next {period}.

{Two short sentences stating the obvious, positive facts about the situation.} {One sentence naming why it looked like the safe, correct choice.}

{One sentence naming the real, hidden cost in specific terms.} {One sentence with the moment you did the math, plus the two hard numbers: it was N% of {resource A} and N% of {resource B}.}

So I {resolution action}, and {how it ended, in a few words}.

What I did not expect: {result 1, in one clause}. {result 2, a short standalone sentence}. The {period} came in {N%} ahead of the one before it, with {the trade-off named plainly}.

Your best {resource or person} is not the one who {surface-level, obvious metric}. It's the one {the real, harder-to-measure value}.

If you have a {kind of person or thing} in your head right now, that's the post.
```

**Sanity check, filled with an unrelated topic (a freelance designer firing a client):** "I turned down my highest-paying client on a Friday, and my referrals went up 40% the next quarter... Your best client is not the one who pays the most. It's the one whose feedback you can take without dreading the call." It still reads like a real post. The abstraction kept the right words.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable. Part 1 was the working.

---

# Teardown: the client-fire post

Read from pasted text. Engagement numbers were supplied.

One post cannot prove a pattern. This is a qualitative read of what this post does, not a measurement of whether it is typical or repeatable. For that, run this on a body of posts.

---

## Hook classification

**Story Cold Open** | marker that fired: first-person subject, past-tense single event, time anchor ("on a Tuesday")

> "I fired my best-performing client on a Tuesday and my revenue went up 22% the next quarter."

This hook is a clean Story Cold Open: a first-person subject, a single past-tense event, and a time anchor. It also carries a Number-Promise-flavored stake inside the same sentence (the 22 percent), without qualifying as that archetype, because the number is not the head of the sentence's subject. Scene plus embedded result, in one line, is doing more work than either alone.

---

## Structure map

**Hook** (17 words): "I fired my best-performing client on a Tuesday and my revenue went up 22% the next quarter."

**Build** (77 words across 3 paragraphs): establishes why the client looked like the obvious one to protect (she paid on time, referred people), then names the real, hidden cost in specific numbers (31 percent of revenue, 60 percent of working hours), then states the resolution taken (a 60-day handoff with a referral built into the exit).

**Payoff** (61 words): the unexpected result, stated with numbers (the two waiting clients expanded, one doubled, the quarter finished 22 percent ahead), plus the post's thesis line: "Your best client is not the one who pays the most. It's the one whose work you can do again next month without dreading it." That line is the most shareable line in the post: a general, detachable rule.

**CTA**: "If you have a name in your head right now, that's the post." No explicit ask (no "comment," "tag," or "share" appears anywhere in the post). This is an implicit CTA, a personal completion task rather than a platform instruction.

---

## Pacing read

13 sentences across 7 paragraphs, averaging 12.9 words per sentence. Sentence mix: 3 short (under 10 words), 9 medium (10 to 20), 1 long (21 or more, the 24-word sentence in paragraph 3 that carries the post's hard numbers).

Paragraph 2 opens with two short sentences back to back, 4 words then 3 words, before a 12-word sentence closes it. That short-short-long run builds tension through rhythm before the real problem is named in the next paragraph.

Paragraph 3, at 40 words, is the densest block in the post. It sits one word under the 41-word density flag, so it is not flagged. It is also the paragraph carrying the specific numbers, so the density is earning its keep.

Every beat of the structure map gets its own paragraph. Seven beats, seven paragraphs, each separated by a line break, built for a scroll rather than a wall of text.

---

## Visual hook

Not analyzed. No screenshot was supplied. Paste one and rerun to get this section.

---

## Why it worked

1. The hook fires as a Story Cold Open with a result number embedded in the same sentence. A scene and a stake in one 17-word line does more than a plain story open or a plain number promise would alone.
2. Paragraph 2 uses a short-short-long pacing pattern, two very short sentences then one longer one, to set the client up as obviously worth keeping right before the next paragraph reveals the trap.
3. The CTA hands the reader a personal completion task instead of asking for a platform action, and the 20.5 percent share ratio below lines up with that design: a prompt that points at a specific person tends to get forwarded to them rather than typed into a comment box.

---

## Engagement read

2,100 reactions, 380 comments, 640 shares. Engagement (reactions plus comments plus shares): 3,120. Comment ratio: 12.2%. Share ratio: 20.5%.

No baseline exists for one post, so these numbers describe this post, they do not rank it against anything. A 20.5 percent share ratio is worth naming because it lines up with the post ending on a detachable, quotable reframe line rather than a question, which is the kind of line people forward more than they comment on.

---

## Reuse template

```
I {counterintuitive action} on a {day of the week}, and my {outcome metric} went {up/down} {N%} the next {period}.

{Two short sentences stating the obvious, positive facts about the situation.} {One sentence naming why it looked like the safe, correct choice.}

{One sentence naming the real, hidden cost in specific terms.} {One sentence with the moment you did the math, plus the two hard numbers: it was N% of {resource A} and N% of {resource B}.}

So I {resolution action}, and {how it ended, in a few words}.

What I did not expect: {result 1, in one clause}. {result 2, a short standalone sentence}. The {period} came in {N%} ahead of the one before it, with {the trade-off named plainly}.

Your best {resource or person} is not the one who {surface-level, obvious metric}. It's the one {the real, harder-to-measure value}.

If you have a {kind of person or thing} in your head right now, that's the post.
```

---

## What this teardown is standing on

One post, read once, for its hook, its structure, and its pacing. No ranking, no median, no archetype table: those require more than one post and this skill never produces them from a single one. Engagement numbers were supplied and reported as raw counts and ratios, with no baseline, because no baseline exists for one post. Not in this reading: whether the post was boosted, per-emoji reaction detail, reach or impressions, comment text, or anything about the account that posted it.

Analysis based on 1 captured post. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=viral-post-teardown
