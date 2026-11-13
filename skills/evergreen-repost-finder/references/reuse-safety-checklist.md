# reuse-safety-checklist.md

A 24-item checklist for whether ONE SPECIFIC post is safe to repost, right now, unchanged. The main rubric (`rubric.md`) runs the evergreen filter and the age gate across a whole export mechanically. This checklist is the by-hand version: run it on a single post when a user wants to sanity-check one specific candidate, or when a post sits close to a boundary and deserves a second look before it goes out again.

Every item is yes or no. Every item states what a "no" means. Run all 24. A post does not need a perfect sheet to be repostable, most items will be "no" in the harmless direction on most posts, but every "yes" that flags a real risk needs the stated action before the post goes back out.

Version 1.0 | 2026-08-04

---

## How to use this

Take one post: its `Content`, `Type`, `Link_URL`, `Link_Title`, `Media_URLs`, and `Duration_Sec` fields from the export. Work down the list. Where the item asks a yes/no question about the post, answer it from the export data and the caption text alone, never by guessing or by fetching a URL. Where an item requires information outside the export (whether a price is still accurate, whether a linked page still exists), the answer is "not checked" until the user confirms it, and "not checked" is reported as its own state, never collapsed into "no" or "yes."

---

## A. Dated-language checks

**1. Does the hook contain a currency-anchor phrase** ("since {month or year}" describing the author's own streak, a near-term deadline paired with a weekday, "this week/month/year" describing the author's own current state rather than a reader-facing generic label)?
- **Yes:** the hook needs replacing before repost. This is the section 2.1 test from `rubric.md`; run it before answering.
- **No:** the hook passes this check.

**2. Does the body (the caption minus the hook) contain a currency-anchor phrase?**
- **Yes:** the post is DATED-BODY. Exclude it from any repost or remake until the underlying claim is manually re-verified and rewritten. A hook swap alone cannot fix this.
- **No:** the body passes.

**3. Does the hook or body contain an explicit calendar year or product/app version used as a currency claim** ("this year's," "the new X," a version number), as opposed to a year embedded in a personal-history detail that does not change truth value over time?
- **Yes:** flag the specific phrase and treat as category B in `rubric.md` section 2.2.
- **No:** passes.

**4. Does the hook or body name a live, one-time event as the reason to act now** (a named sale, a launch, "the offer ends Friday")?
- **Yes:** the post is tied to an event that has already happened. Exclude or rewrite before reposting.
- **No:** passes.

**5. Control question, not a disqualifier: does the post contain a time word (a weekday, a month, "this week") that reads as a narrative anchor or a reader-facing generic instruction, not a currency claim, per the section 2.1 test?**
- **Yes:** this is fine. Time words are common in captions; only currency claims (items 1 through 4) are a problem. Say which test result applies so the reasoning is visible.
- **No:** there is no time word in the post at all, which is also fine, and slightly easier to verify.

---

## B. Factual-claim aging

**6. Does the post state a specific price, cost, or dollar figure?**
- **Yes:** confirm the figure is still accurate before reposting. A "no" to that confirmation means update or drop the figure; do not repost a stale price.
- **No:** nothing to check here.

**7. Does the post cite a count that grows over time** (years in business, total clients served, a cumulative total)?
- **Yes:** the number is stale the moment more time passes after publish. Confirm the current figure. A "no" to "is this still the right number" means update it before reposting.
- **No:** nothing to check here.

**8. Does the post name a specific product, brand, tool, or app?**
- **Yes:** confirm the product still exists and is still what the creator would recommend. A "no" means swap or drop the mention.
- **No:** nothing to check here.

**9. Does the post reference a policy, rule, or regulation** (a store's return window, an HOA rule, a tax rule, a platform's terms)?
- **Yes:** these change without notice. Confirm the rule still holds before reposting. A "no" means the post needs a rewrite or a caveat.
- **No:** nothing to check here.

**10. Does the post make a comparative claim against a named competitor or alternative** ("better than X," "unlike Y")?
- **Yes:** confirm the comparison still holds and the named competitor still exists in the form described. A "no" means revise the comparison.
- **No:** nothing to check here.

---

## C. Seasonal windows

**11. Is the post's core subject a season or a holiday** (packing away winter coats, back-to-school bins, holiday decor storage), as opposed to a season mentioned only in passing?
- **Yes:** classify this post SEASONAL EVERGREEN, not CLEAN EVERGREEN, per `rubric.md` section 2.3. It is reusable, but only in the matching season.
- **No:** this check does not apply to this post.

**12. If item 11 is yes, does the post pin the season to an exact date or year** ("Christmas 2025," "back to school 2026")?
- **Yes:** the year must be dropped or updated before reposting even in-season.
- **No:** the general seasonal framing is safe to reuse indefinitely, once per matching season.

**13. If item 11 is yes, has the matching season actually arrived relative to today's date?**
- **No:** hold the post. Do not repost a seasonal post off-season no matter how well it scored the first time.
- **Yes:** the post is in its window and may be reposted, subject to every other item on this list.

---

## D. Audience-shift checks

**14. Does the post address a specific life-stage or demographic segment whose needs might have shifted since publish** ("new parents" writing about a specific-age child, "renters" writing about a lease term)?
- **Yes:** confirm the segment would still recognize itself in the post as written. A "no" means the post needs a different angle before reposting, not just a repost.
- **No:** nothing to check here.

**15. Does the post reference the creator's own current business capacity or offer** ("I have two openings left," "booking for Q3")?
- **Yes:** this is almost always stale by the time a post is old enough to repost. Drop or update the line before reposting.
- **No:** nothing to check here.

**16. Does the post describe a specific platform feature or UI step** ("tap the three dots," "swipe up")?
- **Yes:** confirm the feature still exists and works as described; platform UIs change without notice. A "no" means rewrite the instruction.
- **No:** nothing to check here.

**17. Does the post cite the creator's own follower count, reach, or account size** ("with 40k of you watching")?
- **Yes:** this number changes constantly and is almost never worth reposting verbatim. Drop the specific figure or generalize it.
- **No:** nothing to check here.

---

## E. Link-rot check, via `Link_URL` presence

**18. Is `Link_URL` populated on this post** (a `link`-type post, or a link embedded in the caption text)?
- **Yes, and the destination has been checked in this run:** proceed.
- **Yes, and it has NOT been checked:** report "link not verified," not "safe." This skill never fetches URLs itself; verifying a link is a step for the user to confirm outside this analysis.
- **No:** this check does not apply to this post.

**19. If `Link_URL` is populated, does `Link_Title` still describe something the creator would currently promote?**
- **Yes, and confirmed in this run:** proceed, subject to item 18's verification status.
- **Not checked:** report "promotion status not verified," not "safe." This skill never fetches the destination itself; confirming what the creator would currently promote is a step for the user to confirm outside this analysis.
- **No:** the linked content is superseded. Exclude the post from repost until the link is swapped, or repost without the link if the caption stands alone.

**20. Does `Content` contain a link written as plain text, separate from `Link_URL`** (a URL typed into the caption body rather than attached as a link post)?
- **Yes:** apply items 18 and 19 to that in-caption link as well. A caption-embedded link is just as capable of rotting as a formal `Link_URL`.
- **No:** this check does not apply.

---

## F. Media dependency, via `Media_URLs` presence, expiry noted

**21. Is `Media_URLs` populated on this post?**
- **Yes:** the post's original meaning may depend on an image or video this skill has never seen and will never fetch, because `Media_URLs` links expire and this skill treats them as an opaque presence flag only, per `references/csv-parse.md` section 5 (condensed from `_shared/csv-contract.md`; full version in the bundle).
- **No:** the post is text-only, or its media did not survive capture. Repost readiness for this post does not depend on a visual this skill cannot check.

**22. If item 21 is yes, does the caption stand alone without the image, or does it depend on the reader seeing something** ("look at this drawer," "before and after below")?
- **Depends on the image:** the user must confirm they still have the original photo or video file before reposting, separate from whatever PostSnag captured, because the captured link will not resolve.
- **Stands alone:** the missing media is not a blocker for text repurposing, though a remake to a stronger format (per `rubric.md` section 4.2) would still want fresh media.

**23. If `Type` is `video`, is `Duration_Sec` populated?**
- **Yes:** this confirms the row captured as a video, but the export never stores the video file itself, only that it existed with this length. The user must confirm the source video file still exists before committing to a straight repost.
- **No:** the video metadata did not fully capture on this row. Treat the row's `Type` as reported but flag that duration data is absent, not zero.

**24. Does the post's value depend on a screenshot, chart, or graphic that itself contains data** (a stat graphic, a labeled before-and-after, a price list rendered as an image)?
- **Yes:** that graphic's data can go stale independently of the caption text, and this skill cannot read image content it has not been shown. Check the graphic's numbers separately from every dated-language check above, using the user's own copy of the image.
- **No:** nothing further to check here.

---

## Reading the finished sheet

**Count the "yes" answers that flagged a risk (items 1 through 4, 6 through 10, 12, 14 through 17, 19 with a "no," 21 through 24 with a dependency).** Zero flags plus a passed age gate plus a score at or above 1.5x is what `rubric.md` calls REPOST AS-IS. One or more flags that a hook swap or a format change fixes is a REMAKE, per `rubric.md` section 4. A DATED-BODY flag (item 2) or an unresolved factual-aging flag (items 6 through 10) that the user has not personally verified means the post stays off the shortlist regardless of its score, because this skill can compute an era-adjusted score from an export, but it cannot verify a price, a policy, or a still-existing product from a CSV file. That gap is exactly why this checklist exists as a manual companion to the automated rubric, not a replacement for it.