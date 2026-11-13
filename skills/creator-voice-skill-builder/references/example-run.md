# example-run.md

> **SYNTHETIC.** Maya Torres is a fictional creator. Every post, number, and date below is invented. Source file: `../../_shared/synthetic-data/profile-maya-torres.csv`. Nothing here describes a real person or a real Facebook account.

This is the recipe in `rubric.md` executed start to finish, with every number computed from the source file or reused directly from `facebook-caption-writer/references/example-run.md`, which measured the same 9 mechanics on the same style-source set. Anyone can re-run the parse and check. If a number here disagrees with a recomputation from the CSV, this file is wrong and gets fixed.

Version 1.0 | 2026-08-04

---

# PART 1: THE WORK

Everything in Part 1 is the builder's working, shown so the recipe is auditable. Part 2 is what the user actually receives: the two finished files and the acceptance run.

---

## Step 1: Parse and validate

```
rows parsed                60
date range                 2026-03-21 to 2026-07-28
span                       130 days
empty captions              0 of 60
lite mode                  OFF (60 posts >= 40, 130 days >= 60)
corpus median engagement   458.5
corpus mean engagement     639.7
```

---

## Step 2: Select the style-source posts and run the concentration check

`k = floor(60 / 4) = 15`. Sorted descending by engagement, cut value **700**, no tie at the boundary. Same 15 posts `facebook-hook-analyzer` and `facebook-caption-writer` use on this file, because the top-quartile definition lives in one place, `references/foundations.md` section 6 (condensed from `_shared/engagement-math.md` section 8; full version in the bundle), and every skill in this catalog cites it instead of picking its own.

**The three-part concentration check from `references/foundations.md` section 4 (condensed from `_shared/engagement-math.md` section 5), run on the style-source set as a single bucket:**

```
sum of style-source set's engagement          20,735
highest post's engagement                      4,118

1. top_share = 4,118 / 20,735 = 19.9%                    flag if > 40%      NO FLAG
2. median of the 15                             = 980
   median with the top post removed (14 posts)  = 942.5
   change = |942.5 - 980| / 980 = 3.8%                    flag if > 20%      NO FLAG
3. mean of the 15 = 1,382.33
   divergence = 1,382.33 / 980 = 1.41                     flag if >= 1.5     NO FLAG
```

**All three parts clear.** This profile is built on 15 posts pulling roughly even weight. The highest post is a fifth of the set's total engagement, not a plurality of it, and removing it moves the set's median under 4 percent. Nothing here is one viral post wearing 14 posts as a disguise.

---

## Step 3: The promo screen

**Run against the 15 style-source posts, per `rubric.md` section 2.1.**

```
Category A (partnership / sponsorship language): 0 of 15 matched
Category B (discount-code language):             0 of 15 matched
Category C, structural (Type == link):           2 of 15 matched
Category C, phrasing ("link in bio" etc.):        0 of 15 matched
```

**2 of the 15 style-source posts are flagged, both by the structural link-out test, neither by any language marker:**

| Rank | Date | Engagement | Marker matched | Link_URL |
|---|---|---|---|---|
| 4 | 2026-07-20 | 1,402 | Structural: `Type == link` | `mayatorresorganizes.com/blog/storage-loan` |
| 6 | 2026-06-23 | 1,188 | Structural: `Type == link` | `mayatorresorganizes.com/blog/worst-tuesday` |

**Manual review, per `rubric.md` section 2.2:**

- **Rank 4** ("You do not need more storage. You need fewer decisions."): links to `mayatorresorganizes.com`, her own domain. No partnership or discount-code language anywhere in the caption. **Confirmed: not promotional. Kept in the style-source set.**
- **Rank 6** ("Most organizing systems fail because they were designed on a good day."): same domain, same result. No marker language anywhere in the caption. **Confirmed: not promotional. Kept in the style-source set.**

**Zero posts excluded.** Per `rubric.md` section 2.3, this is the false-positive risk showing up exactly where it was predicted to: the structural link test cannot tell a self-published blog link from a paid placement, because `Type == link` fires on both identically. Both flagged posts turned out to be Maya's own content, on her own domain, and the manual review cleared them in one glance each. The two posts outside the style-source set that also carry `Type == link` (a free-PDF post at 402 engagements and a sheet-storage blog post at 244) were not screened here at all, because the promo screen only runs against the style-source set, not the whole 60-post file.

**Style-source set after review: unchanged, all 15 posts.**

---

## Step 4: Extract the voice markers

**Reused directly from `facebook-caption-writer/references/example-run.md` Step 3, which measured these 9 mechanics on this exact style-source set (same 15 posts, same 0 exclusions).** Recomputing them here would risk a second, slightly different answer to a question this catalog already answered once. Condensed:

| # | Mechanic | Measured result |
|---|---|---|
| 1 | Opening-line pattern | Question Open 4 (26.7%), Bold Claim 3 (20.0%), Number Promise 2 (13.3%), Curiosity Gap 2 (13.3%), Problem Callout 2 (13.3%), Story Cold Open 1 (6.7%), Confession 1 (6.7%). Default opening move: Question Open. |
| 2 | Sentence-length rhythm | Median 12.0 words/sentence, range 5.4 to 16.3, tight (2.7 std dev, under the 3.0 flag). Bands: 2 short, 11 medium, 2 long. Word-count range 38 to 69. Hook word-count range 7 to 18. |
| 3 | Line-break and whitespace style | 13 of 15 use 3 lines (hook, blank, 2-line body). 2 named exceptions: a 4-line post (the 4,118-engagement Story Cold Open) and a 5-line numbered-list post (the 3,402-engagement Number Promise). |
| 4 | Emoji usage | 0 across all 15. |
| 5 | CTA placement and phrasing | 0 of 15 carry an explicit platform CTA. 3 of 15 close on a bare imperative sentence. |
| 6 | Hashtag behavior | 0 across all 15. |
| 7 | Capitalization habits | 15 of 15 hook lines sentence case. 0 ALL-CAPS words. 2 of 15 hooks lead with a digit; one of those two has spelled-out list markers (One:, Two:, Three:, Four:) in its body, digit in the hook and words in the list, same post. |
| 8 | Question frequency | 4 of 15, the same 4 posts as the Question Open row, not a second finding. |
| 9 | First-versus-second person | 10 of 15 second person (66.7%), 4 of 15 first person (26.7%), 1 mixed (6.7%). No fully third-person post. |

---

## Step 5: Choosing the example posts for the built skill

5 posts, spanning 5 of the 7 archetypes present in the style-source set, including the two most common (Question Open and Bold Claim):

| Rank | Engagement | Archetype | Rhythm band | Structure |
|---|---|---|---|---|
| 1 | 4,118 | Story Cold Open | Medium (11.3 w/s) | 4-line exception |
| 2 | 3,402 | Number Promise | Medium (12.0 w/s) | 5-line, numbered-list exception |
| 3 | 1,904 | Confession | Long (15.8 w/s) | 3-line dominant |
| 6 | 1,188 | Bold Claim | Medium (9.8 w/s) | 3-line dominant, closing imperative |
| 10 | 902 | Question Open | Medium (11.0 w/s) | 3-line dominant, closing imperative |

Rank 6 is one of the two posts the promo screen flagged and cleared in Step 3. It is included here as a model post anyway, because the review confirmed it is her own content, not a paid placement, and excluding a cleared post from the model set for no reason would waste the review that just happened.

---

## Step 6: Filling the two templates

The filled files appear in full in Part 2, since they are the actual deliverable. Working note on the example-post selection: Models 1 and 2 above are the same two posts `facebook-caption-writer/references/example-run.md` Step 4 chose as its own Model 1 and Model 2, for the same reason stated there: highest engagement, then highest engagement with a different archetype. This skill's selection then diverges, adding a Bold Claim and a Question Open example beyond what a single 3-caption generation needs, because a permanent voice skill needs more than 3 models to draw from over its lifetime, not just enough for one topic.

---

## Step 7: The 3-test acceptance run

### Test 1: a topic Maya covered. Topic: "kitchen pantry reset before the holidays."

**Model chosen: rank 2, Number Promise, 3,402 engagements** ("4 rules that keep my pantry alive past week three."), because the topic is directly pantry-related and the model's structure, a digit-led hook over a spelled-out numbered list, fits a reset-checklist topic well.

**Draft:**

> 4 rules that get your pantry ready before the holiday cooking starts.
>
> One: pull everything expired before you buy anything new.
> Two: baking supplies get their own shelf, not scattered ones.
> Three: the good serving dishes move to eye level for the next six weeks.
> Four: box the half-used flour and sugar together, so one container holds what four used to.

**Self-check against `voice-skill-template.md`'s checklist:**

| Check | Model (rank 2) | Draft | Pass |
|---|---|---|---|
| Word count | 60 | 61 | yes, within range (38 to 69) |
| Sentence count / words per sentence | 5 sentences, 12.0 w/s | 5 sentences, 12.2 w/s | yes, medium band |
| Hook word count | 10 | 12 | yes, within range (7 to 18) |
| Line count | 5 (named exception, 4-item list) | 5 (4-item list) | yes |
| Emoji | 0 | 0 | yes |
| Hashtags | 0 | 0 | yes |
| CTA | no platform CTA | no platform CTA | yes |
| Capitalization | digit-led hook, spelled-out list markers | digit-led hook ("4"), spelled-out markers (One:, Two:, Three:, Four:) | yes |
| Person | 2nd | 2nd ("your pantry," "you buy") | yes |
| Question mark | none | none | yes |
| No literal reuse | n/a | 1 shared three-word run, disclosed below | **no, disclosed** |
| Out-of-niche disclosure needed? | n/a | topic is directly covered, disclosure not required | n/a |

**1 narrow miss, and it is the same one `facebook-caption-writer/references/example-run.md` disclosed on this exact model post.** The draft's hook shares the three-word run "4 rules that" with the model's hook. Two things force it: the item count of 4 is fixed by the list structure the draft is matching, and "rules that" is the Number Promise marker phrase itself, the number sitting as the head of the subject noun phrase. Per `voice-skill-template.md`'s self-check conclusion (not `rubric.md` section 5, which states the 11-item pass bar but not this exception; see the reconciling note added there), a single narrow miss on Test 1 gets a one-line disclosure rather than a rewrite. **Verdict: PASS, 10 of 11 checks clear, 1 narrow miss disclosed** (the shared three-word run above), not 11 of 11.

### Test 2: a topic Maya never covered, still inside home organizing. Topic: "setting up a small home gym in a spare bedroom corner."

**Model chosen: rank 6, Bold Claim, 1,188 engagements** ("Most organizing systems fail because they were designed on a good day."), the highest-engagement example whose structure, a general-subject declarative hook plus a closing imperative, transfers well to a new equipment-and-habit topic.

**First pass caught a problem before it shipped.** An early draft opened "Most home gyms fail because they were designed for motivation, not friction," which shares the five-word run "fail because they were designed" with the model's hook, and closed on "your worst Tuesday," which borrows the model's central turn of phrase rather than just its shape. Both were rewritten before the check cleared, which is the entire point of running the check mechanically instead of reading the draft once and moving on.

**Final draft:**

> Most home gyms stall because they get built for a mood, not a habit.
>
> You set it up energized. You skip it exhausted.
> Build the corner for the day you almost skip it, not the day you are excited to start.

**Self-check:**

| Check | Model (rank 6) | Draft | Pass |
|---|---|---|---|
| Word count | 39 | 41 | yes, within range (38 to 69) |
| Sentence count / words per sentence | 4 sentences, 9.8 w/s | 4 sentences, 10.25 w/s | yes, medium band |
| Hook word count | 12 | 14 | yes, within range (7 to 18) |
| Line count | 3 (dominant) | 3 | yes |
| Emoji | 0 | 0 | yes |
| Hashtags | 0 | 0 | yes |
| CTA | closing imperative, no platform CTA | closing imperative ("Build the corner..."), no platform CTA | yes |
| Capitalization | sentence case | sentence case, 0 ALL-CAPS | yes |
| Person | 2nd (via "you") | 2nd ("You set it up," "you almost skip it") | yes |
| Question mark | none | none | yes |
| No literal reuse | n/a | 0 shared three-word sequences with the model, checked after 2 revisions | yes |
| Out-of-niche disclosure needed? | n/a | no, home gyms sit inside the same organizing niche as everything Maya covers, just a subject with no example post behind it | n/a, correctly not fired |

**Verdict: PASS**, 11 of 11, after the mechanical reuse check forced two rewrites. This is the test the whole recipe exists to prove: the built skill transfers Maya's structure, rhythm, and closing habit to a subject she has never posted about, without needing an example post on that exact subject to work from.

### Test 3: a topic outside the niche entirely. Topic: "paying off credit card debt."

**This test is graded on the disclosure firing, not just the mechanical checks, per `rubric.md` section 5.**

**Attempt 1, modeled on rank 1 (Story Cold Open, 4,118 engagements), drafted with no disclosure:**

> A client cried over her credit card statement on Monday, and it was not about the number.
>
> It was about a store card she opened in 2019 for a discount she never used again.
> We sat there for ten minutes. Then she closed two cards and kept the one with the lowest rate, and the plan was done in an hour.
> The debt is never about the debt. That is why the minimum payments keep failing.

**This attempt fails, and it fails on two separate grounds:**

1. **The no-literal-reuse check fails, badly.** Run the three-word-sequence comparison against the model post mechanically (tokenize both, lowercase, strip punctuation, compare every three-word run) and it returns **20 shared trigrams**, not a narrow one or two: `a client cried`, `on monday and`, `it was about`, `there for ten`, `for ten minutes`, `is never about`, `that is why`, and 13 more. The draft did not write a new post modeled on the old one. It kept the old one's sentence skeleton almost word for word and swapped in new nouns: pantry became credit card statement, flour became store card, the bins became the minimum payments. That is a copy wearing a new topic, and the mechanical check catches the whole thing at once, not just the one or two phrases a human skim would have flagged.
2. **The out-of-niche disclosure never fires.** Nothing in Maya's example posts covers personal finance. The draft presents a confident, emotionally-loaded financial narrative in her voice with zero content authority behind it, and says nothing about that. Two mechanical failures on one draft is the rubric's own threshold for "rewrite it before it ships" (`facebook-caption-writer/references/rubric.md` section 4, the same 2-or-more rule this skill's self-check inherits), so it does not ship.

**Attempt 2, fixed, using the guardrail's exact fixed string** (`voice-skill-template.md`: "None of the example posts above cover {topic}. This draft applies the measured structure with no content authority behind it. Treat it as untested until you have read it the way {creator name} would.", filled here with `topic = budgeting or credit card debt` and `creator name = Maya`):

> None of the example posts above cover budgeting or credit card debt. This draft applies Maya's measured structure with no content authority behind it. Treat it as untested until you have read it the way Maya would.
>
> A client stared at her card statement last week, and the number was not the problem.
>
> Most of it was one store card, opened years ago for a single discount.
> We called the bank together that same afternoon. She closed two cards and kept the one with the lowest rate, and the whole plan took forty minutes.
> The card was never the problem. Looking away was the six-year habit.

**Self-check on the caption itself, disclosure now present and shown separately above it:**

| Check | Model (rank 1) | Draft | Pass |
|---|---|---|---|
| Word count | 68 | 69 | yes, within range (38 to 69) |
| Sentence count / words per sentence | 6 sentences, 11.3 w/s | 6 sentences, 11.5 w/s | yes, medium band |
| Hook word count | 15 | 16 | yes, within range (7 to 18) |
| Line count | 4 (named exception) | 4 | yes |
| Emoji | 0 | 0 | yes |
| Hashtags | 0 | 0 | yes |
| CTA | no platform CTA, no closing imperative | no platform CTA, no closing imperative | yes |
| Capitalization | sentence case | sentence case | yes |
| Person | 1st (via "we") | 1st (via "We called the bank together") | yes |
| Question mark | none | none | yes |
| No literal reuse | n/a | 0 shared three-word sequences, rewritten twice to clear it: dropped "it was about" (shared with the model's own second sentence) and the whole "is never about... that is why" closing device | yes |
| Out-of-niche disclosure present and ran before the draft? | n/a | yes, shown above the caption | yes |

**Verdict: PASS, on the second attempt.** 11 of 11 mechanical checks clear and the disclosure fired first. **The first attempt is left in this file rather than deleted, because the failure is the actual proof the acceptance run works.** A voice skill that only ever shows passing drafts has not been tested; it has been demonstrated.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable: the two finished files, plus the honesty record of how they were built and tested.

---

# Building Maya Torres's voice skill

60 posts, 2026-03-21 to 2026-07-28, 130 days.

---

## Your style-source set

Top 15 posts by engagement, cut value 700. No single post carries this profile: the highest post is 19.9 percent of the style-source set's total engagement, under the 40 percent flag, and removing it moves the set's median by 3.8 percent, under the 20 percent flag. Mean over median is 1.41, under the 1.5 flag. All three parts of the concentration check clear.

---

## The promo screen

0 posts matched a partnership or sponsorship marker. 0 matched a discount-code marker. 2 of the 15 matched the structural link-out marker (`Type == link`), 0 matched a link-out phrase.

**Manual review list, both shown, neither summarized away:**

| Date | Type | Engagement | Marker matched | Link_URL domain |
|---|---|---|---|---|
| 2026-07-20 | link | 1,402 | Structural: post type is `link` | mayatorresorganizes.com |
| 2026-06-23 | link | 1,188 | Structural: post type is `link` | mayatorresorganizes.com |

**Your decision, recorded:** both confirmed as Maya's own content, linking to her own domain, with no partnership or discount-code language in either caption. Both kept in the style-source set. Zero posts excluded.

No posts in the style-source set matched a partnership, sponsorship, or discount-code marker at all. That does not prove Maya has never run a paid post, only that none of her top 15 used the language this screen checks for.

---

## Your voice, measured

**Opening-line pattern.** Question Open, 4 of 15 (26.7 percent), your default opening move. Bold Claim, 3 of 15 (20.0 percent). Number Promise, Curiosity Gap, and Problem Callout, 2 of 15 each. Story Cold Open and Confession, 1 each. Archetype definitions: `references/hook-archetypes.md` (condensed; the full ladder ships in the facebook-hook-analyzer skill and the bundle).

**Sentence-length rhythm.** Median 12.0 words per sentence, range 5.4 to 16.3. Tight rhythm, 2.7 words standard deviation. 11 of 15 posts sit in the medium band, 8 to 14 words per sentence. Observed word-count range: 38 to 69. Observed hook word-count range: 7 to 18.

**Line-break and whitespace style.** 13 of 15 posts use exactly 3 lines: the hook, a blank line, then a 2-line body. Two exceptions: your best-performing post runs a 4-line structure for a client story, and your second-best runs a 5-line numbered list.

**Emoji usage.** 0 across all 15. You do not use emoji in your winning posts.

**CTA placement and phrasing.** 0 of 15 carry an explicit platform CTA. 3 of 15 close on a bare imperative sentence instead of asking for engagement mechanically.

**Hashtag behavior.** 0 across all 15.

**Capitalization habits.** 15 of 15 hook lines sentence case, 0 ALL-CAPS words anywhere. When a hook leads with a number it is a digit ("4 rules," "7 questions"). When a numbered list appears in the body, its markers are spelled-out words (One:, Two:, Three:, Four:), not digits. Both habits appear in the same post.

**Question frequency.** 4 of 15, the same 4 posts as your Question Open row above.

**First-versus-second person.** 10 of 15 second person, 4 of 15 first person, 1 mixed. First person shows up as a story you were present for or as you describing your own kit or process, never as a distant account of someone else.

---

## Your two finished files

### File 1: `maya-torres-voice-writer/SKILL.md`

```markdown
---
name: maya-torres-voice-writer
description: Write new Facebook captions in Maya Torres's measured voice, on any topic, using a voice profile built from her own top-performing posts. Trigger with "write this like Maya", "give me a caption in my voice", "3 options on {topic} in my style", "write me something for {topic}", or when the user gives a topic and wants a caption that matches this profile.
---

# Maya Torres's voice

Built from 60 captured posts, 2026-03-21 to 2026-07-28, 130 days. Style-source set: the top 15 posts by engagement, cut value 700. No single post carries this profile; the highest post is 19.9 percent of the style-source set's total engagement, under the 40 percent flag.

## Voice profile

**Opening-line pattern.** Question Open (4 of 15, 26.7 percent, her default opening move), Bold Claim (3, 20.0 percent), Number Promise, Curiosity Gap, and Problem Callout (2 each), Story Cold Open and Confession (1 each). These names are descriptive labels assigned during the build; using this skill does not require re-classifying anything, only picking the example below that fits a new topic.

**Sentence-length rhythm.** Median 12.0 words per sentence, range 5.4 to 16.3, tight (2.7 word standard deviation). 11 of 15 sit in the medium band, 8 to 14 words per sentence. Observed word-count range 38 to 69. Observed hook word-count range 7 to 18.

**Line-break and whitespace style.** 13 of 15 posts use exactly 3 lines: hook, blank line, 2-line body. Two exceptions: a 4-line client story (her best post) and a 5-line numbered list (her second-best).

**Emoji usage.** 0 across 15. Never add one, even where it would look natural.

**CTA placement and phrasing.** 0 of 15 explicit platform CTAs. 3 of 15 close on a bare imperative sentence.

**Hashtag behavior.** 0 across 15. Never add one.

**Capitalization habits.** Sentence case throughout, 0 ALL-CAPS words. Hook-leading numbers are digits ("4 rules"). Body numbered-list markers are spelled-out words (One:, Two:, Three:, Four:), even in the same post that used a digit in its hook.

**Question frequency.** 4 of 15, same posts as the Question Open row.

**First-versus-second person.** 10 of 15 second person, 4 first person, 1 mixed. First person narrates a specific event she was present for, or her own process. Never a distant third-person account.

## Example posts, with the evidence attached

**1. 4,118 engagements | Story Cold Open | Medium rhythm | 4-line exception**

> A client cried in her own pantry on Monday, and it was not about food.
>
> It was about a bag of flour her mother bought her in 2019.
> We stood there for ten minutes. Then she kept the flour and let go of forty other things, and the pantry was done in an hour.
> The stuff is never about the stuff. That is why the bins keep failing.

Her highest-engagement post and her flagship structural exception: a client story told in 6 short sentences instead of the usual 3-line default.

**2. 3,402 engagements | Number Promise | Medium rhythm | 5-line numbered-list exception**

> 4 rules that keep my pantry alive past week three.
>
> One: nothing lives above eye level except backstock.
> Two: every category gets a container, and the container is the limit.
> Three: open packages go in one bin, not seven.
> Four: the shopping list lives on the door, not on your phone, because your phone is where lists go to die.

The digit-hook, spelled-out-list capitalization split lives here. Use this model for any checklist-shaped topic.

**3. 1,904 engagements | Confession | Long rhythm | 3-line dominant**

> I have a closet in my own house I do not film.
>
> It is the hall closet, and it is bad. Gift bags, a vacuum that works, a vacuum that does not, and the box the router came in.
> I am telling you because the version of this job where the organizer has no bad closet is a version that does not exist.

Her only confession in the style-source set, and her longest sentence rhythm. Use when the topic calls for an admission against her own authority.

**4. 1,188 engagements | Bold Claim | Medium rhythm | 3-line dominant, closing imperative**

> Most organizing systems fail because they were designed on a good day.
>
> You built it rested. You use it exhausted.
> Design for your worst Tuesday, and your good Saturdays will feel like a bonus instead of a maintenance requirement.

General-subject declarative hook, second-person body, closing instruction. Reviewed and cleared by the promo screen: this post links to her own blog and carries no partnership language.

**5. 902 engagements | Question Open | Medium rhythm | 3-line dominant, closing imperative**

> What is the one drawer you would not let a guest open?
>
> Everyone has one. Mine is the second drawer left of the stove, and it contains a phone charger for a phone I have not owned since 2019.
> That drawer is the honest inventory of your house. Start there, not with the pretty closet.

Her most common archetype, shown with its own closing-imperative habit rather than a platform CTA.

## How to write a new caption with this profile

1. Pick the example post above whose archetype and structure best fit the new topic. If none fit well, use example 1 (the highest-engagement post) and adapt its structure.
2. Match the voice profile above on every mechanic: rhythm band, line structure, zero emoji, zero hashtags, CTA behavior, capitalization, person voice.
3. Never reuse the model post's actual sentences, objects, or numbers. The pattern transfers. The content does not.
4. Run the self-check below before shipping any draft.

## Guardrails (fixed, do not edit)

**No literal sentence reuse.** Before shipping any draft, tokenize it and every example post above, lowercase, strip punctuation, and compare every three-word sequence in the draft against every three-word sequence in each example. Any match means rewrite that phrase before shipping. Do this mechanically, every time; a draft that reads fresh on a skim can still share whole phrases with its model.

**The out-of-niche disclosure.** Before drafting on a topic with no example post behind it and no plausible connection to Maya's covered subjects (home organizing: closets, pantries, entryways, garages, kids' spaces, paper piles, cleaning supplies, linens, client stories), say so first: "None of the example posts above cover {topic}. This draft applies Maya's measured structure with no content authority behind it. Treat it as untested until you have read it the way Maya would." Then draft it, labeled, rather than either refusing outright or shipping it with the same confidence as a topic the examples do support.

## Self-check before shipping any draft

1. Word count within 38 to 69.
2. Sentence count and words-per-sentence in the model post's specific band.
3. Hook-line word count within 7 to 18.
4. Line count and blank-line placement match the dominant 3-line structure, or a named exception.
5. Emoji count is 0.
6. Hashtag count is 0.
7. CTA behavior matches: no platform CTA; a closing imperative only if the model post had one.
8. Capitalization matches: sentence case, no ALL-CAPS, numerals versus spelled-out numbers in the correct role.
9. Person voice matches the specific model post.
10. Question-mark presence matches whether the model was a Question Open.
11. No literal reuse, checked mechanically.
12. If the topic triggered the out-of-niche guardrail, the disclosure ran first.

If a draft fails 2 or more checks, rewrite it before it ships.

---

**Version 1.0 | 2026-08-04**

Built by the PostSnag Creator Voice Skill Builder from a captured export. Not PostSnag's one-click voice skill; this one was built by hand, following a recipe, and it stays accurate only as long as it gets updated the first time it gets something wrong.
```

### File 2: `maya-torres-voice-writer/references/style-playbook.md`

```markdown
# Maya Torres's style playbook

Companion to `maya-torres-voice-writer`. Read this once to understand the voice profile. The voice skill itself is what actually gets used on every future topic.

## Hook patterns

Archetype names below are descriptive labels assigned during the build. Recognizing them again is not required to use this playbook, only picking the one that fits a new topic.

**Default opening move:** Question Open, 4 of 15 style-source posts.

**Question Open (4 posts):** her most common opener. Use for topics where the reader already has a personal answer worth surfacing.
**Bold Claim (3 posts):** her second-most common and her tightest small bucket by the hook analyzer's own concentration check. Use for a confident reframe with no hedge.
**Number Promise (2 posts), Curiosity Gap (2 posts), Problem Callout (2 posts):** each has real evidence behind it. Number Promise for checklist topics, Curiosity Gap for a genuine reveal, Problem Callout sparingly, it is easy to overuse.
**Story Cold Open (1 post), Confession (1 post):** single-instance but her highest and third-highest posts in the whole set. Worth testing again before trusting fully.

**Not seen in her top 15, so not backed by measured evidence here:** Direct Address, Contrarian Take, Myth Bust, Permission Grant, Command. Her wider account uses some of these; this playbook is scoped to her winning posts only, and a draft reaching for one of these five should carry the out-of-niche-style caution even on a covered topic.

## Rhythm and structure

**Sentence rhythm:** tight, 12.0 words per sentence median, 2.7 word standard deviation. Write every draft to land between 8 and 14 words per sentence on average. A draft that comes in looser than that should be cut into shorter sentences, not left as one long one.

**Caption length:** 38 to 69 words. Do not draft meaningfully outside this range without a structural reason, a numbered list needs more room, a one-line reaction needs less, and name the reason when it happens.

**Line structure:** 3 lines by default, hook, blank line, 2-line body. Two earned exceptions: a 4-line structure for a story that needs a third beat, and a 5-line structure for a numbered list. Do not default to an exception just because it is more interesting to write; both exceptions in her data belong to her two highest-performing posts, not to routine ones.

**Hook length:** 7 to 18 words. Outside this range, tighten or expand before shipping.

## Vocabulary and mechanics

**Emoji:** none, ever. Her winning posts have zero.

**Hashtags:** none, ever. Same reason.

**Capitalization:** sentence case throughout, no ALL-CAPS. A hook-leading number is a digit. A body numbered-list marker is spelled out as a word, even inside the same post that used a digit in its hook.

**CTA behavior:** no platform-mechanic CTAs, ever. A closing imperative sentence appears in 3 of 15 posts instead, a direct instruction to the reader rather than a request for engagement.

**Person voice:** second person dominates (10 of 15). First person appears specifically as a story she was present for or her own process described in her own voice, never a distant third-person account of someone else.

## Never do

- Never add an emoji, even where it would look natural. Her winning posts have none.
- Never add a hashtag block. Her winning posts have none.
- Never add a comment-bait or follow-request line. She earns engagement without asking for it mechanically.
- Never write a fully third-person caption with her absent from it. Even her story posts keep her present as narrator.
- Never lead with Direct Address, Contrarian Take, Myth Bust, Permission Grant, or Command without new evidence; none of the five appear in her top 15.
- Never mix a spelled-out hook number with digit list markers; her one numbered-list post does the opposite split, and it is a specific habit, not a free choice.

## When a draft gets something wrong

Per the maintenance habit in `creator-voice-skill-builder/references/rubric.md` section 6: the first time a generated draft misses her voice in a way the self-check did not catch, add a line to this file, in the relevant section. Do not just remember it. The correction only compounds if it lives here.

---

**Version 1.0 | 2026-08-04**
```

---

## The 3-test acceptance run (summary; full drafts and self-checks in Part 1, Step 7)

**Test 1, "kitchen pantry reset before the holidays," modeled on the Number Promise example: PASS, 10 of 11 checks clear, 1 narrow miss disclosed.** The disclosed miss is a narrow carry-over shared with the model's hook, forced by the list structure itself.

**Test 2, "setting up a small home gym in a spare bedroom corner," modeled on the Bold Claim example: PASS.** 11 of 11 checks clear. The first draft shared a five-word run and a borrowed turn of phrase with its model; both were caught by the mechanical reuse check and rewritten before shipping.

**Test 3, "paying off credit card debt," modeled on the Story Cold Open example: FAIL, then PASS.** The first attempt is shown in full in Part 1 because the failure is the proof this check works: it reused the model's exact closing rhetorical device and never disclosed that the topic sits outside anything Maya has posted about. The second attempt opens with the out-of-niche disclosure and rewrites the closing to remove the borrowed structure. 11 of 11 mechanical checks clear on the second attempt, and the disclosure fires first.

---

## Keeping it current

The first time a caption drafted from `maya-torres-voice-writer` gets something wrong, the fix is not "remember to avoid that next time." Open the relevant file, `SKILL.md` for a voice-profile miss, `references/style-playbook.md` for a never-do or a hook-pattern miss, and add one line describing exactly what went wrong. The skill only improves if the correction lives in the file.

---

## What this build is standing on

Analyzed 60 posts captured 2026-03-21 to 2026-07-28, 130 days. Style-source set: top 15 posts by engagement, cut value 700, concentration check clear on all three parts. Promo screen: 2 of 15 flagged by the structural link-out marker, 0 by any language marker, 0 excluded after manual review. Voice mechanics measured on the confirmed 15-post set, reused directly from `facebook-caption-writer`'s measurement of the same set.

Not in Maya's export, so not in this build: sponsored or paid-partnership flags, which is why the promo screen is a manual-review heuristic instead of a filter. Per-emoji reactions. Reach or impressions.

PostSnag captures what you scrolled, so this is a sample of the account, not its full history.

Analysis based on 60 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=creator-voice-skill-builder

---

# APPENDIX: the same recipe on a free-tier export

Run against `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv`, the most recent 30 rows of the same file.

```
posts                30
date range            2026-05-30 to 2026-07-28
span                  60 days
lite mode             ON (30 posts < 40)
k                     floor(30 / 4) = 7
cut value             902
```

**Style-source set: 7 posts instead of 15.** Reusing `facebook-caption-writer/references/example-run.md`'s appendix numbers for the same slice: top post share 31.2 percent, under the 40 percent flag, and 6 distinct archetypes appear across the 7 posts, so the example-post selection for the built skill still gets 3 genuinely distinct models (Number Promise at 3,402, Confession at 1,904, Problem Callout at 1,402), though a 4th and 5th example, which this recipe prefers over the 3 a single caption-writing run needs, would repeat an archetype already used.

**The promo screen on this slice:** recomputed top 7 by engagement at cut 902: 3,402, 1,904, 1,402, 1,206, 1,188, 905, 902. Both link posts clear this cut: the 2026-07-20 post (1,402, "You do not need more storage. You need fewer decisions.") and the 2026-06-23 Bold Claim post (1,188, "Most organizing systems fail because they were designed on a good day."). Same result on review as the full-file run: both link to her own domain, no partnership or discount-code marker in either caption, both kept in the style-source set.

**What thins out:** the built skill still works, with fewer example posts to draw from over its lifetime and a narrower rhythm-band read (7 posts instead of 15 means a single new post shifts every percentage by 14 points). The banner this run would open with:

> **Lite mode.** This capture has 30 posts across 60 days. Below 40 posts or 60 days, your style-source set is smaller than full mode: 7 posts instead of 15. The two finished files below are real and installable, built on less evidence. To get a wider range of example posts, capture about 60 posts across at least 120 days.
