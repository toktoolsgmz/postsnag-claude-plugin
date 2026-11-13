# topic-inventory-method.md

The depth asset for Competitor Content Gap Finder. This is the full mechanical procedure both files run through, written so two agents on the same pair of exports produce the same cluster list. `rubric.md` calls this file for the extraction, clustering, and naming steps and does not restate them.

Version 1.0 | 2026-08-04

---

## 0. Why a mechanical procedure and not "read the captions and figure out the topics"

Two agents asked to eyeball 60 captions and "name the topics" will not converge. One calls it "closets," the other calls it "storage spaces." One merges "pantry" and "kitchen," the other keeps them separate. The moment the topic list depends on a reader's taste, the gap table built on top of it is not reproducible, and a skill whose central claim cannot be checked is not worth the download.

This procedure trades a small amount of nuance for full reproducibility. It runs the same way on both files, unattended, and lands on the same clusters every time it is run on the same data. `example-run.md` is the proof: it shows this exact procedure, run as real code, against the two files.

---

## 1. Extraction rules

Run this once per file, independently. Never look at the other file while extracting.

**Step 1: Isolate the text.** For each post, take the `Content` field. Do not include the hook line separately, do not exclude it either. The whole caption is the input.

**Step 2: Normalize.** Lowercase everything. Replace every character that is not a lowercase letter, a digit, an apostrophe, or whitespace with a single space. Split on whitespace. The result is the post's raw word list, in original order.

**Step 3: Filter.** A raw word survives into the candidate pool only if all four of these are true:
- it is not in the STOPWORD list (Appendix A): grammatical connective tissue (articles, pronouns, prepositions, conjunctions, auxiliary verbs, contractions).
- it is not in the FILLER list (Appendix B): generic verbs and abstract nouns that appear in almost any caption regardless of subject (`keep`, `make`, `need`, `thing`, `time`, `day`, `way`, and so on), plus whatever a prior run added there after Section 6 below caught it in the wild.
- it is at least 4 characters long.
- it is not purely digits.

A word that fails any test is dropped. It still exists in the original caption; it is simply not a candidate for a topic label. This is the same "empty is absent, not zero" discipline `references/csv-parse.md` applies to CSV fields, applied to words: a filtered word did not stop meaning something, it stopped being useful as a cluster label.

**Step 4: Stem.** Apply the fixed suffix rule to every surviving word, in this order, first match wins:
```
if len(word) > 5 and word ends "ies":  strip "ies", add "y"
elif len(word) > 5 and word ends "es":  strip "es"
elif len(word) > 4 and word ends "ing": strip "ing"
elif len(word) > 4 and word ends "ed":  strip "ed"
elif len(word) > 4 and word ends "s" and not "ss": strip "s"
else: unchanged
```
This is a suffix-stripper, not a dictionary lemmatizer. It will occasionally produce a stem that is not a real word (`organizing` to `organiz`). That is fine: the stem is a clustering key, never something a reader sees. Every cluster's display name (Section 4) comes from the most common surface form, never the stem.

---

## 2. Candidate terms: unigrams and bigrams

**Unigrams.** Every surviving, stemmed word from Step 4 is a unigram candidate.

**Bigrams.** Walk the ORIGINAL word list (before filtering, in original order). For every adjacent pair of raw words, form a bigram candidate if and only if BOTH words individually survive Step 3's filter. Stem each half and join with a space. This means a bigram only forms between two words that were genuinely next to each other in the sentence, not between two survivors that merely ended up next to each other after unrelated words were filtered out. `coat closet` is a valid bigram because `coat` and `closet` sit next to each other in the caption and both survive. A stopword or filler word sitting between two topic words blocks the bigram; it does not get silently deleted and bridged.

**Per post, per candidate:** record which posts contain it (for document frequency) and the original, unstemmed surface form it came from (for display naming).

---

## 3. Document frequency

For every candidate term (unigram and bigram), count the number of POSTS that contain it at least once. Not the number of occurrences: a word used three times in one caption counts once for that post. This is document frequency (`df`), and it is what gets compared against the floor.

---

## 4. Cluster formation, merge rule, and the floor

**The floor is 5 posts**, reused directly from `references/foundations.md` section 3 (the per-bucket minimum). A topic cluster is not a new kind of number; it is the same "is there enough evidence to call this a thing" question the rest of the catalog already answers with 5. No skill in this catalog invents its own threshold, and this one does not either.

**Step 1: Rank bigram candidates** by `df` descending (ties broken alphabetically). Any bigram with `df >= 5` is a cluster candidate.

**Step 2: The containment merge.** For each qualifying bigram, check both of its component unigrams. If the bigram's `df` is at least 60 percent of a component unigram's own `df`, that component is considered "contained in" the bigram and is absorbed: it does not also become its own separate cluster, because the two are describing the same posts, not two different topics. `df(bigram) >= 0.6 * df(unigram)` is the merge threshold. A component that clears the floor independently AFTER accounting for the bigram (its own occurrences outside the phrase are still frequent enough) keeps its own cluster too. Reasoning: if `closet` appears 10 times and 9 of those are inside the phrase `coat closet`, one cluster (`Coat Closet`) is the honest answer. If `closet` appears 10 times and only 4 are inside `coat closet`, both `Closet` and `Coat Closet` are real, distinct clusters.

**Step 3: Remaining unigrams.** Any unigram not absorbed in Step 2, with `df >= 5`, becomes its own cluster.

**Step 4: Everything else.** Candidates below the floor, whether unigram or bigram, do not form a cluster. They are not reported individually and they are not thrown away silently either: Section 6 (failure modes) below is the check that makes sure nothing that should have cleared the floor was lost to a filtering mistake.

**A post can belong to more than one cluster.** Unlike hook archetypes, topics are not mutually exclusive: a post about a "coat closet system" belongs to both a `Closet` cluster and possibly a `System` cluster if both clear the floor. Composition percentages for topics do not have to sum to 100 percent, and the output says so once rather than implying a clean partition that is not there.

---

## 5. Naming a cluster

**Display name = the most frequent literal (unstemmed) surface form observed for that cluster's key, title-cased.** If `closet`, `closets`, and `Closets` all appear, count each literal string's occurrences separately and title-case the winner. Ties break alphabetically. The reader never sees a stem; they see the plainest, most common way the creator actually wrote the word.

---

## 6. Failure modes, and the tests that catch them

**Failure mode 1: over-clustering on generic language.** The mechanical procedure has no concept of "topic" beyond "a content word that clears the floor." Run without a filler list, it will happily produce clusters named `Open`, `Work`, `Built`, `Failing`, `Nobody`, and `Decision` on a real 60-post organizing-niche file, because those words are common and 4+ characters, but none of them names a subject the posts are about; they are generic verbs and abstract state-words riding along on real topical sentences. This is not hypothetical: it is what the first unfiltered run against `_shared/synthetic-data/profile-maya-torres.csv` actually produced, shown in full in `example-run.md` Step 1.

**The test.** After forming the candidate list, read every cluster name and ask one question: does this name a physical object, a place, a category of thing, or a named activity, or is it a verb, connector, or abstract state-word riding along? Any cluster that fails this test gets added to the FILLER list (Appendix B) and the run repeats. This is the one manually-reviewed step in an otherwise mechanical pipeline, and it only has to happen once per new noise word: FILLER accumulates across runs, so a term flagged once does not have to be re-judged every time this method runs on a new pair of files.

**Failure mode 2: singleton spam.** Without a floor, every proper noun, every one-off product name, every rare word a creator used exactly once becomes its own "cluster" of one post, and the topic table balloons into noise nobody can act on. The 5-post floor is the test: a candidate that never reaches 5 posts containing it is not a cluster, full stop, the same way an archetype used once is not a rankable bucket in `facebook-hook-analyzer`.

**Failure mode 3: double-counting a phrase and its half.** Without the containment merge in Section 4 Step 2, a corpus that says "coat closet" nine times out of ten times it says "closet" produces two clusters that are really one topic counted twice, inflating that topic's apparent share of the corpus. The test: after merging, spot-check the largest two or three clusters by asking whether one is a strict subset of another's posts. If it is and they were not merged, the containment threshold was applied wrong.

**Failure mode 4: a stemming collision that merges two real topics.** The suffix-stripper in Section 1 Step 4 is blunt. It is possible, on a large enough corpus, for two genuinely different words to stem to the same string. This procedure has not hit that case on either shared synthetic file (checked by hand in `example-run.md`), but the test for it is simple: before shipping a cluster's name, glance at 3 of its member captions and confirm they are actually about the same thing. If they are not, split the cluster and note the collision in FILLER's neighboring notes so the next run does not repeat it.

---

## 7. A worked micro-example (illustrative, not from the shared dataset)

Five invented one-line captions, run through the procedure by hand, to show the mechanics on a small case before `example-run.md` runs the real thing at scale:

```
1. "My entryway bench finally has a home for every shoe in this house."
2. "The garage shelf system took one Saturday and it is still holding."
3. "Every entryway needs one bench and nothing else fighting for space."
4. "I built a shelf system for the garage in an afternoon, no drilling."
5. "Stop buying bins for the garage. Build one shelf system instead."
```

**Step 2-3 (normalize, filter), surviving words per post, run for real, not paraphrased:**
```
1. "My entryway bench finally has a home for every shoe in this house."
   raw words that individually survive: entryway, bench, finally, home, shoe, house
   Note: STOPWORD removes "my, has, a, for, every, in, this". Nothing here is in FILLER;
   "finally", "home", "shoe", "house" are real surviving candidates, they are just about
   to fail the floor instead, which is the point (see below).

2. "The garage shelf system took one Saturday and it is still holding."
   STOPWORD removes "the, and, it, is, one". FILLER removes "took, still".
   Survivors: garage, shelf, system, saturday, holding

3. "Every entryway needs one bench and nothing else fighting for space."
   STOPWORD removes "and, for, one". FILLER removes "every, needs, nothing".
   Survivors: entryway, bench, else, fighting, space

4. "I built a shelf system for the garage in an afternoon, no drilling."
   STOPWORD removes "i, a, for, the, in, an, no". FILLER removes "built".
   Survivors: shelf, system, garage, afternoon, drilling

5. "Stop buying bins for the garage. Build one shelf system instead."
   STOPWORD removes "for, the, one". FILLER removes "stop, build".
   Survivors: buying, bins, garage, shelf, system, instead
```

**Document frequency, unigrams (stemmed), run for real:**
```
garage: df=3 (posts 2, 4, 5)
shelf:  df=3 (posts 2, 4, 5)
system: df=3 (posts 2, 4, 5)
entryway: df=2 (posts 1, 3)
bench:    df=2 (posts 1, 3)
everything else, all stemmed (finally, home, shoe, house, saturday, hold, else, fight,
  space, afternoon, drill, buy, bins, instead): df=1, one post each
```

**Document frequency, bigrams (raw-adjacent, both words must survive):**
```
shelf system:   df=3 (posts 2, 4, 5)     <- "shelf" and "system" sit next to each other in all three
entryway bench: df=1 (post 1 only)       <- in post 3, "needs one" sits between them, so no bigram forms there
garage shelf:   df=1 (post 2 only)
bench finally:  df=1 (post 1 only)
buy bins:       df=1 (post 5 only)
system instead: df=1 (post 5 only)
```

**Floor is 5, and this 5-post toy example has no term reaching it, on purpose.** Two things worth reading closely in these numbers:

1. `shelf system` at df=3 is the strongest bigram in the toy set, and it is exactly the kind of phrase Section 4's containment merge exists for: if this micro-example were 20 posts instead of 5 and `shelf system` cleared the floor while lone `shelf` and lone `system` barely exceeded it beyond the phrase, all three would collapse into one `Shelf System` cluster rather than reporting the same posts three times.
2. The df=1 terms (`finally`, `home`, `shoe`, `house`, `saturday`, `holding`, and the rest) are real surviving candidates that were never touched by FILLER. They are excluded by the floor alone, which is Failure Mode 2 doing its job on ordinary one-off words, not a FILLER problem. FILLER exists for a different failure (Failure Mode 1, generic words that are common enough to clear the floor while meaning nothing), and this toy example is too small to demonstrate that one; `example-run.md` Step 1 demonstrates it on the real 60-post file, where FILLER's last two lines earned their place.

The shared synthetic files are 40 and 60 posts, large enough for real clusters to clear the floor, which is what `example-run.md` shows with the actual numbers.

---

## Appendix A: STOPWORD list

```
a an and are as at be been being but by do does did for from had has have he her here
hers him his how i if in into is it its itself just me more most my no nor not now of
off on once only or other our ours out over own same she should so some such than that
the their theirs them then there these they this those through to too under until up
very was we were what when where which while who whom why will with would you your
yours yourself yourselves all any because before below between both cannot could down
each few further having let s t ve ll re m y d o dont doesnt didnt isnt wasnt arent
werent wont wouldnt cant couldnt shouldnt im ive youre theyre weve hes shes whats thats
```

## Appendix B: FILLER list (generic verbs and abstract nouns, not topics)

```
keep keeps kept make makes made get gets got getting need needs needed want wants wanted
know knows knew think thinks thought look looks looked find finds found start starts
started stop stops stopped still even one ones every everyone everything everybody
something anything nothing someone somebody thing things way ways time times day days
week weeks month months year years people person really actually literally exactly also
here there right now today tonight tomorrow yesterday last next first second third own
same new old good great best better worst worse little big small much many lot lots
never always ever again back yours doing done goes went going come comes came
takes took take turn turns turned tell tells told said says say kind sort part parts
around about after until before once twice three four five six seven eight nine ten
open opens opened work works worked working built build builds building fail fails
failed failing nobody somebody decision decisions
```

The last two lines (`open` through `decisions`) were added after Failure Mode 1 fired on the real Maya file. See `example-run.md` Step 1 for the before-and-after.

---

**Version 1.0 | 2026-08-04**
