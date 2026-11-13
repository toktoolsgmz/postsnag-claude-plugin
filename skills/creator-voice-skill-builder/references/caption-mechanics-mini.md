Condensed reference. The full version lives in the complete-bundle download.

# caption-mechanics-mini.md

The 9 caption mechanics with their measurement rules, plus the 11-item draft self-check. Condensed from the facebook-caption-writer rubric, sections 2 and 4. "Write like this creator" is a guess; these 9 numbers are checkable against the user's own export.

Version 1.0 | 2026-08-05

---

**Shared definitions.** **Lines:** split `Content` on newlines, drop lines empty after trimming; the count of what remains is the line count. **Sentences:** count terminal punctuation marks (`.`, `!`, `?`); a mechanical proxy, deliberately simple so two agents get the same count. **Words:** whitespace-delimited tokens. **Hook line:** the first line after dropping empties, extracted with the CTA and chrome skip tests in `hook-archetypes.md` section 1, so a CTA-first post's real hook is what gets measured.

Run all 9 on every post in the style-source set (the top quartile by engagement), then aggregate.

---

**1. Opening-line pattern.** *Measure:* classify each style-source hook into one of the 12 archetypes using the precedence ladder in `hook-archetypes.md`. Do not invent a second classification system. *Encode:* a table of archetype, count, and share of the set, sorted by count descending. Name the most common one as "your default opening move", and name both if two tie.

**2. Sentence-length rhythm.** *Measure:* per post, `word_count` (tokens across the whole `Content`), `hook_word_count` (tokens in the hook line), and `words_per_sentence = word_count / sentence_count`. Compute the median of `words_per_sentence` and its min-to-max range. Band every post: **Short** under 8, **Medium** 8 to 14, **Long** above 14. Compute the population standard deviation of `words_per_sentence`: rhythm is **tight** under 3.0 words, **loose** at 3.0 or above. The 3.0 threshold is this skill's stated working flag, not a platform fact. *Encode:* the median, its band, the tight-or-loose call with its standard deviation, and the count per band ("11 of 15 sit in the medium band"). **Encode two observed ranges as ranges, because the self-check tests every draft against them and a run that skips them cannot finish its own self-check:** the **caption word-count range** (min to max across the set) and the **hook word-count range** (min to max across the same set). Both are observed ranges from this creator's winning posts, not targets and not platform limits.

**3. Line-break and whitespace style.** *Measure:* the line count per post and where the blank lines fall. Record for each post whether the dominant pattern holds (a blank line immediately after the hook and nowhere else) or deviates (a blank line inside the body, none at all, more than one). *Encode:* the dominant line count and its share ("13 of 15 use exactly 3 lines"), then name the exceptions and what makes them different. Do not average line count into a decimal; report the dominant value and the spread.

**4. Emoji usage.** *Measure:* count emoji characters per post with a Unicode emoji range match. Record the total, and if any are present, which recur and where they sit (hook line, inside the body, trailing). *Encode:* "{N} emoji across {k} posts." If N = 0, say it plainly: this creator does not use emoji in her winning posts, and a generated caption does not add one even if it would look natural, because it would not match her.

**5. CTA placement and phrasing, two different behaviors.** *Measure:* (a) **explicit platform-mechanic CTAs** using the skip-test A marker list (`comment`, `follow`, `share this`, `tag a`, `drop a`, `type`, `save this`, `like if`, a bracketed or quoted comment keyword), searched across the **whole caption**, not just the hook; record count and position. (b) **The closing-line imperative:** does the last sentence open with a bare imperative aimed at the reader's next action that is not a platform mechanic ("Start there, not with the pretty closet.")? Test the first word of the final sentence against imperative verbs plausible for the topic; record the count. *Encode:* both as separate lines. A creator can have zero platform CTAs and still close several posts on a command, and that is a real, distinct habit.

**6. Hashtag behavior.** *Measure:* count `#\w+` matches per post; record the total, whether any tag repeats across posts, and typical position (inline versus a trailing block). *Encode:* the total, and if zero, the plain statement that this creator does not use hashtags.

**7. Capitalization habits, three things.** *Measure:* (a) **hook-line case**, sentence case versus Title Case versus an ALL-CAPS opening word; (b) **ALL-CAPS words anywhere**, word-boundary match on runs of two or more capitals, excluding the single-letter "I", counted; (c) **numerals versus spelled-out numbers in two places**, because they are frequently different habits in the same caption: does a hook leading with a count use a digit ("4 rules") or a word ("Four rules"), and separately, are body list markers digits ("1.", "2.") or spelled-out ordinals ("One:", "Two:")? *Encode:* "sentence case in {N} of {k} hook lines", "{N} ALL-CAPS words across the set" (0 is a real finding, say so), and the numeral pattern as two separate lines when both roles occur.

**8. Question frequency.** *Measure:* count of style-source posts whose hook line contains a question mark, and the share. *Encode:* "{N} of {k} open with a question." **Cross-check against mechanic 1:** if the count matches the Question Open archetype count exactly, say so in one line and do not present it as a second independent finding. It is the same posts counted twice.

**9. First versus second person.** *Measure:* per post, count first-person markers (`I`, `my`, `me`, `mine`, `we`, `our`, `us`, case-insensitive, word-boundary) and second-person markers (`you`, `your`, `yours`). Classify: **1st** if first-person outnumbers second, **2nd** if the reverse, **mixed** if equal (including zero and zero). *Encode:* the distribution as counts and share. If first person appears, state in one line how it is used (narrating a specific event or an admission, rather than a distant account of someone else). Genuine third-person-about-someone-else captions get their own category and count, never folded into "mixed".

---

## The self-check pass, 11 items

Run this on every drafted caption before it ships. It is a checklist, not a vibe check. Confirm each against the style profile above, and against the specific model post's own numbers where noted.

1. **Word count** falls within the style-source set's observed range (mechanic 2), not just near the median.
2. **Sentence count and words-per-sentence** land in the same rhythm band as the model post specifically, not merely the set's median band.
3. **Hook-line word count** is within the observed hook-length range.
4. **Line count and blank-line placement** match the dominant structure, or intentionally match the model post's named exception, and the draft is not silently doing a third thing.
5. **Emoji count** matches the profile (0 if the profile found 0).
6. **Hashtag count** matches the profile (0 if the profile found 0).
7. **CTA behavior** matches: no platform-mechanic CTA if the profile found none; a closing imperative only if the specific model post had one.
8. **Capitalization** matches: sentence case or whatever the profile found, no stray ALL-CAPS, numerals versus spelled-out numbers assigned to the correct role.
9. **Person voice** matches the model post specifically (1st, 2nd, or mixed).
10. **Question-mark presence** in the hook matches whether the model was a Question Open.
11. **No literal reuse** of the model post's wording, objects, or numbers. The topic is the user's, the pattern is the model's.

**Two or more misses means rewrite before shipping:** the draft is not actually modeled on the post it claims to be modeled on. **A single narrow miss** (the word count is 4 words over the observed range) is worth a one-line disclosure in the output rather than a rewrite loop.
