# rubric.md

The full method for Facebook Group Post Analyzer. Written so an agent with no other context can execute it and reach the same numbers as anyone else running it on the same file.

Version 1.0 | 2026-08-04

---

## Section 0: Why a group export needs its own skill, not a scoped-down profile skill

A profile tells you what works for one voice, posting alone, over time. A group is a shared room: many authors, a set of norms nobody wrote down, and a real cost to breaking one, which is being ignored. `facebook-hook-analyzer` and `facebook-profile-audit` answer "what works for me." This skill answers a different question: "what does this room reward, regardless of who is posting." That is why the unit of analysis here is the post type and the norm, not the hook archetype, and why the `Author` column, which the profile export does not even have, is one of this skill's four analysis surfaces instead of an afterthought.

---

## Section 1: Detecting a group export

Compute every number in this analysis with code.

Read the header row before anything else.

```
Group export headers   : Author, Username, Posted, Type, Reactions, Comments, Shares, Content, Post URL
Profile export headers : Posted, Type, Reactions, Comments, Shares, Views, Duration_Sec, Content, Post_URL, Media_URLs, Link_Title, Link_URL
```

**The mechanical test:** does an `Author` column exist? Yes, group export, proceed. No, profile export, stop.

A second confirming signal, checked only if the first is ambiguous: the permalink column is named `Post URL` with a space in a group export and `Post_URL` with an underscore in a profile export. Never rely on column position, only on the header name, per `references/csv-parse.md` section 1.

**If the file fails the test, do not run any part of this rubric on it.** Say plainly: "This file has no `Author` column, which means it is a profile export. This skill needs a group export, the one you get from capturing a Facebook group instead of a profile page. Recapture the group and try again." Half-running the profile analysis on a group file, or vice versa, produces numbers that look plausible and describe nothing real.

---

## Section 2: Ranking the real post types

**The type values that exist, and no others:** `text`, `photo`, `video`, `link`, `album`. There is no poll type anywhere in a PostSnag export. If a value outside this set appears, treat it as `UNCLASSIFIED`, count it, and exclude it from the ranking.

1. Group every post by its `Type` value.
2. Compute `n`, median engagement, mean engagement, and the top post per type.
3. Split into rankable (`n >= 5`) and unrankable (`n < 5`), per `references/foundations.md` section 3.
4. **Run the concentration check on every rankable type** before it becomes a recommendation: median after deleting the top post, the top post's share of the type's total engagement, mean over median. `references/foundations.md` section 4. Any flag is written inline next to the number.
5. Rank the rankable types by median engagement, descending. Compute the mean-based ranking too, and if the two orders disagree, say so and name the posts responsible, same as every other skill in this catalog.
6. **Unrankable types are listed, not deleted**, with their `n` and median, and called "too small to rank, worth testing." A type with the single highest median in the whole capture but too few posts to rank is the most actionable line on the page, the same finding `facebook-hook-analyzer` protects for hook archetypes.
7. **Check for overlap between a low-performing type and the promo-marker bucket (Section 3.3) before writing anything about that type.** If most or all of a type's posts are also promo-marked, the type's low median is a promo finding wearing a format costume, not a format finding. Say which one it actually is.

**Worked on the shared synthetic file, `group-declutter-community.csv` (25 posts):**

| Type | n | Median | Mean | Rankable? | Concentration flags |
|---|---|---|---|---|---|
| photo | 8 | 164.5 | 226.4 | yes | none |
| text | 11 | 133 | 254.3 | yes | divergence (mean/median 1.91) |
| video | 3 | 228 | 270.3 | no | too small to rank |
| album | 1 | 144 | 144 | no | too small to rank |
| link | 2 | 12.0 | 12.0 | no | too small to rank |

Ranked by median, photo beats text. Ranked by mean, text (254.3) beats photo (226.4), because two of text's 11 posts (609 and 621 engagement, both from the same author, see Section 4) pull the average up without moving the median much. The median ranking ships.

**The overlap check fires here.** Both of the group's 2 link posts are also flagged by the promo-marker heuristic in Section 3.3. Link's low median (12.0) is not evidence that link posts underperform in this group; it is evidence that these two specific promotional posts underperformed, and they happen to both be links. A group with more, non-promotional link posts could easily rank differently. State it exactly that way.

---

## Section 3: Extracting group norms

Three norms, each measured mechanically. None of these are eyeballed or inferred from a general sense of the posts; each has a formula.

### 3.1 Length norms

1. Compute `word_count = len(Content.split())` for every post with non-empty content.
2. Report the median word count across the whole capture.
3. Bucket into three fixed bands so results are comparable across runs: **0-19 words, 20-29 words, 30+ words.** These bands are a working definition sized for the volume a typical group capture carries, not a platform fact, and the rubric says so.
4. Compute `n`, median, and (for rankable bands) the concentration check, same as any other bucket.
5. **Before calling a length band a norm, check who is in it.** If a band's clean result is carried mostly by the same 1 or 2 recurring authors identified in Section 4, say so, because "long posts win" and "this group's two most consistent posters happen to write long posts" are different claims and only one of them transfers to a stranger's post.

**Worked on the synthetic file:**

| Band | n | Median | Mean | Rankable? | Median after deleting top | Top post's share | Mean/median | Flags |
|---|---|---|---|---|---|---|---|---|
| 0-19 words | 4 | 92 | 95.8 | no | not checked, below floor | not checked | not checked | too small to rank |
| 20-29 words | 15 | 133 | 200.1 | yes | -1.5% | 20.7% | 1.50 | divergence |
| 30+ words | 6 | 423.0 | 367.0 | yes | -12.8% | 27.7% | 0.87 | none |

Median word count across the capture: 23.

The 30+ band is the strongest clean signal in the length read: over 3 times the 20-29 band's median, and it clears the floor with zero concentration flags. The author check in Section 4 applies here directly: 4 of the 6 posts in the 30+ band belong to the two recurring high performers. The other 2 (105 and 159 engagement) sit far below the band's median of 423. Reported honestly, this is "long posts do well in this group, and they do especially well when a proven author writes one," not a clean length-only effect.

### 3.2 Tone

Two mechanical markers, each checked with the concentration check before being called a norm.

**First-person share.** A post counts as first-person if it contains, anywhere in `Content`, a case-insensitive whole-word match for any of: `I`, `I'm`, `I've`, `I'll`, `my`, `me`, `we`, `we're`, `we've`, `our`. This is a presence test across the whole post, not just the opening line, because tone is a property of the voice, not the hook.

**Question share.** A post counts as a question post if `Content` contains a `?` anywhere.

**Worked on the synthetic file:**

| Marker | n | Share of corpus | Median | Rankable? | Median after deleting top | Top post's share | Mean/median | Flags |
|---|---|---|---|---|---|---|---|---|
| First-person present | 19 | 76.0% | 159 | yes | -8.2% | 13.0% | 1.58 | divergence |
| Not first-person | 6 | 24.0% | 128.0 | yes | -12.5% | 28.1% | 1.06 | none |
| Contains a question mark | 5 | 20.0% | 133 | yes (n=5) | -11.7% | 40.9% | 2.29 | **top-share and divergence: two flags, excluded from recommendation** |
| No question mark | 20 | 80.0% | 151.5 | yes | -5.0% | 11.9% | 1.34 | none |

**First-person is a real norm here, and both sides of the comparison clear the floor.** 76 percent of the capture is first-person, at a median of 159, against 128 for the 24 percent that is not, a clean 1.24x gap between two rankable buckets. The first-person bucket carries one concentration flag (divergence), so glue that caveat to its number. The not-first-person bucket comes back clean on all three parts of the concentration check (mean/median 1.06, top post 28.1 percent of the bucket, median moves 12.5 percent if the top post is removed), so its side of the comparison needs no caveat at all. Report this as a checked finding, not a directional one: this group's first-person posts genuinely out-earn its non-first-person posts.

**Question marks are not a norm here, and this is exactly the kind of finding a shallow read would get backwards.** The question-mark bucket technically clears the 5-post floor at n=5, but it fires two concentration flags, which per `references/foundations.md` section 4 means it does not become a recommendation. Two of its five posts, both from the same recurring author (Section 4), are also the group's two highest-engagement posts overall, and they are carrying the whole bucket. Meanwhile the no-question-mark bucket, at n=20, is clean and its median (151.5) is actually higher than the question bucket's (133). The honest read: this group does not reward questions as a device. It rewards one author who happens to ask them.

### 3.3 Promo tolerance

**The problem stated honestly.** PostSnag captures no sponsored, paid-partnership, or promotional flag anywhere in any export. There is no field to check. The only way to find promotional posts is to read the language, which means this section is a heuristic, and it says so before it says anything else.

**The marker list, checked case-insensitively anywhere in `Content`:**

```
affiliate, % off, percent off, discount, link in my profile, link in bio,
dm me, spots open, book a, discovery call, virtual organizing service,
my service, rates
```

A post is promo-marked if any one marker matches. This is a working list tuned to the kind of self-promotion that shows up in interest-based groups (a service pitch, a discount code, an affiliate link, a booking call to action), not an exhaustive taxonomy.

**The false-positive risk, stated plainly.** This heuristic will miss promotional posts that avoid all of the listed language entirely, for example a post that only says "check my profile" with no other marker, or a soft pitch with no call to action at all. It can also flag a genuine, non-promotional post that happens to contain one of the phrases for an unrelated reason, for example a member asking "does anyone know a good service for X" is not selling anything but could match "service" in a looser list. Read the flagged posts before treating the list as a verdict; it is a starting point for a human read, not a classifier with guaranteed accuracy.

**Measurement:** compute `n`, median, and the concentration check for the promo-marked bucket, and compare its median against both the whole-group median and the non-promo median.

**Worked on the synthetic file:**

| Bucket | n | Share of corpus | Median | Rankable? | Median after deleting top | Top post's share | Mean/median | Flags |
|---|---|---|---|---|---|---|---|---|
| Promo-marked | 3 | 12.0% | 14 | no (n=3) | not checked, below floor | not checked | not checked | too small to rank |
| Not promo-marked | 22 | 88.0% | 164.5 | yes | -3.3% | 11.2% | 1.53 | divergence |
| Whole group | 25 | 100% | 144 | n/a | n/a | n/a | n/a | n/a |

The promo-marked bucket is below the 5-post floor, so it is never given a rank, but 3 posts at a median of 14 against a group median of 144, an 11-times gap, is not a subtle signal. Report it as "too small to rank, worth testing" per the standard floor language, and let the number do the talking: this group's promotional posts have performed far below its median, on the evidence available. That is a directional finding, stated as one, not a rule.

---

## Section 4: Recurring high performers via the `Author` column

The group export carries `Author` and `Username`. The profile export has neither. This is the one analysis in the whole catalog this skill can run that no profile-scoped skill can.

**The rule: 3 or more posts by the same author before naming any pattern.** Two posts from one person is a coincidence you cannot yet distinguish from two lucky posts. Three is where a real repeated behavior starts to be visible.

1. Group all posts by `Author`.
2. For every author with `n >= 3`: compute median engagement, mean engagement, and the concentration check.
3. Describe what their posts mechanically share: post type mix, presence in the length bands from 3.1, presence of first-person or question markers from 3.2, and any structural repeat (a recurring thread format, a recurring opening phrase, a recurring reference to a past post).
4. **Anonymize.** In every output, refer to qualifying authors as Author A, Author B, Author C, in descending order of median engagement. Never print a real name from the export into the skill's output. This is a one-sentence courtesy: a report someone pastes into a chat or a deck should not carry a stranger's name without their say. This rule covers working notes too, not just the final deliverable: any draft, example run, or intermediate analysis that gets saved or shown anonymizes exactly the same way, with the same letters, start to finish.

**Worked on the synthetic file. Two authors clear the 3-post floor:**

| | n | Median | Mean | Median after deleting top | Top post's share | Mean/median | Flags | Type mix | Length band | Tone |
|---|---|---|---|---|---|---|---|---|---|---|
| Author A | 3 | 609 | 569.0 | -10.8% | 36.4% | 0.93 | none | text, photo, text | 2 of 3 in 30+ words | first-person in all 3, question mark in 2 of 3 |
| Author B | 3 | 460 | 437.3 | -9.9% | 36.8% | 0.95 | none | photo, video, text | 2 of 3 in 30+ words | first-person in all 3, question mark in 0 of 3 |

Both authors clear the floor clean, no concentration flags, which means neither is a one-hit wonder padding a small sample. Both sit well above the group median of 144.

**Author A's mechanical pattern:** all 3 posts open as a direct, structured question to the group ("What is the one zone you are attacking this week?", "Who did the thing they said they would do?") and explicitly grant permission for an incomplete answer ("No judgment thread", "'I did not' is a complete and welcome answer"). This is a repeated thread format, not three unrelated posts that happened to ask something. It is also the entire explanation for the question-mark bucket's inflated appearance in Section 3.2: Author A supplies 2 of the group's 5 question-mark posts, and both are Author A's two highest-engagement posts.

**Author B's mechanical pattern:** all 3 posts reference a prior post or prior group advice before showing a result ("after the closet post", "the thing everyone here told me to do"), and are written as first-person before-and-after narratives with a concrete count in the close (bags out, minutes taken). This is a callback-and-result structure, distinct from Author A's open-ended-question structure, and both patterns outperform the group median without overlapping in mechanism.

**What this section does not claim.** Two authors with 3 posts each is 6 of 25 posts, not a majority, and the pattern each one runs is specific to that person's format. This section names what works for the people who have already proven it works, so a newcomer can borrow the mechanism (open with a direct, low-stakes question; or callback to prior advice with a concrete result), not the identity.

---

## Section 5: Day-of-week responsiveness, reused from `best-time-to-post-reader`

**This skill does not re-derive a bucketing system that already exists.** `best-time-to-post-reader` defines the day-of-week and day-by-time-band method, its floors, its concentration check, and its format-confound check, in full, at `../best-time-to-post-reader/references/rubric.md`. This section names what this skill reuses, what it deliberately does not, and gives a condensed table so an agent does not have to open the other file to run the day-of-week layer correctly.

**What this skill reuses, verbatim:**

- The 5-post-per-bucket floor (`references/foundations.md` section 3).
- The concentration check (`references/foundations.md` section 4), run on every rankable day.
- The format-confound check (`best-time-to-post-reader/references/rubric.md` section 5): for a rankable day, and for every `Type` present in it, `rep_ratio = type_share_bucket / type_share_corpus` and `type_median_ratio = type_median_corpus / corpus_median`. Flag if `rep_ratio >= 1.5 AND type_median_ratio >= 1.2`. Every ranked day reports one of exactly three confound states: the named confound, **"checked, no confound"**, or **"not checked"**. Never "none," for the same reason `best-time-to-post-reader` never uses it: "none" reads as clean whether or not the check ran.

**What this skill does NOT reuse, on purpose:** the time-of-day bands and the day-by-time-band layer. `best-time-to-post-reader`'s own worked examples show only 1 of 28 day-by-time cells clearing the floor on a 30-post free-tier slice, and a group capture is typically thinner than a single profile's export because it is split across many authors' posting habits rather than one person's. Running the day-by-time layer on a group export would produce a grid that is almost entirely "n<5" and calling that a section would be padding, not analysis. **Groups get day-of-week only, and this skill says so in one sentence in the output** rather than shipping an empty grid.

**Timezone caveat.** `Posted`'s timezone is not stated anywhere in the export, so a day-of-week bucket can shift by one calendar day for posts made near midnight in the poster's own timezone. Report day-of-week as a relative finding ("Wednesday out-earns the rest of the week"), never as clock-time advice, and say once that the split assumes the timestamps are read as captured, not corrected for any single author's timezone.

**Worked on the synthetic file (25 posts, span 43 days, lite mode ON):**

| Day | n | Median | Mean | Rankable? | Concentration flags | Format-confound |
|---|---|---|---|---|---|---|
| Wednesday | 6 | 326.0 | 342.3 | yes | none | **video flagged: rep_ratio 2.78, type_median_ratio 1.58** |
| Monday | 4 | 151.5 | 149.0 | no | too small to rank | not checked |
| Saturday | 4 | 78.5 | 197.0 | no | too small to rank | not checked |
| Friday | 4 | 92.0 | 171.8 | no | too small to rank | not checked |
| Sunday | 3 | 369.0 | 328.3 | no | too small to rank | not checked |
| Tuesday | 2 | 126.0 | 126.0 | no | too small to rank | not checked |
| Thursday | 2 | 112.5 | 112.5 | no | too small to rank | not checked |

**Only Wednesday clears the floor.** Its median, 326.0, is 2.26 times the group's overall median of 144, and its concentration check comes back clean. But the format-confound check fires: video makes up 2 of Wednesday's 6 posts, `rep_ratio = (2/6) / (3/25) = 2.78`, well over the 1.5 line, and video is corpus-wide the highest-median type at 228, `type_median_ratio = 228/144 = 1.58`, over the 1.2 line. Both conditions clear, so the flag fires. **Say it exactly this way in the output:** "Wednesday's median is real and it clears the concentration check, but 2 of its 6 posts are video, which is this group's strongest format corpus-wide and is over 2.7 times its normal share of a Wednesday post. Some of Wednesday's edge may be a video effect wearing a day costume." That sentence, not a bare "post on Wednesday," is what the reused check exists to produce.

**Monday is worth naming even though it is unranked.** At n=4 it sits one post below the floor, with a median of 151.5, close to the group median. Listed, not ranked, per the standard floor language: "too small to rank, worth testing."

---

## Section 6: Building the 3 drafted posts

**The rule that governs this whole section: every draft is built from the group's own topics, pulled from posts actually in the export, never a generic example from a different niche.** A draft that would work unchanged for any group in any niche proves the skill did not read the file.

1. **Read the norms block you just built (Sections 2 through 5) and select the norms that are real, not the ones you wish were real.** A norm that failed its own concentration check (question marks, in the worked example) does not get cited in a draft as if it were confirmed.
2. **Pull 3 to 5 topic phrases from the group's actual `Content` field**, favoring the topics that recur across multiple authors, not one person's specialty.
3. **Draft post 1: the highest-confidence norm draft.** Built from the length band and type that ranked cleanly (no concentration flags), in first person if that tone cleared its own check, on one of the group's real topics.
4. **Draft post 2: modeled on one recurring author's mechanism, not their identity.** Take the *structure* named in Section 4 (a direct opening question with permission for an incomplete answer, or a callback-and-result narrative), fill it with a different topic than that author actually used, and say in one line which author's pattern (by letter, never by name) it borrows the mechanism from.
5. **Draft post 3: a test of the best unranked signal.** If a type or band was "too small to rank, worth testing" and its median was strong (video, in the worked example, at 228, the highest of any type), draft into that format rather than repeating what is already proven, and say explicitly that this one is a test, not a repeat of a confirmed finding.
6. **Every draft ends with a one-line citation of which norms it satisfies**, naming the section each norm came from, so the reader can check the draft against the evidence instead of taking it on faith.
7. **No draft may contain a promo marker from Section 3.3's list**, unless the point of the draft is explicitly to test promo tolerance, which this skill does not recommend doing on someone else's group without reading that group's actual rules first.

---

## Section 7: What this rubric refuses to do

- **No claim that a norm found in one group applies to any other group.** Every finding here is scoped to the captured group, stated as such, and never generalized to "groups in general," which is what `references/group-norms-taxonomy.md` is for, as a separate, explicitly general reference.
- **No promo-marker heuristic presented as a moderation tool.** It estimates performance, not policy. It is not evidence a post violated group rules, only a language pattern correlated with lower engagement in this data.
- **No day-by-time claim.** Section 5 is explicit about why: the volume is not there in a typical group capture, and a mostly-empty grid is not a section.
- **No author pattern below 3 posts**, and no author's real name in any output, ever.
- **No superlative that has not been checked literally.** "Best," "worst," "only," and any word ending in "-est" must be confirmed against the actual ranking before it is written, scoped to what was ranked, not to the group's reputation.
