# caption-mechanics-catalog.md

24 Facebook caption mechanics, beyond the 9 this skill measures in every run (`rubric.md` section 2). These are patterns that show up across Facebook creators generally, not specific to any one style profile. Use this catalog to spot something in a user's export that the 9 core mechanics do not name, and to know whether it is worth copying into a generated caption or worth leaving alone.

Original writing for this skill. Every example below is invented to illustrate the mechanic, not lifted from a real creator's post.

Version 1.0 | 2026-08-04

---

## How to use this file

The 9 mechanics in `rubric.md` are the ones this skill measures on every run, because they are cheap to compute and true of almost every caption. This catalog is wider and shallower: mechanics worth naming when you see them, not worth measuring by default on every export. If a style-source set shows a strong instance of one of these, name it in the style profile as an extra finding, using the same "measure it, show the number, say what it means" discipline as the core 9.

Each entry has four parts: what it is, how to detect it in an export mechanically, what a heavy or absent use of it signals, and when a generated caption should copy it versus leave it out.

---

## Hook and open mechanics

### 1. The trailing twist clause

**Definition.** A hook that states a fact, then adds a short clause that reframes or undercuts it: "and it is not what you think," "and it was not about the flour," "which was the whole problem."

**Detect it.** Search hook lines for a comma followed by `and it`, `which is`, or `but not` in the final clause of the sentence.

**Signals.** A creator using this heavily is deliberately building a small curiosity gap into an otherwise plain statement, rather than relying on a full Curiosity Gap archetype hook. It is a lighter-weight version of the same mechanic.

**Copy or skip.** Copy it only when the twist is genuinely surprising given the topic. A twist clause that states the obvious ("and it took a while") reads as a tic, not a hook.

### 2. The direct-quote cold open

**Definition.** The hook is someone else's exact words, in quotation marks, with no attribution in the first line.

**Detect it.** A hook line that opens with a quotation mark and closes one before the sentence ends.

**Signals.** Borrows authority or shock value from a real voice other than the creator's. Works especially well for client-story or customer-story content.

**Copy or skip.** Only usable when the export or the user's own account of the topic includes a real quoted line to draw from. Never invent a quote and present it as something someone actually said; that is a fabrication risk this skill does not take, the same reasoning `references/csv-parse.md` (condensed; full version in the bundle) applies to unverified data.

### 3. The specificity anchor

**Definition.** An oddly precise number or detail standing in for a vague one: "118 hangers" instead of "a lot of hangers," "forty seconds" instead of "a while."

**Detect it.** Numbers in the hook or the first body line that are not round (not 10, 50, 100) and that quantify something the reader would normally estimate loosely.

**Signals.** Precision reads as credibility. A creator who reaches for oddly specific numbers is signaling firsthand, counted experience rather than a generic claim.

**Copy or skip.** Copy the habit, never the number. Generate a plausible, topic-appropriate odd number for the new caption rather than reusing the model post's figure, which is someone else's counted fact, not a reusable constant.

### 4. The rhetorical self-correction

**Definition.** A two-sentence opening where the first sentence states a belief the creator used to hold, and the second reverses it: "I used to think the label maker was the answer. It was not."

**Detect it.** A hook or early body line with a past-tense belief statement followed immediately by a short negation sentence.

**Signals.** A softer cousin of Confession and Myth Bust (see `references/hook-archetypes.md` section 2, condensed; full version in the facebook-hook-analyzer skill or the bundle). Where those archetypes classify the whole hook, this mechanic can show up as a body-level move even when the hook itself is a different archetype.

**Copy or skip.** Copy when the model post's body uses it and the topic supports a believable "I used to think" claim. Skip if it would require inventing a belief the user never expressed; that is putting words in their mouth.

---

## Body and rhythm mechanics

### 5. Anaphora, repeating the sentence starter

**Definition.** Two or more consecutive sentences that open with the same word or phrase: "Count the hangers. Count the mugs. Count the bins."

**Detect it.** Split the body into sentences (the same terminal-punctuation method as `rubric.md` section 2, shared definitions) and check whether 2 or more consecutive sentences share their first word.

**Signals.** A deliberate rhythm device, usually paired with the Command archetype or a numbered-list body. It reads as punchy and memorable, and it is easy to overuse.

**Copy or skip.** Copy at most once per generated caption. A style-source post using it once is a technique; a generated caption using it in every option is a tic that will read as AI-generated rather than creator-matched.

### 6. The comma-spliced run-on

**Definition.** A single sentence joining 3 or more independent clauses with commas rather than periods, building momentum instead of pausing: "We tore out the shelving, we found the sled, she laughed, and that was the whole afternoon."

**Detect it.** Count commas per sentence (using the sentence-splitting rule from `rubric.md`). A sentence with 3 or more commas separating clause-like segments (each with its own subject and verb) is a candidate.

**Signals.** Breathless pacing, usually used at a story's climax or a list's payoff. The opposite of the short declarative staccato in mechanic 7.

**Copy or skip.** Copy only in the sentence position where the model post used it (usually the second-to-last sentence, building to a close), not scattered through the whole draft. This skill's core sentence-rhythm measurement (`rubric.md` section 2.2) already flags whether a style-source set runs tight or loose; a run-on sentence inside an otherwise tight rhythm is a deliberate exception, not a new baseline.

### 7. Short declarative staccato

**Definition.** A run of very short sentences, each under 6 words, stacked back to back: "Labels do not organize anything. Limits do."

**Detect it.** 2 or more consecutive sentences under 6 words each.

**Signals.** Confidence and speed. Common in Bold Claim and Command archetypes. The opposite move from mechanic 6.

**Copy or skip.** Copy when the style-source set's median words-per-sentence (`rubric.md` section 2.2) is already in the short or tight-medium band; forcing staccato onto a set with a long, loose rhythm produces a caption that sounds like a different creator wrote it.

### 8. Self-deprecating aside

**Definition.** A short parenthetical or trailing clause that undercuts the creator's own authority, usually for warmth: "Keep the toaster, I am not a monster."

**Detect it.** A short clause, often after a comma or in parentheses, where the subject is the creator and the content admits a limit, a joke at their own expense, or a concession.

**Signals.** Humanizes an otherwise instructional caption. Common right after a piece of advice that could read as strict or preachy without it.

**Copy or skip.** Copy the placement (right after the strictest instruction in the caption) more than the wording. A generic joke inserted anywhere reads as filler; one placed exactly where the advice needs softening reads as voice.

### 9. Embedded rhetorical question

**Definition.** A question placed mid-body rather than as the hook, often unanswered or answered by the next sentence: "Why does the pantry always fail before the fridge does? Because the fridge has a deadline and the pantry does not."

**Detect it.** A question mark appearing anywhere in the body text (not the hook line, which is covered separately by question frequency in `rubric.md` section 2.8).

**Signals.** A different device from a Question Open hook: this one keeps the reader moving through the body rather than stopping them at the top. Worth naming separately when a style-source set has few Question Open hooks but several mid-body questions, because it means the creator likes the question mechanic even though it rarely leads.

**Copy or skip.** Copy when present in the specific model post being drafted from. Do not add one to every option; it is a body-level choice, not a universal rule.

### 10. Named-object specificity

**Definition.** Naming the exact item instead of its category: "a phone charger for a phone I have not owned since 2019" instead of "an old charger."

**Detect it.** Nouns in the body that are modified by a specific, personal detail (a date, a brand, a relationship) rather than standing alone as a generic category noun.

**Signals.** The single most reliable marker separating a caption that reads as lived experience from one that reads as generic advice. A style-source set heavy on named-object specificity is a set where the generated captions will fail hardest if they revert to generic nouns.

**Copy or skip.** Always copy the habit. Never copy the specific object, brand, or date; invent a new one that fits the user's topic, following the same rule as mechanic 3.

---

## Closing and CTA mechanics

### 11. The callback close

**Definition.** The caption's last line echoes or inverts the hook line's wording: hook is "Your closet is not messy. It is over capacity," close returns to "capacity" or "messy" as its final word.

**Detect it.** Compare the hook line's key nouns against the final sentence's key nouns for an exact or near-exact repeat.

**Signals.** A structural signature, not a content one. It signals a creator who drafts with the ending in mind, which is worth knowing when writing new captions in their voice: the draft should be built end-first, not just opened well.

**Copy or skip.** Copy when the model post uses it; it is one of the easiest high-value mechanics to transfer because it does not depend on the topic's specifics, only on planning the last line before the first.

### 12. The one-line paragraph closer

**Definition.** A final line, alone on its own paragraph, short enough to function as a standalone statement: "That is the actual project."

**Detect it.** The last line in the caption's line structure (`rubric.md` section 2.3) is under 8 words and stands as its own line, not folded into a longer paragraph.

**Signals.** A pacing choice: the creator wants the last thing the reader sees to have room to land. Distinct from the closing-imperative mechanic already measured (`rubric.md` section 2.5), which is about the sentence being a command; this one is about the sentence standing alone regardless of whether it commands anything.

**Copy or skip.** Copy the isolation (put it on its own line) more than force it to be a command if the model post's closer was not one.

### 13. The permission-style release close

**Definition.** A closing line that explicitly lowers the reader's obligation rather than adding to it: "Nobody is coming to inspect your linen closet."

**Detect it.** The final sentence contains a release marker (`allowed to`, `do not have to`, `nobody is`, `it is okay to`) rather than an instruction or a claim.

**Signals.** Same family as the Permission Grant hook archetype (`references/hook-archetypes.md` section 2, condensed; full version in the facebook-hook-analyzer skill or the bundle), but appearing as a closing move under a hook that opened with something else entirely. Worth naming as its own finding when it recurs at the end of captions whose hooks are Problem Callouts or Direct Address, because it shows the creator likes softening a hard opening by the time they close.

**Copy or skip.** Copy when the model post's hook archetype and closing move pair this way. Do not bolt a release close onto a Bold Claim model post that never uses one; that changes the shape of the whole caption.

### 14. The extended, on-topic CTA

**Definition.** A CTA that is a full, specific question about the post's own content, not a generic platform ask: "What is sitting in your entryway right now that does not have a home?" instead of "Comment below!"

**Detect it.** A question in the closing position that references a noun or claim already made earlier in the same caption, as opposed to a content-free platform instruction.

**Signals.** This is functionally a CTA but structurally indistinguishable from an embedded rhetorical question (mechanic 9) placed at the end. The distinction that matters for a generated caption: an extended on-topic CTA is asking for a specific, answerable reply, which tends to earn comments; a generic platform CTA (`rubric.md` section 2.5's explicit-CTA measurement) tends to earn fewer, lower-quality ones.

**Copy or skip.** Prefer this over a generic platform CTA whenever the style-source set has neither, because it is closer to how this creator's winning posts already work: specific, not mechanical.

### 15. The math or arithmetic reveal

**Definition.** A closing move that shows actual numbers doing work: "Ten minutes a day is seventy minutes a week." "About a quarter of what you expected."

**Detect it.** A sentence containing 2 or more numbers connected by an implied or explicit operation (multiplication, a ratio, a before-and-after comparison).

**Signals.** Converts an abstract claim into something the reader can verify themselves, which is a credibility move distinct from the specificity anchor (mechanic 3): that mechanic makes a detail feel real, this one makes a claim feel checkable.

**Copy or skip.** Copy the structure (show the math) with new, topic-appropriate numbers. Never reuse the model post's actual figures; they belong to that post's real claim, not the new topic's invented one.

---

## Formatting and structural mechanics

### 16. The single-sentence hook paragraph

**Definition.** The hook line is isolated on its own paragraph before any body text, with a blank line separating it from everything else.

**Detect it.** Already measured directly by `rubric.md` section 2.3. Listed here because it interacts with several other mechanics on this list (the callback close, the one-line closer) to form a symmetrical caption shape, hook alone at the top, one line alone at the bottom, body in between.

**Signals.** When both the hook-isolation habit and a one-line closer both show up in the same style-source set, the creator is writing to a visual shape, not just a content plan. Worth naming as a combined finding rather than two separate ones.

**Copy or skip.** Always copy if the style profile shows it as dominant (`rubric.md` section 2.3 reports this directly).

### 17. Emoji-as-bullet

**Definition.** Emoji used in place of numbers or dashes to mark list items: a checkmark or arrow at the start of each line in a body list.

**Detect it.** An emoji character (`rubric.md` section 2.4's detection method) appearing at the start of 2 or more consecutive lines, rather than scattered through prose.

**Signals.** A structural use of emoji, different from decorative or emotional emoji use elsewhere in a caption. A style-source set with 0 total emoji (this skill's most common finding on this catalog's synthetic fixture, and a common one on real exports too) by definition has none of this either, and the style profile already states that plainly.

**Copy or skip.** Never introduce this if the measured emoji count is 0. If the style-source set does use emoji this way, match the specific emoji used as a marker, not a random substitute.

### 18. Single-word ALL-CAPS emphasis

**Definition.** One word, and only one, rendered in capitals for emphasis inside an otherwise sentence-case caption: "This is the ONE thing that matters."

**Detect it.** Distinct from the habitual ALL-CAPS check in `rubric.md` section 2.7, which counts every ALL-CAPS word across the set. This mechanic is about a single, deliberate emphasis word appearing rarely, once every several posts, rather than a general capitalization habit.

**Signals.** A rare, high-impact device. If it shows up on exactly one word in one post out of 15, it is a deliberate choice for that specific claim, not a style habit to replicate everywhere.

**Copy or skip.** Copy at most once, on the single most important word in the new caption's strongest sentence, and only if the style-source set shows this exact rare-and-deliberate pattern rather than frequent ALL-CAPS use (which is a different, louder habit `rubric.md` section 2.7 already catches and reports as its own finding).

### 19. The numbered-list body

**Definition.** A body organized as an explicit sequence (One, Two, Three or 1, 2, 3), each item a short, complete instruction.

**Detect it.** Already measured directly by `rubric.md` sections 2.3 and 2.7 (line structure and the numeral-versus-spelled-out habit). Listed here to flag the interaction: a numbered-list body changes the sentence-rhythm math, because each item tends to be short and roughly equal in length, which can pull the whole post's median words-per-sentence down even if the creator's prose posts run longer.

**Signals.** When a style-source set mixes list-format posts and prose posts, report the rhythm separately for each, or the median will describe neither accurately.

**Copy or skip.** Match list-format to list-format, prose to prose. A caption modeled on a numbered-list post should be a numbered-list caption, not a prose caption with the same word count.

---

## Post-type and platform-specific mechanics

### 20. Link-post title complement

**Definition.** On a `link`-type post, the relationship between the caption's `Content` and the `Link_Title` field: does the caption repeat the title, or add something the title does not say?

**Detect it.** Compare the caption's hook line against `Link_Title` for a `link`-type row. Overlap in key nouns means the caption is restating the title; no overlap means the caption is doing separate work (setting up curiosity, adding a personal frame) and the link is the payoff.

**Signals.** A caption that just restates its own link title wastes the caption. A caption that sets up a question the link answers is using the two fields as a single two-part hook.

**Copy or skip.** For a generated caption on a topic that will link out, prefer the complement pattern: write the caption to raise a question or make a claim the linked content resolves, rather than summarizing the link in advance.

### 21. Video engagement-per-view flatness

**Definition.** Not a caption-text mechanic at all, but relevant to what a caption should promise: whether a creator's `Views`-to-engagement ratio is flat or variable across their video posts (`references/foundations.md` section 8, condensed; full version in the bundle).

**Detect it.** Computed from `Views` and engagement on `video`-type rows, not from `Content`.

**Signals.** If the ratio is flat (the synthetic fixture's finding: 1.66 to 2.20 percent across a 20x raw-engagement spread), the caption's job on video posts is to earn the click into the feed, not to change how the video performs once seen, because the video itself is converting viewers at a consistent rate regardless of caption.

**Copy or skip.** Not a copyable text mechanic. Included here because it changes what a video caption should be optimized for: reach into the scroll, not persuasion once stopped. State this as a note when drafting captions for video-type topics, citing `references/foundations.md` section 8 rather than guessing at the algorithm.

### 22. Quoted dialogue insert

**Definition.** A short, quoted line of speech from someone other than the creator, embedded mid-caption rather than as the cold open (compare mechanic 2, which puts the quote first): "She laughed, then she said, 'I forgot that was in there.'"

**Detect it.** A quotation mark pair appearing after the hook line, attributed to a named or described third party.

**Signals.** Grounds a story in a specific, verifiable-feeling moment. Common in Story Cold Open bodies. Distinct from the cold-open quote (mechanic 2) in position and function: this one pays off a story already in motion rather than starting it.

**Copy or skip.** Copy the placement and the brevity (these are almost always under 10 words) with an invented, topic-appropriate line. Never present an invented quote as something a real person said if the caption implies a real client or customer; keep the framing honest about who is speaking, the same discipline `references/csv-parse.md` applies to every other invented detail in a synthetic or hypothetical example.

### 23. The frequency-count opener

**Definition.** A hook or early body line built entirely around how often something happens: "You reorganize the same shelf every three months."

**Detect it.** A time-interval phrase (`every`, `once a`, `twice a`) in the hook or first body line, paired with a habitual action.

**Signals.** A close cousin of Problem Callout (`references/hook-archetypes.md` section 2, condensed; full version in the facebook-hook-analyzer skill or the bundle), narrower in scope: it names a cadence specifically, which makes the diagnosis feel measured rather than vague.

**Copy or skip.** Copy when the topic supports a believable interval. Do not invent a suspiciously precise interval with no basis; a vague "sometimes" beats a fabricated "every 11 days" that reads as manufactured.

### 24. The cost-reframe close

**Definition.** A closing sentence that reframes an action or object in terms of what it costs the reader, rather than what it saves them: "It is a loan against your future attention, and the interest is compounding in your garage."

**Detect it.** A closing sentence using financial vocabulary (`loan`, `interest`, `cost`, `pay`, `rent`) applied metaphorically to a non-financial subject.

**Signals.** A specific rhetorical move that converts an organizing or lifestyle claim into a loss-aversion frame, which tends to land harder than a straightforward benefit statement.

**Copy or skip.** Copy the metaphor family (financial language applied to the topic) rather than the specific words. A metaphor this specific, reused verbatim on a new topic, reads as a mismatched cliche rather than a matched style.

---

## What this catalog will not do for you

**It will not tell you which mechanic to reach for.** That is what the 9 measured mechanics in `rubric.md` are for: they tell you what this specific creator actually does, on this specific export, with numbers attached. This catalog exists for the mechanics that show up strongly enough to be worth naming as an extra finding, and for the moments when a user asks "why does this caption feel off" and the answer is a pattern the 9 core mechanics do not individually cover.

**It will not survive being applied as a checklist to every caption.** A generated caption that hits all 24 of these mechanics at once will read like a mechanic demonstration, not like a person. Most style-source posts use 2 or 3 of these at most, on top of their core archetype and rhythm. Match what the specific model post actually does, not everything this file lists.
