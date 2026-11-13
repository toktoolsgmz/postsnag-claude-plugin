Condensed reference. The full version lives in the complete-bundle download.

# hook-archetypes.md

The 12 Facebook hook archetypes, their recognition markers, and the precedence ladder that resolves them. Condensed from the facebook-hook-analyzer rubric, sections 1, 2, and 2.13. Classification behavior is unchanged: two agents running this file on the same posts must produce the same table.

Version 1.0 | 2026-08-05

---

## 1. Finding the hook line

The hook is **the first substantive sentence of `Content`**. Not always the first line.

1. Split `Content` on newlines. Drop empty lines.
2. Take the first remaining line and apply the three skip tests below, in order. If a line is skipped, move to the next line and test again. **Stop after 3 skips** and take whatever line you land on.
3. If the line holds multiple sentences, the hook is **the first sentence only**, up to the first terminal punctuation mark. If there is none, the whole line is the hook.
4. Record the hook verbatim, punctuation and capitalization included. Never paraphrase.

**Skip test A, the CTA-first pattern.** Skip the line if it matches any of:
- opens with an imperative aimed at a platform mechanic: `follow`, `comment`, `share this`, `tag a`, `drop a`, `type`, `save this`, `like if`
- contains a bracketed or quoted keyword the reader is told to comment (`comment "TOOLS"`, `type LIST below`)
- is entirely a link, an @ mention, or a hashtag block

**Skip test B, chrome.** Skip the line if it is under 3 words AND is not a complete sentence with a verb. `New post`, `Day 14`, `Part 2`, a lone emoji.

**Skip test C, a leaked label.** Skip lines beginning with an export or drafting artifact: `Copy:`, `Caption:`, `Draft:`, `Post:`.

**Empty caption.** If `Content` is empty or is only chrome after all skips, tag the post `NO CAPTION`. Exclude it from hook classification and from the archetype table, keep it in the engagement corpus, and report both counts ("60 posts analyzed for engagement, 57 for hooks").

**Report the skip counts.** If you skipped CTA lines on 19 of 60 posts, that is a finding in one line: the creator's real hook is buried under a mechanic on a third of their posts.

---

## 2. The 12 archetypes

Every hook gets **exactly one** label. Run the ladder in section 3 top to bottom and take the first match. The qualifiers below ("any one", "needs BOTH", "needs the first two", "needs ALL THREE") are load-bearing; an unqualified marker list classifies the same corpus two ways.

**Question Open (QO).** The hook is a question in form. It hands the reader an open loop by asking rather than asserting. *Markers, any one is sufficient:* ends in a question mark; opens with an interrogative word (`what`, `why`, `how`, `when`, `who`, `which`, `where`) and is a question in form; opens with a modal or auxiliary in inverted order (`do you`, `have you`, `are you`, `did you`, `can you`, `would you`, `is it`). *Example:* `What is the one drawer you would not let a guest open?`

**Bold Claim (BC).** A flat declarative assertion about how the world works, stated without qualification and without evidence in the hook itself. The confidence is the hook. *Markers:* a declarative sentence with a **general subject (a category, a thing, a practice), not `you` and not `I`**; no number quantifying the post's contents, no question mark, no named audience, no narrative event; frequently an `X is not Y` or `X does not Z` construction, or a definitional claim. **This is the catch-all and it sits last on the ladder**, so a hook reaches it by failing everything above it. *Example:* `Labels do not organize anything. Limits do.`

**Curiosity Gap (CG).** Names a specific thing and deliberately withholds its identity. Precise vagueness, not general vagueness. *Markers, needs BOTH:* a definite reference to an unnamed specific (`one shelf`, `the cheapest thing`, `the one question`, `a single change`, `there is one`); and an explicit withholding move (`and it is not what you think`, `it is not X and it is not Y`, `nobody talks about it`, **or the sentence simply ends without naming it**, which satisfies the second marker structurally). *Example:* `The cheapest thing in my organizing kit does the most work, and it is not what you think.`

**Problem Callout (PC).** Names a problem the reader has, in second person, as a diagnosis rather than a complaint. *Markers, needs the first two:* second-person subject (`you`, `your`) in the first clause; a negative state, failure, or unwanted condition attributed to the reader. *Often plus, not required:* an `it is not X, it is Y` reframe of the reader's own situation. *Example:* `Your closet is not messy. It is over capacity.`

**Number Promise (NP).** Leads with a count of what the post will deliver, converting an unbounded read into a bounded one. *Markers, needs ALL THREE:* a cardinal number, digit or spelled out, in the first clause; the number quantifies the post's own contents (things, items, rules, questions, steps, minutes, reasons, mistakes); **the number is the head of the sentence's subject noun phrase**. *Example:* `4 rules that keep my pantry alive past week three.` Subject is `4 rules`.

**Story Cold Open (SC).** Drops the reader into a specific past event with no setup. *Markers, needs the first two:* first-person subject (`I`, `we`) **or a named third party** (a person introduced as a person counts, including `a client`, `my mother in law`, or `she`); a past-tense narrative verb describing a single event, not a habit. *Usually plus, not required:* a specific time, place, or quantity. *Example:* `I opened a client's coat closet last Tuesday and a sled fell on me.`

**Contrarian Take (CT).** Names a prevailing belief and rejects it. *Markers, needs the explicit reference:* an explicit reference to what others believe (`everyone says`, `everyone tells you`, `unpopular opinion`, `conventional wisdom`, `the internet will tell you`, `they tell you`, `contrary to`, `most people think`), followed by a rejection (`is wrong`, `is backwards`, `nobody checks`, `that is not it`). Without that reference it is not this archetype. *Example:* `Everyone tells you to buy the bins first. That is exactly backwards, and it is why you own four empty bins.`

**Direct Address (DA).** Names or conditions on a specific subset of readers before making any claim. *Markers:* the first clause names an audience segment in vocative form (`Renters,`, `New parents,`) or by description (`To everyone still...`, `To the person who...`, `Anyone with a...`); **or** the first clause is a conditional that filters readers (`If you have a bin labeled misc,`). Either form counts, and **the address must come before the claim or the instruction**. *Example:* `Renters, this one changes nothing about your lease.`

**Confession (CF).** A present-tense admission that costs the author authority. *Markers:* first-person subject; present tense or present perfect describing **a standing state, not a past event**; content against the author's own interest or expertise. The tense test is decisive: Confession requires the admission to be true right now. *Example:* `I have a closet in my own house I do not film.`

**Command (CM).** A bare imperative. *Markers:* **the first word of the hook is an imperative verb**, with no subject and no preceding clause; no question mark and no audience filter in front of it. *Example:* `Go empty one drawer. Right now. Set a timer for four minutes.`

**Myth Bust (MB).** Names a specific belief and corrects it as factually false. Contrarian Take rejects advice; Myth Bust corrects a fact. *Markers:* names a specific belief, practice, or product claim as false; marker words (`myth`, `does not work`, `is a lie`, `no, X does not`, `the truth is`, `this is wrong and here is why`); **the correction is checkable in principle, not a matter of taste**. *Example:* `Suction shower caddies do not fail because you bought a cheap one. They fail because the wall is textured.`

**Permission Grant (PG).** Relieves the reader of an obligation or a guilt. The only archetype that lowers the reader's workload in the first line. *Markers:* second person, addressed to the reader; an explicit release (`you are allowed to`, `you do not have to`, `it is okay to`, `nobody is grading`, `nobody has ever`, `you can stop`); the released obligation is named specifically, not in general. *Example:* `You are allowed to keep the ugly thing that works. Nobody is coming to inspect your linen closet.`

---

## 3. The precedence ladder

Run top to bottom, first match wins. Record the label, and record the runner-up in your working notes when a hook matched more than one; the runners-up are useful in the write-up ("6 of your problem callouts are one prefix away from being contrarian takes").

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

**Why Bold Claim is last.** It is the catch-all, and a catch-all anywhere but last swallows the archetypes above it. If Bold Claim comes out as the largest bucket by a wide margin, check that the ladder ran in order before writing a word about it.

**`UNCLASSIFIED`** is the thirteenth outcome, not a thirteenth archetype: a hook that survives the skip tests and matches nothing (a bare fragment, a hashtag pile that skip test A missed, a language you are not reading). Count it in the corpus, exclude it from the ranking, report the count, and if it exceeds 10 percent of posts say so, because at that point the table describes a minority of the file.

---

## 4. Borderline calls: form wins over function

**The governing principle.** When a hook feels like one archetype and is shaped like another, the shape wins. Form is mechanically checkable; function is a judgment two agents will make differently. Note the flavor in your working table if it helps the write-up, but the count goes to the form.

| Confusion | The decisive test | The call |
|---|---|---|
| Question that works by withholding ("Want to know why your system keeps failing by week three?") | Is it a question in form? | Question Open, not Curiosity Gap |
| A confident reframe ("The container store is the last stop, not the first.") | Is there an explicit reference to what everyone believes? | Bold Claim without one, Contrarian Take with one |
| `you`-fronted contrast ("Your pantry looks organized in photos and fails on a Tuesday night.") | Second person plus a named failure? | Problem Callout, every time. Bold Claim's own marker excludes a `you` subject |
| A hook containing numbers ("You are storing three sizes of clothes for three versions of yourself.") | Is the number the head of the subject? | Not Number Promise. Subject is `you`, so Problem Callout |
| First-person admission ("I threw out my own label maker last month.") | Past-tense single event, or present-tense standing state? | Story Cold Open for the event, Confession for the standing state |
| Audience filter ending in an imperative ("To everyone still folding fitted sheets: stop.") | Is the imperative verb the first word? | Direct Address. Command needs the imperative first |
| Audience filter that also releases ("Renters, this one changes nothing about your lease.") | Which mechanism occupies the first clause? | Direct Address. The ladder puts it at 6, above Permission Grant at 9 |
| Forceful `is not` with no checkable fact ("Landlord white is not a personality.") | Could the correction be checked in principle? | Bold Claim. Myth Bust needs something checkable |
| Withholding without an announced tease ("There is one shelf in every kitchen that predicts the whole house.") | Does the sentence end without naming the thing? | Curiosity Gap. Structural withholding satisfies marker two |
