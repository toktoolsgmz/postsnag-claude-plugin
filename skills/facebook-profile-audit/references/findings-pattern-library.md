# findings-pattern-library.md

29 mechanical patterns for reading a profile audit's own numbers into conclusions worth putting in front of a client. Original writing, built for this skill. Each pattern names the exact signal in the data that triggers it, the evidence line to cite, the recommendation it generates, and one worked example computed from the shared synthetic file.

**How to use this file.** Run the method in `rubric.md` first, so you have the format table, the topic table, the cadence numbers, the video duration bands, and the trajectory read (if it ran). Then walk this list top to bottom. A pattern fires when its signal is literally true of a bucket in your tables, not when it feels like it should apply. Every fired pattern gets instantiated with your real numbers before it goes in the output; an un-instantiated pattern name is not a conclusion.

Version 1.0 | 2026-08-04

---

## Format patterns

### 1. Format Lift

**Signal:** a rankable format (n >= 5) has a median at least 15 percent above the corpus median, with zero or one concentration flag.
**Evidence to cite:** the format's n, median, corpus median, and any single flag glued inline.
**Recommendation:** write more in this format, at the current mix or slightly higher.
**Worked example:** Video, 14 posts, median 585 against a corpus median of 458.5 (a 27.6 percent lift), one flag on mean/median (1.89), median is the number to trust.

### 2. Format Drag

**Signal:** a rankable format sits below the corpus median with zero concentration flags, so the underperformance is not noise.
**Evidence to cite:** the format's n, median, corpus median, zero flags stated explicitly.
**Recommendation:** reduce the format's share of the rotation, or redesign what goes into it before cutting it outright.
**Worked example:** Long videos (71 seconds and over), 5 posts, median 455 against a corpus median of 458.5, no concentration flags: a clean, real, mild underperformance.

### 3. Absent From The Top

**Signal:** a format or topic has real volume (5 or more posts, at least 10 percent of the corpus) and zero presence in the top quartile.
**Evidence to cite:** the bucket's share of the corpus against its 0-count share of the top quartile.
**Recommendation:** the strongest "stop doing this as much" conclusion in the catalog; pair it with a specific alternative format or topic.
**Worked example:** Album, 8 posts (13.3 percent of the corpus), 0 of the top 15 posts.

### 4. Untested Standout

**Signal:** a bucket sits below the 5-post ranking floor and its raw median (reported, not ranked) is the highest or near-highest of its category.
**Evidence to cite:** the bucket's n, its median, and the phrase "too small to rank, worth testing," never a rank number.
**Recommendation:** write enough more posts in this bucket to clear n=5, a specific number away.
**Worked example:** Link posts, 4 posts, median 795, the highest median of any format in the file, one post short of rankable.

### 5. Volume Mismatch, Over-invested

**Signal:** a bucket's share of the corpus exceeds its share of the top quartile by a wide margin (roughly 1.5x or more).
**Evidence to cite:** both shares, side by side, with the ratio stated.
**Recommendation:** trim the bucket's volume and redirect the freed slots toward an under-invested bucket.
**Worked example:** Album is 13.3 percent of the corpus and 0.0 percent of the top 15, an infinite ratio in practice; a smaller but real example from the format table is text and photo together carrying 56.6 percent of volume for 53.4 percent of the top 15, roughly even, which is why this pattern is written as "a wide margin," not any divergence at all.

### 6. Volume Mismatch, Under-invested

**Signal:** a bucket's share of the top quartile exceeds its share of the corpus by a wide margin.
**Evidence to cite:** both shares, side by side, with the ratio stated.
**Recommendation:** increase the bucket's volume; it is already proving itself on too little evidence.
**Worked example:** Video is 23.3 percent of the corpus and 33.3 percent of the top 15, a 1.43x over-index relative to its own volume.

### 7. Flat Bucket, No Signal

**Signal:** a rankable bucket's median sits within roughly 5 percent of the corpus median, with zero flags.
**Evidence to cite:** the bucket's n, median, corpus median, and the percentage gap.
**Recommendation:** none. State plainly that this bucket was tested and returned nothing, per `references/foundations.md` section 6's "report no signal, do not drop it" rule.
**Worked example:** Kitchen & Counters, 5 posts, median 462 against a corpus median of 458.5, a 0.8 percent gap, no flags: tested and flat.

### 8. One-Post Carry

**Signal:** a ranked bucket flags two or three of the three concentration checks.
**Evidence to cite:** all three check values (median-after-removal, top-share, mean/median), not just which ones flagged.
**Recommendation:** never a bucket-level recommendation. Name the specific post or posts responsible and suggest studying them individually.
**Worked example:** the medium-length video duration band (41 to 70 seconds), 5 posts, flags on top-share (45.1 percent) and mean/median (2.65); the honest conclusion is that two specific posts, not a duration effect, explain the number.

---

## Topic patterns

### 9. Dominant Topic

**Signal:** the topic cluster with the highest post count in the whole inventory, regardless of its performance.
**Evidence to cite:** its n against the second-highest cluster's n, and its median against the corpus median.
**Recommendation:** if its median is at or above the corpus median, keep the rate; if below, the volume is not the problem, the execution inside the topic is.
**Worked example:** Closets, 10 posts, nearly 1.5x the next-largest cluster (Labels & Systems at 7), median 530 against a corpus median of 458.5: dominant and clean.

### 10. Thin Topic Cluster

**Signal:** a topic cluster has 1 to 4 posts.
**Evidence to cite:** its n and its raw median, explicitly not ranked.
**Recommendation:** write the specific number of additional posts needed to reach n=5.
**Worked example:** Garages, 4 posts, median 460.5, one post from the floor.

### 11. Topic Gap

**Signal:** a topic implied by the profile's stated niche or bio never clears even 2 posts in the extraction, or does not appear at all after the merge step.
**Evidence to cite:** the topic's absence, stated plainly, with the niche context that made you look for it.
**Recommendation:** a specific test: write 3 posts in the missing topic and see if it earns a place in the next audit.
**Worked example:** Entryways, a real organizing subtopic, appears only once (268 engagement) in 60 posts about a home-organizing niche.
**Note:** bio exists only in the Markdown export, not the CSV; a CSV-only capture cannot run the bio-implied side of this check and should fall back to niche context alone.

### 12. Cross-Format Topic

**Signal:** a topic cluster's posts span 3 or more different `Type` values.
**Evidence to cite:** the topic's format breakdown (n per type within the cluster).
**Recommendation:** this is a topic that survives format changes; it is a safer bet for a new format than an untested one.
**Worked example:** Closets appears across photo (5), video (4), and link (1) posts in the synthetic file, three types clearing the trigger, the topic itself carrying the engagement regardless of format.

### 13. Bimodal But Clean

**Signal:** a ranked bucket's member posts span a very wide raw range (the highest is 5x or more the lowest) but the concentration check clears all three parts.
**Evidence to cite:** the range, then all three concentration numbers, explicitly stating that the check clears.
**Recommendation:** trust the median as reported; do not discount it just because the range looks dramatic.
**Worked example:** Closets spans 208 to 1,904 (a 9.2x range) and clears the concentration check clean on all three parts; the median of 530 is real.

---

## Cadence patterns

### 14. Steady Rhythm

**Signal:** the gap-day distribution (using calendar-date subtraction) has a tight range, typically a median gap within 1 day of both the minimum and maximum.
**Evidence to cite:** the median, minimum, and maximum gap.
**Recommendation:** none needed; name it as a strength the client should not disrupt.
**Worked example:** median gap 2 days, minimum 0, maximum 3, across 130 days: a reliable, low-variance schedule.

### 15. Silent Days

**Signal:** one or more days of the week carry fewer than 5 percent of total posts.
**Evidence to cite:** the exact posting count for each quiet day.
**Recommendation:** a specific, small test (one post) on a quiet day, framed as untested rather than as a known weak day, since this skill does not measure day-of-week performance.
**Worked example:** Wednesday, Friday, and Sunday each carry 1 post out of 60, against Saturday's 19.

### 16. Same-Day Doubling

**Signal:** two or more posts share an actual calendar date, confirmed with calendar-date subtraction, not raw timestamp subtraction.
**Evidence to cite:** the date and both posts, with their times and engagement.
**Recommendation:** if the doubled day performed well, suggest testing the pairing deliberately (for example, one long-form post and one quick engagement post on the same day) rather than treating it as an accident.
**Worked example:** 2026-07-28 carries a 238-engagement text post in the morning and a 902-engagement photo post in the evening (engagement is Reactions plus Comments plus Shares, not the Reactions cell alone); the photo sits inside the top 10 posts in the capture, so the recommendation fires: suggest testing the pairing deliberately.

### 17. False Same-Day Signal

**Signal:** a naive full-timestamp subtraction reports a 0-day gap that a calendar-date subtraction does not confirm.
**Evidence to cite:** the two timestamps and their actual time-of-day gap.
**Recommendation:** none; this is a method-integrity check, not a conclusion to report to the client. Fix the computation before reporting cadence at all.
**Worked example:** 2026-07-25 at 16:00 to 2026-07-26 at 11:05 is a 19-hour gap that a raw `timedelta.days` reports as 0, misreading a normal one-day cadence as a same-day double post.

### 18. Long Silence

**Signal:** the single longest gap in the corrected gap-day list, named with its two surrounding dates.
**Evidence to cite:** the gap length and both dates.
**Recommendation:** ask what happened around that date (a launch, travel, a break) before assuming it was a mistake; note it as context for the client conversation.
**Worked example:** the longest gap in the full 60-post capture is 3 days, and it recurs 17 times, which is itself the point: there is no true outlier silence in this file, cadence is uniformly tight.

---

## Video patterns

### 19. Flat Conversion, Wide Raw Spread

**Signal:** raw engagement across video rows with `Views` spans much wider (as a multiple) than engagement-per-view spans.
**Evidence to cite:** both spreads, as multiples, side by side.
**Recommendation:** whatever separates the winners from the losers happened before the view (distribution, not content quality per view); do not chase per-video "quality" fixes without also addressing reach.
**Worked example:** raw engagement spans 19.8x across 14 videos while engagement-per-view spans only 1.32x.

### 20. Duration Band Signal

**Signal:** two duration bands both clear the 5-post floor and their medians differ by 20 percent or more, with the higher band's concentration check clean.
**Evidence to cite:** both bands' n, median, and concentration results.
**Recommendation:** shift new video length toward the stronger, clean band.
**Worked example:** in this file, no clean pair exists (medium flags, long is clean but lowest), which is itself worth stating: not every profile hands you a clean duration recommendation, and this one does not.

### 21. Video Premium With A Caveat

**Signal:** video's rankable median beats the corpus median, and its concentration check flags on exactly one of the three parts.
**Evidence to cite:** the median lift and the specific flagged part.
**Recommendation:** trust the median, name the flag, do not claim the mean.
**Worked example:** video median 585 against corpus 458.5, flagged only on mean/median (1.89).

### 22. Two Posts, Not A Trend

**Signal:** a ranked bucket flags on top-share and mean/median specifically because 2 individual posts, not 1, account for most of its total.
**Evidence to cite:** both posts, named, with their engagement and their shared trait.
**Recommendation:** treat the shared trait as a hypothesis to test with new posts, not as a validated rule.
**Worked example:** the medium-video-length band's two highest posts (4,118 and 3,402 engagement) are the profile's two best posts of any kind, both roughly a minute long.

### 23. Views Present, Duration Thin

**Signal:** `Views` is populated on enough posts for the raw-versus-rate read (5 or more), but no individual duration band clears the 5-post floor.
**Evidence to cite:** the total video-with-views count against each band's count.
**Recommendation:** report the raw-versus-rate conclusion, explicitly withhold any duration-band claim, and name the capture depth needed to unlock it.
**Worked example:** the free-tier slice has 7 of 7 videos with `Views` (enough for the rate read) but only 2, 2, and 3 posts per band (none rankable).

---

## Engagement-spread and structure patterns

### 24. Top-Heavy Corpus

**Signal:** the top-quartile cut value is 1.5x or more the corpus median.
**Evidence to cite:** the cut value and the corpus median, with the ratio.
**Recommendation:** frame the account's ceiling honestly: a handful of posts are doing outsized work, and the median describes a normal week, not a viral one.
**Worked example:** top-quartile cut value 700 against a corpus median of 458.5, a 1.53x ratio.

### 25. Repeat Offender, Bottom 10

**Signal:** one format or topic appears in the bottom 10 at a rate at least double its share of the whole corpus.
**Evidence to cite:** the bucket's bottom-10 count against its corpus share.
**Recommendation:** name it plainly as a pattern in the client's weakest posts, distinct from a "does not work" median conclusion, because this is about the tail specifically.
**Worked example:** on the synthetic file, no format doubles its corpus share in the bottom 10 (photo is closest, 4 of 10 against a 28.3 percent corpus share), which is itself worth stating: the weak tail here is spread across formats, not concentrated in one.

### 26. Repeat Winner, Top 10

**Signal:** one format or topic appears in the top 10 at a rate at least double its share of the whole corpus.
**Evidence to cite:** the bucket's top-10 count against its corpus share.
**Recommendation:** the strongest single-line pitch material in the audit; lead with it in the client conversation.
**Worked example:** link is 2 of the top 10 (20 percent) against a 6.7 percent corpus share, a 3.0x over-index, clearing the 2x trigger. (Video comes close but does not fire: 4 of the top 10 against a 23.3 percent corpus share is a 1.72x over-index, below the 2x bar, so it is reported as a near-miss, not as this pattern.)

---

## Trajectory patterns (gated on span >= 90 days and full mode)

### 27. Rising Half

**Signal:** trajectory_ratio >= 1.15, and neither half flags 2 or more concentration checks.
**Evidence to cite:** both halves' medians and dates, the ratio, and the confound sentence, every time, no exceptions.
**Recommendation:** frame it as momentum worth protecting, never as proof the content strategy alone caused it.
**Worked example:** later-half median 530 against earlier-half median 402, ratio 1.32, both halves clean, confound sentence attached.

### 28. Flat Trajectory

**Signal:** trajectory_ratio between 0.87 and 1.15.
**Evidence to cite:** both halves' medians, the ratio, and the confound sentence.
**Recommendation:** no trend claim in either direction; state that the account has been stable across the capture window.
**Worked example:** not present in the shared synthetic file (the file was built to show a clean rising trend); a flat result elsewhere would be reported exactly as plainly as a rising or falling one.

---

## Single-post patterns

### 29. Single Best Post

**Signal:** one individual post is the highest-engagement post in the entire capture, independent of which bucket (format, topic, duration band) it belongs to.
**Evidence to cite:** the post's engagement number, its format and topic, and its caption's hook or opening line, verbatim.
**Recommendation:** study this post on its own, independent of any bucket ranking; a single standout post is evidence about that post, not proof a whole bucket works.
**Worked example:** Maya's all-time top post (4,118 engagement, "A client cried in her own pantry on Monday, and it was not about food."), a first-person client story, medium-length video (47 seconds).
