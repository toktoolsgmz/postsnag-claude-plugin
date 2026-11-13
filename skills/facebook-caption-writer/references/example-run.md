# example-run.md

> **SYNTHETIC.** Maya Torres is a fictional creator. Every post, number, and date below is invented. Source file: `../../_shared/synthetic-data/profile-maya-torres.csv`. Nothing here describes a real person or a real Facebook account.

This is the rubric in `rubric.md` executed start to finish, with every number computed from the source file rather than estimated. Anyone can re-run the parse and check. If a number here disagrees with a recomputation from the CSV, this file is wrong and gets fixed. Topic requested: **garage shelving one-day makeover.**

**What is standalone-checkable here and what is not.** The full text of all 15 style-source captions lives in the bundle fixture (`_shared/synthetic-data/profile-maya-torres.csv`), not reproduced word for word in this file. What this file does reproduce, in full, is the measured profile: every count, median, share, and formula in Steps 1 through 4 is shown with its inputs and its arithmetic, so the numbers are checkable against this file alone even without the CSV open. Quoted hook lines, model-post captions, and the specific phrases cited as catalog-mechanic evidence are all reproduced verbatim where they appear in Steps 3, 4, and 6.

Version 1.0 | 2026-08-04

---

# PART 1: THE WORK

Everything in Part 1 is the analyst's working, shown so the method is auditable. Part 2 is what the user actually receives.

---

## Step 1: Parse and validate

Parsed with a real CSV reader, columns addressed by header name.

```
rows parsed                60
date range                 2026-03-21 to 2026-07-28
span                       130 days
empty captions             0 of 60
lite mode                  OFF (60 posts >= 40, 130 days >= 60)
corpus median engagement   458.5
corpus mean engagement     639.7
```

Zero empty captions is a receipt, not a non-event. Every mechanic below is measured on caption text, so a file with 9 empty captions in its top quartile would be measuring 6 posts and calling it 15. This run had none, and the count is printed so nobody has to assume it.

---

## Step 2: Select the style-source posts

`k = floor(60 / 4) = 15`. Sorted descending by engagement, cut value **700**, no tie at the boundary. Same 15 posts the hook analyzer's example run uses, because this rubric shares the top-quartile definition in `references/foundations.md` section 6 (condensed; full version in the bundle).

```
sum of style-source set's engagement    20,735
highest post's engagement                4,118
top_share                                4,118 / 20,735 = 19.9%
```

19.9 percent is under the 40 percent concentration-check flag. **No flag.** The style profile below is built on 15 posts pulling roughly even weight, not one viral post wearing 14 posts as a disguise.

---

## Step 3: The 9 mechanics, measured on the 15 style-source posts

### 3.1 Opening-line pattern

Classified with the 12-archetype ladder in `references/hook-archetypes.md` sections 2 and 3 (condensed; full version in the facebook-hook-analyzer skill or the bundle).

| Archetype | Count | Share |
|---|---|---|
| Question Open | 4 | 26.7% |
| Bold Claim | 3 | 20.0% |
| Number Promise | 2 | 13.3% |
| Curiosity Gap | 2 | 13.3% |
| Problem Callout | 2 | 13.3% |
| Story Cold Open | 1 | 6.7% |
| Confession | 1 | 6.7% |

**Question Open, 4 of 15, is her default opening move**, and no other archetype reaches it. Bold Claim is second at 3. The two together are 7 of the 15 posts that earned a place in her own top 15, and the remaining 8 are spread across five archetypes, so the top of her style is concentrated and the tail is not.

### 3.2 Sentence-length rhythm

Words per sentence, one value per style-source post: 11.3, 12.0, 15.8, 10.0, 13.8, 9.8, 5.4, 12.5, 12.0, 11.0, 12.5, 10.2, 16.3, 12.0, 7.6.

```
median words per sentence     12.0
range                         5.4 to 16.3
population standard deviation 2.7
```

2.7 is under this skill's 3.0-word tight/loose flag. **Tight rhythm.** Band counts: 2 short (under 8 words per sentence), 11 medium (8 to 14), 2 long (over 14). **11 of 15 posts sit in the medium band.** She does not swing between clipped one-liners and long run-ons; her winning posts hold a narrow lane.

### 3.3 Line-break and whitespace style

| Line count | Posts | Share |
|---|---|---|
| 3 lines (hook, blank line, 2-line body) | 13 | 86.7% |
| 4 lines (hook, blank line, 3-line body) | 1 | 6.7% |
| 5 lines (hook, blank line, 4-line numbered-list body) | 1 | 6.7% |

**13 of 15 style-source posts use exactly 3 lines**, one blank line after the hook and nowhere else in the caption. The two exceptions are both posts that needed more room: the 4,118-engagement Story Cold Open (a client story that needed a third body beat) and the 3,402-engagement Number Promise (a 4-item numbered list). Both exceptions are named as model posts below, and their captions get drafted with their own longer structure, not forced into the 3-line default.

### 3.4 Emoji usage

**0 emoji across all 15 style-source posts.** This creator does not use emoji anywhere in her winning content. A generated caption does not add one, even a single one, even where it would look natural.

### 3.5 CTA placement and phrasing

**0 of 15 posts carry an explicit platform CTA** (comment, follow, tag, share, or a bracketed comment keyword). None of her top posts ask for engagement mechanically.

**3 of 15 posts close on a bare imperative sentence**, a direct instruction rather than a platform ask:

- "Design for your worst Tuesday, and your good Saturdays will feel like a bonus instead of a maintenance requirement." (1,188 engagements)
- "Give that one the good rod and the front of the closet, and put the other two on a deadline." (980 engagements)
- "Start there, not with the pretty closet." (902 engagements)

She closes 1 in 5 of her winners with a command aimed at the reader's next move, never with a platform mechanic.

### 3.6 Hashtag behavior

**0 hashtags across all 15 style-source posts.** Does not use hashtags.

### 3.7 Capitalization habits

**15 of 15 hook lines use sentence case.** No Title Case, no ALL-CAPS opening word. **0 ALL-CAPS words anywhere in the style-source set.**

**Numerals versus spelled-out numbers, and they are not the same habit in the same post.** 2 of 15 hook lines lead with a digit: "4 rules that keep my pantry alive past week three." and "7 questions that end every 'but I might need it' argument." One of those two, the 4-rules post, has a numbered-list body, and its list markers are spelled out as words, not digits: One:, Two:, Three:, Four:. **Digit in the hook, word in the list, same post.** A generated caption in this creator's style needs both halves of that habit, not just one.

### 3.8 Question frequency

**4 of 15 style-source posts open with a question.** This is the same 4 posts as the Question Open archetype in section 3.1, not a second, independent finding.

### 3.9 First-versus-second person

| Person | Count | Share |
|---|---|---|
| Second person (you, your) | 10 | 66.7% |
| First person (I, my, we, our) | 4 | 26.7% |
| Mixed | 1 | 6.7% |

**No fully third-person caption appears in the style-source set.** First person shows up two ways: narrating a specific event she was present for ("We stood there for ten minutes," the 4,118-engagement client story; "I have a closet in my own house I do not film," the confession), and describing her own kit or process in the author's voice ("the cheapest thing in my organizing kit"). It never appears as a distant account of someone else with the author absent.

---

## Step 4: Scanning the wider caption-mechanics catalog

Per Method step 5 in `SKILL.md`, every style-source post gets checked against `caption-mechanics-catalog.md`'s 24 wider mechanics, on top of the 9 core ones already measured above. Reported below only where the detection rule in the catalog entry actually fires; a near-miss is named as a near-miss, not rounded up to a finding.

**Mechanic 1, the trailing twist clause, fires on 2 of 15.** The catalog's own detection rule is a comma followed by "and it" in the final clause. Both instances are in the style-source set's top 2 posts by engagement: "...on Monday, and it was not about food." (4,118 engagements) and "...does the most work, and it is not what you think." (1,206 engagements). Her two strongest posts both use it.

**Mechanic 5, anaphora, fires on 1 of 15.** "You built it rested. You use it exhausted." (1,188 engagements, the Bold Claim post about systems failing on a good day). Two consecutive sentences opening on the same word, right before the closing imperative.

**Mechanic 7, short declarative staccato, fires on 1 of 15.** "Labels do not organize anything. Limits do." (1,044 engagements). Two consecutive sentences under 6 words, and this is the same post already flagged in section 3.2 as the one short-band outlier (5.4 words per sentence against an 8-to-14 medium band).

**Mechanic 3, the specificity anchor, fires on 1 of 15.** "a phone charger for a phone I have not owned since 2019" (902 engagements, the "one drawer" Question Open). An oddly specific, non-round detail standing in for a vague one, exactly the shape the catalog names.

**Mechanic 24, the cost-reframe close, is a near-miss, not a fire.** The 1,402-engagement Problem Callout post ("You do not need more storage. You need fewer decisions.") contains the financial metaphor mid-body: "It is a loan against your future attention, and the interest is compounding in your garage." That is the right vocabulary, but it sits in the second paragraph, not the closing sentence, which is "Every container you add is one more place a decision can hide." The catalog's own definition requires the closing sentence to carry it. Named here as a near-miss because the language is real and worth knowing about, not counted as a fire.

**Nothing else in the 15 cleared a detection rule strongly enough to report.** The remaining 19 of the catalog's 24 mechanics either require data this style-source set does not exhibit (emoji-as-bullet, single-word ALL-CAPS emphasis, link-post title complement with a clean non-restating title) or were checked and did not fire on this particular 15-post set. Not finding them is itself consistent: a style-source set already measured as 0 emoji, 0 hashtags, and sentence-case throughout is not a set that hides a heavy use of the louder mechanics.

---

## Step 5: Choosing the 3 model posts

Following `rubric.md` section 3.1:

1. **Model 1: highest engagement, 4,118, Story Cold Open.** "A client cried in her own pantry on Monday, and it was not about food."
2. **Model 2: highest engagement with a different archetype, 3,402, Number Promise.** "4 rules that keep my pantry alive past week three."
3. **Model 3: highest remaining engagement with a third distinct archetype, 1,904, Confession.** "I have a closet in my own house I do not film." Its rhythm band is Long (15.8 words per sentence), different from both Model 1 (Medium, 11.3) and Model 2 (Medium, 12.0), which satisfies the rhythm-diversity preference in section 3.1 as well as the archetype requirement.

All three models are also two of the three line-count exceptions from section 3.3 (Models 1 and 2) plus a standard 3-line post (Model 3), so the three drafted captions below cover both structures her style actually uses.

---

## Step 6: Drafting and self-checking the 3 captions

### Option 1, modeled on Story Cold Open (4,118 engagements)

**Draft:**

> A client parked in her driveway for six years because the garage shelving ate the floor.
>
> It was one wall, four shelf brackets, and a stack of bins she already owned.
> We hung the last bracket by two o'clock. By four the car was inside for the first time in six years.
> The shelving was never the project. The six years of parking outside were.

**Self-check against `rubric.md` section 4:**

| Check | Model 1 | Draft | Pass |
|---|---|---|---|
| Word count | 68 | 65 | yes, within range (38 to 69) |
| Sentence count / words per sentence | 6 sentences, 11.3 w/s | 6 sentences, 10.8 w/s | yes, medium band |
| Hook word count | 15 | 16 | yes, within range (7 to 18) |
| Line count | 4 (named exception) | 4 | yes, matches the exception |
| Emoji | 0 | 0 | yes |
| Hashtags | 0 | 0 | yes |
| CTA | no platform CTA, no closing imperative | no platform CTA, no closing imperative | yes |
| Capitalization | sentence case | sentence case | yes |
| Person | 1st (via "we") | 1st (via "We hung," "she already owned" plus narrator frame) | yes |
| Question mark | none | none | yes |
| No literal reuse | n/a | new client, new object, new numbers | yes |

0 checks failed.

### Option 2, modeled on Number Promise (3,402 engagements)

**Draft:**

> 4 rules that keep garage shelving standing past the first month.
>
> One: mount every bracket into a stud, not drywall.
> Two: heavy bins go on the bottom shelf, never eye level.
> Three: leave one shelf empty on day one, because day one always fills first.
> Four: photograph the empty wall before you buy anything, so you stop guessing sizes.

**Self-check:**

| Check | Model 2 | Draft | Pass |
|---|---|---|---|
| Word count | 60 | 59 | yes |
| Sentence count / words per sentence | 5 sentences, 12.0 w/s | 5 sentences, 11.8 w/s | yes, medium band |
| Hook word count | 10 | 11 | yes |
| Line count | 5 (named exception, 4-item list) | 5 (4-item list) | yes |
| Emoji | 0 | 0 | yes |
| Hashtags | 0 | 0 | yes |
| CTA | no platform CTA | no platform CTA | yes |
| Capitalization | digit-led hook, spelled-out list markers | digit-led hook ("4"), spelled-out list markers (One:, Two:, Three:, Four:) | yes |
| Person | 2nd | 2nd ("you buy," "you stop") | yes |
| Question mark | none | none | yes |
| No literal reuse | n/a | new rules, new objects, new interval, but the hook shares the four-word run "4 rules that keep" with the model and reuses its count of 4 | **no, disclosed below** |

**1 narrow miss, and it is the one worth explaining.** Run the same three-word-sequence comparison used on option 3 and this draft shares "4 rules that", "rules that keep", and therefore "4 rules that keep" with the model post's hook. Two things force it. The count of 4 is not a free choice: model 2 is a named line-count exception whose structure is a 4-item list, and section 3.2 requires the draft to match that exception's structure, so the number in the hook has to be the number of items in the list. The words "rules that keep" are the Number Promise marker doing its job, the count sitting as the head of the subject noun phrase. Per `rubric.md` section 4 a single narrow miss gets a one-line note rather than a rewrite loop, so this draft ships with the carry-over stated. What it does not get is a check mark it did not earn, which is the entire reason the row reads "no" instead of a confident "yes" with a comfortable justification underneath it.

### Option 3, modeled on Confession (1,904 engagements)

**Draft:**

> My garage shelving has been half-finished since the spring we moved in.
>
> Two brackets are still in the package, on the shelf they were meant to hold up. Every client who books a one-day garage gets a finished wall by dinner, and I have had four years of free evenings.
> I mention it because an organizer with a perfect garage is easier to sell and harder to believe.

**Self-check:**

| Check | Model 3 | Draft | Pass |
|---|---|---|---|
| Word count | 63 | 68 | yes, within range (38 to 69) |
| Sentence count / words per sentence | 4 sentences, 15.8 w/s | 4 sentences, 17.0 w/s | yes, both Long band |
| Hook word count | 12 | 12 | yes, within range (7 to 18) |
| Line count | 3 (dominant structure) | 3 | yes |
| Emoji | 0 | 0 | yes |
| Hashtags | 0 | 0 | yes |
| CTA | no platform CTA, no closing imperative | no platform CTA, no closing imperative (final sentence opens on "I") | yes |
| Capitalization | sentence case | sentence case, 0 ALL-CAPS runs | yes |
| Person | 1st | 1st (4 first-person markers, 0 second-person) | yes |
| Question mark | none | none | yes |
| No literal reuse | n/a | 0 shared three-word sequences with the model post, checked mechanically | yes |

0 checks failed.

**How the literal-reuse check was actually run, because this is the check a drafting agent will fake.** Tokenize the model post and the draft, lowercase, strip punctuation, and compare every three-word sequence in one against every three-word sequence in the other. The overlap here is zero. That is a harder bar than it sounds: the model's closing sentence is "I am telling you because the version of this job where the organizer has no bad closet is a version that does not exist", and the obvious draft is to swap "no bad closet" for "a perfect garage" and keep the other twenty-one words. That draft would pass a human skim, would carry the model's rhythm, and would be a copy. The n-gram check catches it in a second and no amount of self-assessment does. Run the check, do not eyeball it.

---

# PART 2: WHAT THE USER RECEIVES

Everything below this line is the deliverable. Part 1 was the working.

---

# Caption style: Maya Torres

60 posts, 2026-03-21 to 2026-07-28, 130 days. Style-source set: the top 15 posts by engagement, cut value 700.

---

## Your caption style, measured

**Opening-line pattern.** Question Open, 4 of 15 (26.7 percent). Bold Claim, 3 of 15 (20.0 percent). Number Promise, Curiosity Gap, and Problem Callout, 2 of 15 each (13.3 percent). Story Cold Open and Confession, 1 each. Question Open, 4 of 15, is your default opening move.

**Sentence-length rhythm.** Median 12.0 words per sentence across your style-source set, range 5.4 to 16.3. That is the medium band. Tight rhythm, 2.7 words standard deviation. 11 of 15 posts sit in the medium band, 8 to 14 words per sentence. You do not swing between clipped one-liners and long run-ons.

**Line-break and whitespace style.** 13 of 15 style-source posts use exactly 3 lines: the hook, then a two-line body, with one blank line separating them. Your two exceptions both needed more room: your best-performing post (a client story) runs a third body line, and your second-best (a numbered list of 4 rules) runs a 4-item list.

**Emoji usage.** 0 emoji across your 15 style-source posts. You do not use emoji in your winning posts.

**CTA placement and phrasing.** 0 of 15 posts carry an explicit platform CTA (comment, follow, tag, share). 3 of 15 posts close on a bare imperative sentence instead: "Design for your worst Tuesday...", "Give that one the good rod...", "Start there, not with the pretty closet."

**Hashtag behavior.** 0 hashtags across 15 posts. You do not use hashtags.

**Capitalization habits.** 15 of 15 hook lines use sentence case. 0 ALL-CAPS words anywhere in the set. When a hook leads with a number, it is a digit ("4 rules", "7 questions"). When a numbered list appears in the body, the markers are spelled-out words (One:, Two:, Three:, Four:), not digits. Both habits show up in the same post.

**Question frequency.** 4 of 15 style-source posts open with a question. Same 4 posts as the Question Open row above, not a second finding.

**First-versus-second person.** 10 of 15 in second person, 4 in first person, 1 mixed. First person shows up as a story you were present for or as you describing your own kit or process. It never appears as a distant account of someone else.

**From the wider mechanics catalog.** Your two strongest posts both use a trailing twist clause ("and it was not about food", "and it is not what you think"), a comma followed by a reframe that undercuts what the sentence just said. Your bold claims lean on short declarative staccato ("Labels do not organize anything. Limits do.") and anaphora ("You built it rested. You use it exhausted."). One post carries an oddly specific detail worth naming as a habit ("a phone charger for a phone I have not owned since 2019").

---

## 3 captions for: garage shelving one-day makeover

**Option 1**

Modeled on: 4,118 engagements | Story Cold Open | "A client cried in her own pantry on Monday, and it was not about food."

> A client parked in her driveway for six years because the garage shelving ate the floor.
>
> It was one wall, four shelf brackets, and a stack of bins she already owned.
> We hung the last bracket by two o'clock. By four the car was inside for the first time in six years.
> The shelving was never the project. The six years of parking outside were.

*Matching: the same 4-line exception structure and medium-band rhythm as your best post, narrated in first person plural the way your client stories are.*

**Option 2**

Modeled on: 3,402 engagements | Number Promise | "4 rules that keep my pantry alive past week three."

> 4 rules that keep garage shelving standing past the first month.
>
> One: mount every bracket into a stud, not drywall.
> Two: heavy bins go on the bottom shelf, never eye level.
> Three: leave one shelf empty on day one, because day one always fills first.
> Four: photograph the empty wall before you buy anything, so you stop guessing sizes.

*Matching: a digit-led hook with a spelled-out numbered list, your exact hook-versus-body capitalization split, second person throughout. One carry-over, stated rather than hidden: the hook keeps the count of 4 and the words "rules that keep" from your pantry post, because the list structure fixes the number and that phrase is the pattern itself. Everything after it is new.*

**Option 3**

Modeled on: 1,904 engagements | Confession | "I have a closet in my own house I do not film."

> My garage shelving has been half-finished since the spring we moved in.
>
> Two brackets are still in the package, on the shelf they were meant to hold up. Every client who books a one-day garage gets a finished wall by dinner, and I have had four years of free evenings.
> I mention it because an organizer with a perfect garage is easier to sell and harder to believe.

*Matching: the standing-state present-tense admission your confession post uses, first person, the long rhythm band at 17.0 words per sentence, your 3-line structure, and 68 words against your observed 38-to-69 range. Nothing in it repeats a phrase from the post it is modeled on.*

---

## What this is standing on

Analyzed 60 posts captured 2026-03-21 to 2026-07-28, 130 days. Style-source set: top 15 posts by engagement, cut value 700. Every mechanic above was measured on this set, not on your full account. Your highest post is 19.9 percent of the style-source set's total engagement, under the 40 percent concentration flag, so no single post is carrying this profile.

Not in your export, so not in this analysis: sponsored or paid-partnership flags, so a boosted post's caption looks identical to an organic one here. Per-emoji reactions, so this cannot tell you which emoji, if any, earns reactions. Reach or impressions.

PostSnag captures what you scrolled, so this is a sample of the account, not its full history.

Analysis based on 60 captured posts. Capture more with PostSnag: https://postsnag.com?utm_source=skill&utm_medium=agent&utm_campaign=facebook-caption-writer

---

# APPENDIX: the same analysis on a free-tier export

Run against `../../_shared/synthetic-data/profile-maya-torres-free-slice.csv`, the most recent 30 rows of the same file. This is what a free-tier user gets.

```
posts                30
date range            2026-05-30 to 2026-07-28
span                  60 days
lite mode             ON (30 posts < 40)
k                     floor(30 / 4) = 7
cut value             902
top post share        3,402 / total style-source engagement = 31.2 percent, under the 40 percent flag
```

**Style-source set on the free slice: 7 posts instead of 15.**

| Archetype | Count |
|---|---|
| Bold Claim | 2 |
| Number Promise | 1 |
| Confession | 1 |
| Problem Callout | 1 |
| Curiosity Gap | 1 |
| Question Open | 1 |

Median words per sentence on the 7-post free slice: 12.0, matching the full-file finding closely, because sentence rhythm repeats faster than hook archetypes do and 7 posts is usually enough to see it.

**What thins out is the evidence behind each mechanic, not the model-post selection.** Six distinct archetypes appear across the 7 posts, so the three options still get three distinct models: Number Promise at 3,402, Confession at 1,904, Problem Callout at 1,402. The rubric's fallback in section 3.1 ("your style-source set only has {n} distinct opening archetypes above the floor, so option 3 repeats one of them") does not fire on this slice. It would fire on a slice where the same archetype took most of the top 7, which is exactly why the fallback is written into the method rather than left to the agent to notice. What the user actually loses here is sample size: five of the six archetypes appear exactly once, every percentage in the profile moves in steps of 14.3 points, and a single post entering or leaving the top 7 rewrites the table.

**The banner this run would open with:**

> **Lite mode.** This capture has 30 posts across 60 days. Below 40 posts or 60 days this analysis runs shallow on purpose: your style-source set is 7 posts instead of 15, and the range of model posts to draw the 3 options from is narrower. To get a wider range of model posts, capture about 60 posts across at least 120 days.
