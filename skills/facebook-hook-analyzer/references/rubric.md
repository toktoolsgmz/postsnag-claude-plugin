# rubric.md

The full method for Facebook Hook Analyzer. Written so an agent with no other context can execute it and reach the same numbers as anyone else running it on the same file.

Version 1.0 | 2026-08-04

---

## Section 0: The Triple Hook, adapted to Facebook text posts

The Triple Hook read comes from video analysis: the open fires three channels in parallel (verbal, visual, on-screen text) so that if one misses a viewer, another catches them. Facebook text posts do not have a verbal channel, and the visual channel is not in the export. Adapting it honestly means changing the channels, not pretending the video version applies.

**The three channels on a Facebook post:**

| Channel | Where it comes from | Available? |
|---|---|---|
| **Text hook** | The first substantive line of `Content` | Always. This is the primary channel and most of this rubric. |
| **Structural hook** | The shape of the caption: hook length, total length, paragraphing, punctuation | Always, computed from `Content`. Section 3. |
| **Visual hook** | The image or the video's first frame | **Only if the user supplies screenshots or the media zip.** Section 4. |

**The cross-check, run after all available channels are read:** do the channels attack from distinct angles, or do they say the same thing three times? A post whose hook line asks a question, whose structure is one short line followed by a long body, and whose image shows the answer, has resolved its own curiosity before the reader clicks. That is a specific, fixable failure and you can only see it by reading the channels separately first.

**Discipline, non-negotiable:** quote every hook verbatim from the file, never paraphrase. If a caption is empty, that is `NO CAPTION`, which is a different finding from an unreadable one, and you say which. Never describe an image you were not shown.

---

## Section 1: Extracting the hook line

A wrong number presented with confidence is worse than no number.

The hook is **the first substantive sentence of `Content`**. Not always the first line.

**Procedure:**

1. Split `Content` on newlines. Drop empty lines.
2. Take the first remaining line. Apply the three skip tests below, in order. If a line is skipped, move to the next line and test again. Stop after 3 skips and take whatever line you land on.
3. If the line contains multiple sentences, the hook is **the first sentence only**, up to the first terminal punctuation mark. If there is none, the whole line is the hook.
4. Record the hook verbatim, including its punctuation and capitalization.

**Skip test A: the CTA-first pattern.** Many creators open with their call to action, and if you do not skip it you get an archetype table where 19 of the top 30 hooks are the same sentence.

Skip the line if it matches any of:
- opens with an imperative aimed at the platform mechanic: `follow`, `comment`, `share this`, `tag a`, `drop a`, `type`, `save this`, `like if`
- contains a bracketed or quoted keyword the reader is told to comment (`comment "TOOLS"`, `type LIST below`)
- is entirely a link, an @ mention, or a hashtag block

**Skip test B: chrome.** Skip the line if it is under 3 words AND is not a complete sentence with a verb. `New post`, `Day 14`, `Part 2`, a lone emoji.

**Skip test C: a leaked label.** Skip lines that begin with an export or drafting artifact: `Copy:`, `Caption:`, `Draft:`, `Post:`.

**Empty caption.** If `Content` is empty or is only chrome after all skips, tag the post `NO CAPTION`. It is **excluded from hook classification and from the archetype table**, and it **stays in the engagement corpus** (it happened and it performed). Report both counts in the output: "60 posts analyzed for engagement, 57 for hooks".

**Report the skip counts.** If you skipped CTA lines on 19 of 60 posts, that is a finding in its own right and the output says it in one line, because it means the creator's real hook is buried under a mechanic on a third of their posts.

---

## Section 2: The 12 archetypes

Every hook gets **exactly one** label. Run the precedence ladder in Section 2.13 top to bottom and take the first match. The ladder exists because real hooks match several archetypes at once, and consistency matters more than nuance: two agents running this rubric on the same file must produce the same table.

Each archetype below gives you a definition, recognition markers you can apply mechanically, a strong example, and a borderline case with the call. The borderline cases are the whole point. Anyone can classify a clean example.

---

### 2.1 Question Open (QO)

**Definition.** The hook is a question, in form. It hands the reader an open loop by asking rather than asserting, and the reader answers it in their head before deciding whether to keep reading.

**Recognition markers (any one is sufficient):**
- The hook ends in a question mark.
- The hook opens with an interrogative word (`what`, `why`, `how`, `when`, `who`, `which`, `where`) and is a question in form.
- The hook opens with a modal or auxiliary in inverted order (`do you`, `have you`, `are you`, `did you`, `can you`, `would you`, `is it`).

**Strong example.** `What is the one drawer you would not let a guest open?`

**Borderline case.** `Want to know why your system keeps failing by week three?` This is a question in form and a curiosity gap in function. **Call it Question Open.** Form wins over function throughout this rubric, because form is mechanically checkable and function is a judgment two agents will make differently. Add the sub-note "curiosity-flavored" in your working table if it helps the write-up, but the count goes to QO.

---

### 2.2 Bold Claim (BC)

**Definition.** A flat declarative assertion about how the world works, stated without qualification and without evidence in the hook itself. The confidence is the hook.

**Recognition markers:**
- A declarative sentence with a general subject (a category, a thing, a practice), not `you` or `I`.
- No number quantifying the post's contents, no question mark, no named audience, no narrative event.
- Frequently an `X is not Y` or `X does not Z` construction, or a definitional claim (`X is the last stop, not the first`).

**Strong example.** `Labels do not organize anything. Limits do.`

**Borderline case.** `The container store is the last stop, not the first.` The "not X, it's Y" reframe makes this feel contrarian. **Call it Bold Claim.** Contrarian Take (2.7) requires an explicit reference to a prevailing belief (`everyone says`, `they tell you`, `unpopular opinion`). Without that reference, a reframe is just a confident assertion, and confident assertion is Bold Claim.

---

### 2.3 Curiosity Gap (CG)

**Definition.** The hook names a specific thing and deliberately withholds its identity, so the only way to close the loop is to read on. It is not vagueness, it is precise vagueness: the thing is definite, its identity is not.

**Recognition markers (needs BOTH):**
- A definite reference to an unnamed specific: `one shelf`, `the cheapest thing`, `the one question`, `a single change`, `there is one`.
- An explicit withholding move: `and it is not what you think`, `it is not X and it is not Y`, `nobody talks about it`, or the sentence simply ends without naming it.

**Strong example.** `The cheapest thing in my organizing kit does the most work, and it is not what you think.`

**Borderline case.** `There is one shelf in every kitchen that predicts the whole house.` There is no explicit "not what you think" clause. **Call it Curiosity Gap anyway.** The second marker is satisfied by the sentence ending without naming the shelf. The withholding is structural rather than announced, and withholding is the mechanism.

---

### 2.4 Problem Callout (PC)

**Definition.** The hook names a problem the reader has, in second person, as a diagnosis rather than a complaint. The reader recognizes themselves and feels seen, or caught.

**Recognition markers (needs the first two):**
- Second-person subject (`you`, `your`) in the first clause.
- A negative state, failure, or unwanted condition attributed to the reader.
- Often plus: an `it is not X, it is Y` reframe of the reader's own situation.

**Strong example.** `Your closet is not messy. It is over capacity.`

**Borderline case.** `Your pantry looks organized in photos and fails on a Tuesday night.` This has a contrast structure and could read as a Bold Claim about pantries in general. **Call it Problem Callout.** The subject is `your`, and it names a failure the reader owns. Second person plus a named failure is Problem Callout, every time.

---

### 2.5 Number Promise (NP)

**Definition.** The hook leads with a count of what the post will deliver. It converts an unbounded read into a bounded one, and the reader knows exactly how much of their attention is being asked for.

**Recognition markers (needs ALL THREE, and the third one is what makes this mechanical):**
- A cardinal number, digit or spelled out, in the first clause.
- The number quantifies the post's own contents: things, items, rules, questions, steps, minutes, reasons, mistakes.
- **The number is the head of the sentence's subject noun phrase.**

**Strong example.** `4 rules that keep my pantry alive past week three.` Subject is `4 rules`. All three markers.

**Borderline case.** `You are storing three sizes of clothes for three versions of yourself.` There are two numbers in it. **Not Number Promise.** The subject is `you`, the numbers modify object nouns, and neither one counts anything the post will deliver. This is Problem Callout. The third marker exists specifically to catch this: ask whether the number is the subject, not whether a number is present.

---

### 2.6 Story Cold Open (SC)

**Definition.** The hook drops the reader into a specific past event with no setup, usually first person, usually with a time or place anchor. It works because a scene is harder to scroll past than a claim.

**Recognition markers (needs the first two):**
- First-person subject (`I`, `we`) or a named third party.
- Past-tense narrative verb describing a single event, not a habit.
- Usually plus: a specific time (`last Tuesday`, `on Monday`), a specific place (`in a garage in Reno`), or a specific quantity (`nine hours`).

**Strong example.** `I opened a client's coat closet last Tuesday and a sled fell on me.`

**Borderline case.** `I threw out my own label maker last month.` This is an admission against the author's own professional interest, which is Confession territory. **Call it Story Cold Open.** The distinguishing test is tense and event-hood: Story Cold Open is a past-tense event that happened once; Confession (2.9) is a present-tense standing state. `I threw out` is a past event, so SC. `I have a closet I do not film` is a standing state, so CF.

---

### 2.7 Contrarian Take (CT)

**Definition.** The hook names a prevailing belief and rejects it. The energy comes from the reader either agreeing against the crowd or bracing to argue, and both of those keep them reading.

**Recognition markers (needs the explicit reference, which is what separates this from Bold Claim):**
- An explicit reference to what others believe: `everyone says`, `everyone tells you`, `unpopular opinion`, `conventional wisdom`, `the internet will tell you`, `they tell you`, `contrary to`, `most people think`.
- Followed by a rejection: `is wrong`, `is backwards`, `nobody checks`, `that is not it`.

**Strong example.** `Everyone tells you to buy the bins first. That is exactly backwards, and it is why you own four empty bins.`

**Borderline case.** `Unpopular opinion: most of us do not have a clutter problem, we have a shopping problem with a storage symptom.` The `unpopular opinion:` prefix is doing the work, and the claim after the colon is a Bold Claim on its own. **Call it Contrarian Take.** The prefix is an explicit reference to prevailing belief, which is the marker. Strip the prefix and it becomes Bold Claim, which is a useful thing to point out to a creator: the prefix is a two-word archetype change.

---

### 2.8 Direct Address (DA)

**Definition.** The hook names or conditions on a specific subset of readers before making any claim. Everyone outside the subset scrolls, everyone inside it stops harder than they would for a general hook.

**Recognition markers:**
- The first clause names an audience segment in vocative form (`Renters,`, `New parents,`, `Small kitchen people,`) or addresses them by description (`To everyone still...`, `To the person who...`, `Anyone with a...`).
- Or the first clause is a conditional that filters readers (`If you have a bin labeled misc,`, `If your kid is under five,`).
- The address comes **before** the claim or the instruction.

**Strong example.** `Renters, this one changes nothing about your lease.`

**Borderline case.** `To everyone still folding fitted sheets: stop.` It ends in a bare imperative, which is Command territory. **Call it Direct Address.** Command (2.10) requires the imperative verb to be the **first word** of the hook. Here the first word is `To`, and the address does the filtering before the instruction lands.

---

### 2.9 Confession (CF)

**Definition.** The hook is a present-tense admission that costs the author authority. It works by inversion: the person who is supposed to have this handled says out loud that they do not.

**Recognition markers:**
- First-person subject.
- Present tense or present perfect describing a standing state, not a past event.
- The content is against the author's own interest or expertise: something they still do wrong, still avoid, still have not fixed.

**Strong example.** `I have a closet in my own house I do not film.`

**Borderline case.** `The first house I ever organized, I did everything wrong.` Self-deprecating, first person, admits failure. **Call it Story Cold Open.** Same tense test as 2.6: `I did everything wrong` on `the first house I ever organized` is a past event with a time anchor. Confession requires the admission to be true right now.

---

### 2.10 Command (CM)

**Definition.** The hook is a bare imperative. It skips persuasion entirely and asks for an action, which either lands hard or gets ignored hard. There is rarely a middle.

**Recognition markers:**
- **The first word of the hook is an imperative verb**, with no subject and no preceding clause.
- No question mark, no audience filter in front of it.

**Strong example.** `Go empty one drawer. Right now. Set a timer for four minutes.`

**Borderline case.** `Stop labeling. Start counting.` Two imperatives, and the second one implies a claim about method. **Call it Command.** First word is an imperative verb, no preceding clause, so the marker fires. The fact that a Command carries an implied argument does not move it out of the archetype.

---

### 2.11 Myth Bust (MB)

**Definition.** The hook names a specific belief and corrects it as factually false. Contrarian Take rejects advice; Myth Bust corrects a fact. The difference matters because the two archetypes need different proof in the body.

**Recognition markers:**
- Names a specific belief, practice, or product claim as false.
- Marker words: `myth`, `does not work`, `is a lie`, `no, X does not`, `the truth is`, `this is wrong and here is why`.
- The correction is checkable in principle, not a matter of taste.

**Strong example.** `Suction shower caddies do not fail because you bought a cheap one. They fail because the wall is textured, and no amount of money fixes texture.`

**Borderline case.** `Landlord white is not a personality.` Reads as a myth bust because of the `is not` construction. **Call it Bold Claim.** There is no factual belief being corrected, only an opinion being asserted with force. Myth Bust requires something that could in principle be checked.

---

### 2.12 Permission Grant (PG)

**Definition.** The hook relieves the reader of an obligation or a guilt they are carrying. It is the rarest high-performing archetype because it is the only one that lowers the reader's workload in the first line rather than adding to it.

**Recognition markers:**
- Second person, addressed to the reader.
- An explicit release: `you are allowed to`, `you do not have to`, `it is okay to`, `nobody is grading`, `nobody has ever`, `you can stop`.
- The released obligation is named specifically, not in general.

**Strong example.** `You are allowed to keep the ugly thing that works. Nobody is coming to inspect your linen closet.`

**Borderline case.** `Renters, this one changes nothing about your lease.` This is a release from a worry. **Call it Direct Address.** The audience filter comes first and the release is a consequence, not the hook. When both fire, whichever mechanism occupies the first clause wins, and the ladder in 2.13 enforces that.

---

### 2.13 The precedence ladder

Run top to bottom, first match wins. Record the label and, when a hook matched more than one, record the runner-up in your working notes. The runners-up are useful in the write-up ("6 of your problem callouts are one prefix away from being contrarian takes").

```
 1. Number Promise      (number is the head of the subject noun phrase)
 2. Question Open       (question in form)
 3. Command             (first word is a bare imperative)
 4. Confession          (first person, present tense, admission against interest)
 5. Story Cold Open     (first person or named party, past-tense single event)
 6. Direct Address      (first clause names or filters an audience)
 7. Contrarian Take     (explicit reference to prevailing belief + rejection)
 8. Myth Bust           (names a checkable belief as false)
 9. Permission Grant    (explicit release from a named obligation)
10. Curiosity Gap       (definite unnamed specific + withholding)
11. Problem Callout     (second person + named failure)
12. Bold Claim          (catch-all declarative)
```

**`UNCLASSIFIED`** is the thirteenth outcome, not a thirteenth archetype. Use it when a hook survives the skip tests but matches nothing: a bare fragment, a pure list of hashtags that was not caught by skip test A, a caption in a language you are not reading. Count it in the corpus, exclude it from the ranking, and report the count. If `UNCLASSIFIED` exceeds 10 percent of posts, say so, because at that point the table is describing a minority of the file.

**Why Bold Claim is last.** It is the catch-all, and a catch-all placed anywhere but last swallows archetypes above it. If Bold Claim ever comes out as the largest bucket by a wide margin, check that the ladder ran in order before you write a word about it.

---

## Section 3: The structural hook

The second channel. Computed entirely from `Content`, and almost nobody analyzes it, which is why it is worth the twenty lines it takes.

**What you compute per post:**

| Feature | How | Why it matters |
|---|---|---|
| `hook_chars` | Character count of the extracted hook line | A hook that needs two rendered lines has to survive a fold you cannot predict |
| `caption_chars` | Character count of the whole `Content` field | Length is a promise about the read ahead |
| `hook_is_own_paragraph` | True if a blank line follows the hook | Whether the hook gets to stand alone in the feed |
| `hook_has_question_mark` | True if `?` appears in the hook | Cheap to test, and it cuts across archetypes |
| `caption_has_list` | True if the caption contains a numbered or bulleted structure | Scannability |

**The fold, stated honestly.** Facebook truncates long captions behind a "See more" link. The exact character count varies by surface and changes without notice, so **this skill does not assert one and never tells the user a specific character limit.** What it does instead: report the hook line length and the caption length as measured, and flag any hook over 120 characters as at risk of needing a second rendered line. 120 is a working flag, not a platform fact, and the output says that.

**Bucketing.** Use these fixed buckets so results are comparable across runs:

- `hook_chars`: 0-50, 51-75, 76-100, 101+
- `caption_chars`: 0-250, 251-400, 401+

**Apply the 5-post floor to every structural bucket, same as archetypes.** A bucket with 1 post is reported with its number and explicitly not ranked.

**The no-variance rule.** If a feature has effectively no variance in the capture (for example, every post has the same paragraph structure), do not report it as a finding and do not silently drop it. Write one line: "Every caption in this capture uses the same paragraph structure, so there is no signal here to read." A reader who was told nothing about paragraphing cannot tell whether you checked.

---

## Section 4: The visual hook

**Run this section only if the user supplied screenshots or the media zip. Otherwise omit it and write one line saying why.**

`Media_URLs` in the export are expiring Facebook CDN links. This skill never fetches them, never checks them, and never describes an image it has not been shown. See `references/csv-parse.md` section 5 (condensed; full version in the bundle).

**When images are supplied, read each one on its own before looking at the caption:**

1. **The muted test.** With the caption covered, does the image alone stop a scroll? Answer yes or no and say what does the stopping: a face, a mess, a before-and-after split, a number rendered large, high contrast, a pattern interrupt.
2. **On-screen text.** Quote any burned-in text **verbatim**, or mark it `NONE` or `UNREADABLE`. These are three different findings. A string that is not clearly legible is `UNREADABLE`, never a best guess reported as fact. If you need to read small text, ask the user for a larger crop rather than guessing.
3. **The cross-check.** Compare the visual hook to the text hook. Three outcomes worth naming:
   - **Distinct angles.** The image and the line attack from different directions and cover for each other. This is the target.
   - **Redundant.** The image says what the line says. Nothing is lost, nothing is gained, and one channel is wasted.
   - **Resolved.** The image answers the question the line asked. This is the failure mode, and it is common with curiosity-gap hooks paired with a before-and-after photo. The reader's loop closes in the feed and they never open the post.

**Report visual findings only for the posts whose images you actually saw**, with the count stated. "Read the 6 screenshots you supplied" is a scope. "Your visuals tend to..." across 60 posts you saw 6 of is not.

---

## Section 5: Ranking the archetypes

1. **Compute per archetype:** `n`, median engagement, mean engagement, highest post, and the highest post's hook verbatim.
2. **Split into rankable and unrankable** at `n >= 5` (`references/foundations.md` section 3, condensed; full version in the bundle).
3. **Rank the rankable buckets by median engagement, descending.** Never by mean. Not once.
4. **Compute the mean-based ranking as well, and compare.** If the two rankings differ in the top 3, the output says so explicitly, names the posts responsible, and states that the median ranking is the one being shipped. This is a finding, not a footnote: it tells the user their sense of what works is probably built on their two most memorable posts.
5. **Tie-breaks**, in order, and the output names which one fired:
   1. Higher `n` wins. More evidence beats less at the same median.
   2. Higher share of the top quartile wins.
   3. Higher mean wins.
   4. Alphabetical, and say so, because at that point the tie is real and pretending otherwise is worse than admitting it.
6. **Run the concentration check** (`references/foundations.md` section 4) on every bucket that is about to become a recommendation. Any flag is written inline, next to the number, in the sentence, never as a trailing parenthetical.
7. **Unrankable buckets get their own line** beneath the table, with `n` and median, and are described as untested rather than as bad. An archetype used 4 times that won 4 times is the most actionable thing on the page and it must not be hidden by the floor that correctly refuses to rank it.

**Composition, which is where the actual recommendation comes from.** Performance tells you what worked. Composition tells you what to change on Monday.

- For each archetype: share of the corpus (`n / N`) against share of the top quartile (`count in top k / k`).
- Where those diverge, you have the recommendation. An archetype at 27 percent of the corpus and 7 percent of the top quartile is being over-invested in. One at 7 percent of the corpus and 27 percent of the top quartile is being under-invested in.
- Then the top-10 versus bottom-10 split (`references/foundations.md` section 6, condensed; full version in the bundle), which is the same finding at a harder edge and is usually the sentence the user screenshots.

---

## Section 6: Building the gap list

Five archetypes to test next. Built mechanically, not by taste.

**Tier 2 first: used, winning, and under the floor.**
Archetypes where `1 <= n <= 4` AND median engagement is above the corpus median. These are the strongest candidates in the entire analysis, because there is real evidence and the only thing missing is volume. Order them by median, descending.

**Tier 1 next: never used.**
Archetypes where `n = 0`. No performance evidence exists, so order them by **latent fit**, defined mechanically:

> **The latent-fit test.** Search the **bodies** of the creator's posts (the caption minus the hook line) for each unused archetype's recognition markers. An archetype whose language the creator already writes, but has never once used as an opening line, is the highest-confidence gap in the analysis. They can already write it. They have never led with it.

Order Tier 1 by number of body hits, descending, then by topic fit which you state in one clause.

**Tier 3: reported, never recommended.**
Archetypes where `1 <= n <= 4` AND median is below the corpus median. Say so in one line: "tried twice, landed below your median both times, on too few posts to conclude anything." Do not put these in the five. Do not hide them either.

**Fill the five:** all of Tier 2 in order, then Tier 1 in order, until you have five. If Tier 2 alone exceeds five, take the top five and say how many more there were.

**Label each entry with its tier in the output**, using the words UNDERUSED (Tier 2, evidence exists) and UNEXPLORED (Tier 1, no evidence). Calling all five "unexplored" would be wrong, and it would also force you to skip the archetype with the highest median in the file just because it was used once, which is the opposite of useful.

**Draft one hook per gap**, in the creator's own topics, pulled from `hook-template-library.md` and filled with subject matter taken from their actual posts. Never a generic example. A drafted hook that could belong to anyone proves the skill did not read the file.

---

## Section 7: Converting the top 10 hooks into templates

The top 10 hooks by engagement, in order, each shown twice:

1. **Verbatim**, with its engagement number and its archetype label. Exactly as it appears in the file, no cleanup, no smoothing.
2. **As a fill-in pattern**, with the creator's specifics replaced by braces.

**How to abstract a hook into a pattern without gutting it:**

- Replace nouns specific to one topic with a braced slot: `{object}`, `{room}`, `{audience}`, `{number}`, `{timeframe}`.
- **Keep the structural words.** The negation, the contrast, the sentence rhythm, the punctuation. Those are the pattern. `Your {thing} is not {assumed problem}. It is {real problem}.` is reusable. `Your thing is bad` is not.
- Keep the hook's length band. A 40-character hook abstracted into a 90-character template is a different hook.
- Add a one-line usage note: which archetype it is and what kind of post it opens.

**Sanity check before shipping the templates:** fill each one with a topic from a different niche. If it still reads like a real sentence, the abstraction is right. If it reads like a form, you abstracted too much.

---

## Section 8: What this rubric refuses to do

- **No claim about why a hook worked beyond what the numbers support.** Correlation between an archetype and engagement is what is in the file. Causation is not, and neither is the algorithm.
- **No sponsored-versus-organic split.** The export carries no paid-partnership flag. If a creator's top post was boosted, nothing in the data would show it, and this skill says so once rather than pretending the ranking is clean.
- **No sentiment read.** Comment counts are in the file. Comment text is not.
- **No reach claim.** `Views` exists on video rows only, and views are not reach. No sentence in the output may contain "most-viewed" unless it is scoped to the video rows and stated as such.
- **No superlative that has not been checked literally.** Before writing "your best", "your worst", "the only", or any word ending in "-est", open the ranking and confirm it is literally true, not directionally true. A scoped rank is not a global rank, and a bucket is not a corpus.
