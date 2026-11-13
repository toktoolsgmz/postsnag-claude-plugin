Condensed reference. The full version lives in the complete-bundle download.

# foundations.md

Every shared number and formula this skill uses, defined once. Cite these. Do not invent your own.

Version 1.0 | 2026-08-05

---

## 1. Engagement

```
engagement = Reactions + Comments + Shares
```

Total, unweighted, 1 to 1 to 1. PostSnag captures no reach, impressions, clicks, or conversions, so there is no outcome in the file to validate a weighting against. A weighted score would be a number we made up wearing the costume of a model. `Reactions` is a total only. No per-emoji breakdown exists anywhere in the export. Comment-heaviness and share-heaviness get reported as their own numbers (`Comments / engagement`, `Shares / engagement`), never folded into the score.

## 2. Medians rank. Means never do.

Every headline number is a median. Social engagement is a power-law distribution and one or two posts carry the mean. The median describes the post the user is going to write next week.

- Rank on the median. Not once on the mean, in any section.
- Report the mean beside it only when the two diverge, say why, and say which one you ranked on.
- **Divergence flag:** `if mean >= 1.5 * median`, the bucket is carried by its top members and the output says so.

## 3. Sample floors

| Posts analyzed | What you may claim |
|---|---|
| under 5 | Nothing quantitative. Qualitative read only, labeled as one person's opinion. |
| 5 to 14 | Every finding labeled **directional**, next to the ranking, not in a footnote. No superlatives. Write "the highest median in this capture of 12 posts", never "your best hook". |
| 15 to 39 | Rankings may be stated as findings. Lite mode still applies (section 5). |
| 40 or more | Full mode. |

**Per-bucket floor: 5 posts.** A bucket is any group you rank: a hook archetype, a post type, a day of week, a time window, a topic cluster, a format. A bucket under 5 posts gets no rank number, never appears in the ranking table, and is never called best or worst. It is also never deleted. It goes on its own line beneath the table, as "too small to rank (n below 5), worth testing: Bold Claim (n=3, median 1,044), Curiosity Gap (n=2, median 959)". Deleting small buckets hides the most actionable signal in the file. Ranking them fabricates one. Naming them as untested is the only honest option, and "you used this three times and it won three times, go test it" is better advice than any ranking on the page.

**A flags column prints "not checked", never "none".** "None" asserts a result that was never computed. Run the required checks on every ranked bucket.

## 4. Concentration check

Run all three parts on any bucket that is about to become a recommendation. Medians are robust to one outlier by construction, so the old "delete the top post and see if the claim dies" test passes everything and proves nothing. This version fires.

```
1. median_after = median of the bucket with its single highest post removed
   flag if  |median_after - median| / median  >  0.20
2. top_share    = highest post's engagement / sum of the bucket's engagement
   flag if  top_share > 0.40
3. divergence   = mean / median
   flag if  divergence >= 1.5
```

**One flag:** the bucket is being carried. Glue that to the number in the same sentence, never as a trailing parenthetical. "Story Cold Open, median 430 across 8 posts. One post accounts for 59 percent of the archetype's total engagement, so treat the median as the honest number and the average as noise."

**Two or three flags:** the bucket does not become a recommendation at all. It becomes "one post did something worth studying", and you name that post.

## 5. Lite mode

```
LITE MODE if:  posts_analyzed < 40   OR   span_days < 60
span_days = (latest Posted minus earliest Posted) + 1, computed after parsing, never taken from what the user said
```

**In lite mode, do not:** era-adjust, report a trend or trajectory, report time-of-day windows, rank any bucket under 5 posts, or use a superlative about the creator's whole account.

**The one carve-out.** A time-of-day cell that clears the 5-post floor may be reported as one labeled "early signal" (one cell, or the better of two), with its n and its median, under its own heading and outside any windows table. Never a ranked table. A cell that cleared the floor is real evidence and deleting it to honor a mode is the same throwing-away error the floor exists to prevent.

**In lite mode, do:** open with the lite-mode banner, label every ranking directional if the corpus is also under 15 posts, and name the specific missing thing. "You have 30 posts over 60 days. Day-of-week needs 5 posts per day; you clear that on 2 days of 7" is useful. "Limited data" is not.

**The free tier is lite mode by design, and the skill says so out loud.** On the free tier you see 30 posts per profile, so expect an export around that size, which is under 40. Two things worth stating exactly. First, the free slice is the **most recent** posts, not a random sample, so anything that depends on comparing an older era to a newer one is **unavailable, not underpowered**, because the older era is not in the file. Second, the fix is a specific number, not an apology: "this clears the bar at 40 posts and gets its time-of-day section at roughly 5 posts per weekday, so about 60 posts across at least 60 days."

## 6. Top quartile, top 10 versus bottom 10, ties

```
k = floor(N / 4)
```

Sort descending by engagement, take the first `k` posts, and report both `k` and the engagement value at the cut so the user can reproduce it. On a 60-post capture, `k = 15`.

- **If `k < 5` (that is, `N < 20`):** do not call it a quartile. Take the top 5, label it "top 5 posts", and only if `N >= 15`.
- **Ties at the cut:** include every post tied with the cut value and report the real count ("top 15 by definition, 16 posts after including a tie at 700").
- **The finding is composition, not membership.** Compare each bucket's share of the corpus against its share of the top quartile. Where the two disagree, that is the recommendation, and it took no adjectives to produce.

**Top 10 versus bottom 10 requires `N >= 25`.** Below that the two sets are most of the corpus and the contrast is meaningless. Compare their **composition**, never their medians, which is circular. A bucket showing up 4 times in the bottom 10 and once in the top 10 is a finding. A bucket appearing about evenly in both is reported as "no signal", never quietly dropped.

## 7. Rounding

Medians and engagement counts: whole numbers, comma separators above 999. Percentages: one decimal. Multiples and era scores: two decimals. Never report more precision than the input carries, and the input is integer counts of reactions.

## 8. Video, a secondary lens only

`Views` and `Duration_Sec` are populated on video rows and empty everywhere else.

```
engagement_rate_per_view = engagement / Views * 100      (percentage, one decimal)
```

1. **Never mix it with non-video rows.** Compute it over video rows only and say how many rows that is.
2. **Never rank on it.** Rank on raw engagement, use the rate to explain.
3. **A flat rate is itself a finding.** If raw engagement spans 20x and rate per view spans 1.3x, almost everything separating the winners happened before the view. PostSnag captures no reach or impressions, so you say that and stop rather than guessing at the algorithm.

`Duration_Sec` is a grouping variable (short, medium, long), not a performance metric. Do not correlate duration with engagement on fewer than 5 videos per length bucket.

**Nothing here computes a rate against followers, a sponsored versus organic split, a comment sentiment read, a growth curve, or a conversion number**, because the export carries no reach, no paid-partnership flag, no follower history, no comment text, and no click data. If a user asks for one, name the field that would be needed and say PostSnag does not capture it. Capture depth equals scroll depth, so no output ever says or implies "full history".
