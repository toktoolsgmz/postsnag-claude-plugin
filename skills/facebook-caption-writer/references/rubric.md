# rubric.md

The full method for Facebook Caption Writer. Written so an agent with no other context can execute it and reach the same style profile as anyone else running it on the same file, then write captions that match it.

Version 1.0 | 2026-08-04

---

## Section 0: What this rubric is actually doing

A caption writer that just says "write like this creator" produces a plausible-sounding caption that matches nothing measurable. This rubric splits that vague instruction into 9 mechanics, each with a mechanical measurement, so the style profile the user sees is a set of numbers they can check against their own export, not a vibe.

**Two halves, in order:**

1. **Measure.** Select the style-source posts, then extract all 9 mechanics from them. This produces the style profile.
2. **Generate.** Use the style profile to write 3 new captions per topic, each modeled on one specific source post, then run every draft through the self-check pass before it ships.

Do not skip straight to generation. A caption "in this creator's style" that was not built from a measured profile is a guess wearing a citation.

---

## Section 1: Selecting the style-source posts

A wrong number presented with confidence is worse than no number.

**The style-source set is the top quartile by engagement**, using the identical definition, floor, and tie rule as `references/foundations.md` section 6 (condensed; full version in the bundle):

```
k = floor(N / 4)
```

Sort descending by engagement (reactions plus comments plus shares), take the first `k` posts, report `k` and the engagement value at the cut. Include ties at the boundary and report the real count.

**If `k < 5` (that is, `N < 20`):** do not call it a quartile. Take the top 5 posts and label it "top 5", and only if `N >= 15`. Below 15 posts total, run the qualitative path in section 1.3.

### 1.1 Why the winners, not the whole account

The mechanics of a creator's median post describe what they usually do. The mechanics of their winning posts describe what worked. This skill measures the winners on purpose, because the point is to hand the user a pattern worth repeating, not an average worth ignoring.

### 1.2 The concentration check, applied to a style profile instead of a ranking

`references/foundations.md` section 4 (condensed; full version in the bundle) exists to catch a bucket that is being carried by one outlier post before that bucket becomes a performance claim. A style profile is not a performance claim, but the same failure mode applies in a different shape: if one viral post is 3 of the 15 style-source posts' worth of engagement, its caption habits can dominate the measured mechanics even though it is one post's voice, not the account's.

**Run this check on the style-source set as a whole before measuring anything:**

```
top_share = highest style-source post's engagement / sum of style-source set's engagement
flag if top_share > 0.40
```

If it flags, say so in the style profile in one sentence ("your highest post is {x} percent of this style sample's total engagement, so its mechanics carry extra weight below") and continue. This is a disclosure, not a stop condition: the post still belongs in the sample, because it still won, and the user still gets to see what it did.

### 1.3 Below 15 posts: the qualitative path

Below the 15-post corpus minimum in `references/foundations.md` section 3 (condensed; full version in the bundle), do not compute a style profile from a ranking. Take the posts you have (minimum 5, per the same section), read them directly, and produce the same 9 mechanics as a plain description rather than a measured statistic: "in the 8 posts you gave me, 6 open with a question and none use emoji" instead of a median or a percentage that implies more precision than 8 posts can carry. Say once, plainly, that this is a reading of a small sample, not a measurement.

---

## Section 2: The 9 mechanics

Every mechanic below states what to measure, exactly how to measure it, and how to write it into the style profile. Run all 9 on every post in the style-source set, then aggregate.

**Shared definitions used across this section:**

- **Lines.** Split `Content` on newlines, drop any line that is empty after trimming whitespace. The count of what remains is the line count.
- **Sentences.** Count terminal punctuation marks (`.`, `!`, `?`) in the caption. This is a mechanical proxy, not a grammar parser, and it is deliberately simple so two agents running this rubric on the same file get the same count. A quoted line of dialogue's closing punctuation counts the same as any other sentence's.
- **Words.** Whitespace-delimited token count.
- **Hook line.** The first line of `Content` after dropping empty lines, same extraction as `references/hook-archetypes.md` section 1 (condensed; full version in the facebook-hook-analyzer skill or the bundle). Its CTA and chrome skip tests apply here too, so a CTA-first post's real hook is still what gets measured.

### 2.1 Opening-line pattern

**Measure:** classify each style-source post's hook line into one of the 12 hook archetypes using the precedence ladder in `references/hook-archetypes.md` (condensed; full version in the facebook-hook-analyzer skill or the bundle), which ships locally in this skill's folder so classification runs correctly on a standalone download. That file includes the hook-line extraction procedure and its three skip tests (section 1), all 12 archetype definitions with recognition markers (section 2), the precedence ladder (section 3), and the borderline-call table (section 4). This skill does not redefine the archetypes; two skills in this catalog inventing two different classification systems for the same 60 posts would produce two different answers to "what is your best hook", which is worse than picking one system and citing it.

**Encode:** a table of archetype, count, and share of the style-source set, sorted by count descending. Name the single most common archetype in one sentence as "your default opening move." If two or more archetypes tie for most common, name both.

### 2.2 Sentence-length rhythm

**Measure:** for each style-source post, `word_count` (whitespace tokens across the whole `Content`), `hook_word_count` (whitespace tokens in the hook line), and `words_per_sentence = word_count / sentence_count`. Compute the median of `words_per_sentence` across the set and the range (min to max). Record the min and max of `word_count` and of `hook_word_count` as two separate observed ranges: the self-check in section 4 (items 1 and 3) tests every draft against them, so a run that never computes them cannot complete its own self-check. Bucket every post into one band:

```
Short:  words_per_sentence < 8
Medium: 8 <= words_per_sentence <= 14
Long:   words_per_sentence > 14
```

Compute the population standard deviation of `words_per_sentence` across the set. Flag the rhythm as **tight** if the standard deviation is under 3.0 words, **loose** if 3.0 or above. This 3.0-word threshold is this skill's own working flag, the same kind of stated-not-discovered number as the 120-character hook-fold flag in the hook analyzer. It is not a platform fact and the output says so if asked.

**Encode:** median words per sentence, the band it falls in, the tight-or-loose call with its standard deviation, and the count of posts in each band ("11 of 15 sit in the medium band, 8 to 14 words per sentence").

**Also encode the two observed ranges, as ranges, in the style profile:**

- **Caption word-count range**, min to max across the style-source set. On the synthetic fixture in `example-run.md` this is 38 to 69 words.
- **Hook word-count range**, min to max across the same set. On that fixture it is 7 to 18 words.

Both are observed ranges from this creator's own winning posts, not targets and not platform limits. They exist so that "within range" in section 4 means a checkable number instead of a judgment, and so the user can see the shape of their own captions without opening a spreadsheet.

### 2.3 Line-break and whitespace style

**Measure:** the line count per post (section 2, shared definitions), and where the blank lines fall. On this catalog's exports a caption typically renders as: hook line, one blank line, then the body. Record for each post whether that pattern holds (blank line immediately after the hook line and nowhere else) or whether it deviates (a blank line inside the body, no blank line at all, more than one blank line).

**Encode:** the dominant line count and its share of the set ("13 of 15 style-source posts use exactly 3 lines: the hook, then a two-line body, with one blank line separating them"), then name the exceptions and what makes them different (a numbered list running longer, a fourth body line). Do not average the line count into a decimal; report the dominant value and the spread.

### 2.4 Emoji usage

**Measure:** count emoji characters in each style-source post's `Content` using a Unicode emoji range match. Record the total across the set, and if any are present, which specific emoji recur and where they sit (in the hook line, inside the body, or trailing at the end of the caption).

**Encode:** "{N} emoji across {k} style-source posts." If `N = 0`, say so as plainly as the finding it is: "this creator does not use emoji in her winning posts, and a generated caption should not add one even if it would look natural, because it would not match her." If `N > 0`, name the top emoji by frequency and their typical position.

### 2.5 CTA placement and phrasing

**Measure two different things, because they are two different behaviors:**

1. **Explicit platform-mechanic CTAs**, using the same marker list as the hook analyzer's skip test A (`comment`, `follow`, `share this`, `tag a`, `drop a`, `type`, `save this`, `like if`, a bracketed or quoted comment keyword), searched across the **whole caption**, not just the hook line. Record the count and where they occur when present (opening, mid-body, closing).
2. **The closing-line imperative**, a softer pattern: does the caption's last sentence open with a bare imperative verb aimed at the reader's next action, that is not a platform mechanic ("Start there, not with the pretty closet.", "Organize for Tuesday.")? Test the first word of the final sentence against a list of imperative verbs plausible for the creator's topic. Record the count.

**Encode:** "{N} of {k} posts carry an explicit platform CTA (comment, follow, tag, share)." and separately, "{M} of {k} posts close on a bare imperative sentence, a direct instruction rather than a platform ask." These can both be low. A creator can have zero platform CTAs and still close several posts on a command; that is a real, distinct habit and the profile reports it as its own line.

### 2.6 Hashtag behavior

**Measure:** count `#\w+` matches per style-source post. Record total, whether any hashtag repeats across multiple posts, and typical position (inline within a sentence versus a trailing block after the caption).

**Encode:** total count and, if zero, the plain statement that this creator does not use hashtags. If present, the repeated tags and where they sit.

### 2.7 Capitalization habits

**Measure three things:**

1. **Hook-line case.** Sentence case (only the first word and proper nouns capitalized) versus Title Case versus an ALL-CAPS opening word.
2. **ALL-CAPS words anywhere in the caption**, using a word-boundary match for runs of two or more capital letters, excluding the single-letter word "I". Count them.
3. **Numerals versus spelled-out numbers, in two different places, because they are frequently different habits in the same caption.** Does a hook line that leads with a count use a digit ("4 rules") or a spelled-out word ("Four rules")? Separately, when the body contains a numbered list, are the list markers digits ("1.", "2.") or spelled-out ordinals ("One:", "Two:")? These can and do differ within the same creator's own posts, and reporting them separately is what makes this finding checkable rather than a single vague "uses numbers sometimes."

**Encode:** "sentence case in {N} of {k} hook lines" (or Title Case, or ALL-CAPS, whichever appears), "{N} ALL-CAPS words across the set" (0 is a real and common finding, say so), and the numeral-versus-spelled-out pattern stated as two separate lines if both hook-numerals and body-list-numbers occur anywhere in the set.

### 2.8 Question frequency

**Measure:** count of style-source posts whose hook line contains a question mark, and the share of the set.

**Encode:** "{N} of {k} style-source posts open with a question." **Cross-check against 2.1:** if this count matches the Question Open archetype count exactly, say so in one line and do not present it as a second, independent finding. It is the same 11 posts counted twice, and the output must not imply otherwise (the same confound rule the hook analyzer applies to question marks versus the Question Open archetype).

### 2.9 First-versus-second person

**Measure:** for each style-source post, count first-person markers (`I`, `my`, `me`, `mine`, `we`, `our`, `us`, case-insensitive, word-boundary) and second-person markers (`you`, `your`, `yours`, same matching rules). Classify the post: **1st** if first-person markers outnumber second-person, **2nd** if the reverse, **mixed** if equal (including zero and zero).

**Encode:** the distribution as counts and share ("{N} of {k} in second person, {M} in first person, {X} mixed"). If first person appears, state in one line how it is used: narrating a specific event or admission (a story or a confession, in this catalog's archetype terms) rather than a distant third-person account of someone else. If genuine third-person-about-someone-else captions exist (no `you`, no `I`/`we`, a named or unnamed other party throughout), call that its own category and count it separately; do not fold it into "mixed."

---

## Section 3: Generating 3 captions per topic

Run this once the style profile from section 2 is complete.

### 3.1 Choosing the 3 model posts

Pick 3 style-source posts to model the 3 options on, using this order so the selection is reproducible rather than a feeling:

1. **Model 1: the single highest-engagement style-source post.** The flagship pattern, whatever archetype it is.
2. **Model 2: the highest-engagement style-source post whose archetype differs from Model 1's.** This guarantees the 3 options are not secretly the same pattern three times.
3. **Model 3: the highest-engagement remaining style-source post whose archetype differs from both Model 1 and Model 2, and whose sentence-rhythm band (section 2.2) differs from at least one of the first two if possible.** If every remaining post shares an archetype with Model 1 or Model 2, take the highest-engagement remaining post regardless of archetype and say so in one line ("your style-source set only has 2 distinct opening archetypes above the floor, so option 3 repeats one of them").

**If the style-source set has fewer than 3 posts** (this happens in the qualitative path, section 1.3, on very small captures): write as many labeled options as there are distinct source posts, minimum 1, and say plainly that a wider capture would unlock a third distinct model.

### 3.2 Drafting each caption

For the chosen model post, write a new caption on the user's topic that matches:

- **The same archetype** for the hook line (same recognition markers from `references/hook-archetypes.md` section 2, condensed; full version in the facebook-hook-analyzer skill or the bundle), applied to the new topic, never the model's actual wording.
- **The same sentence-rhythm band** from section 2.2: aim for the style-source median words-per-sentence, within roughly one band width of it.
- **The same line-count structure** from section 2.3, unless the model post was one of the named exceptions, in which case match the exception's structure instead (a numbered-list body stays a numbered-list body).
- **The same emoji and hashtag behavior** from 2.4 and 2.6: if the style-source set uses zero of either, the draft uses zero of either, no exceptions for "it would look nice here."
- **The same CTA behavior** from 2.5: no platform CTA if the source set has none; a closing imperative only if that was part of the specific model post's own pattern.
- **The same capitalization habits** from 2.7: sentence case unless the profile found otherwise, numerals or spelled-out numbers matching whichever role (hook lead versus list marker) the model post used.
- **The same person voice** from 2.9, matching the specific model post, not the set's overall majority, since each option is modeled on one post.

**Never reuse the model post's actual sentences, objects, or numbers.** The pattern transfers, the content does not. A caption that could be mistaken for the model post itself has not been written for the user's topic; it has been copied.

**The 6-word rule, checked literally.** No draft reuses more than 6 consecutive words from any post in the style-source set. Check it literally, sliding a 7-word window across the draft and comparing it against every caption in the set. The archetype and rhythm are the pattern; the nouns are new. (Working number, labeled: 6 is this catalog's threshold, not a platform fact, the same one `facebook-content-calendar-builder` uses for its drafts. It sits just above the length of a common phrase and just below the length of a distinctive clause.)

**The one narrow exception, and it is disclosed, not silent:** when the model post is a named line-count exception (section 2.3) whose structure fixes a specific number (a 4-item list means the draft's hook has to carry the number 4), a short phrase carrying that forced number can survive into the draft. Section 4 item 11's self-check is where this gets caught and disclosed as a single narrow miss, per section 4's rule that a single narrow miss ships with a one-line note rather than triggering a rewrite. This is not a license to skip the check; it is the one situation where the check is expected to catch something structural rather than something sloppy.

### 3.3 Labeling every option

Each of the 3 outputs is labeled, before the caption itself, with:

```
Modeled on: {engagement} engagements | {archetype} | "{model post's hook, verbatim, truncated to about 12 words if long}"
```

so the user can go find the real post that earned the pattern being reused.

---

## Section 4: The self-check pass

Run this on every drafted caption before it ships. It is a checklist, not a vibe check.

For each draft, confirm all of the following against the style profile built in section 2, and against the specific model post's own numbers where noted:

1. **Word count** falls within roughly the style-source set's range (section 2.2's min to max), not just near the median.
2. **Sentence count and words-per-sentence** land in the same rhythm band as the model post specifically, not merely the set's median band.
3. **Hook-line word count** is within the style-source set's observed hook-length range.
4. **Line count and blank-line placement** match the dominant structure from 2.3, or intentionally match the model post's named exception, and the draft is not silently doing a third thing.
5. **Emoji count** matches the profile (0 if the profile found 0).
6. **Hashtag count** matches the profile (0 if the profile found 0).
7. **CTA behavior** matches: no platform-mechanic CTA if the profile found none; a closing imperative present only if the specific model post had one.
8. **Capitalization** matches: sentence case (or whatever the profile found), no stray ALL-CAPS, numerals versus spelled-out numbers assigned to the correct role.
9. **Person voice** matches the model post specifically (1st, 2nd, or mixed).
10. **Question-mark presence** in the hook matches whether the model post's archetype was Question Open.
11. **No literal reuse** of the model post's wording, objects, or numbers, checked with the 6-word rule from section 3.2: no run of more than 6 consecutive words repeated verbatim from any style-source post; the topic is the user's, the pattern is the model's.

**If a draft fails 2 or more checks, rewrite it before it ships.** A single narrow miss (the word count is 4 words over the observed range) is worth a one-line note in the output rather than a rewrite loop; 2 or more misses means the draft is not actually modeled on the post it claims to be modeled on, and shipping it anyway would be the exact failure this rubric exists to prevent.
