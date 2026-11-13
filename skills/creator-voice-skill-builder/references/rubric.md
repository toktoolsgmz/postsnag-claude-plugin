# rubric.md

The full recipe for Creator Voice Skill Builder. Written so an agent with no other context can execute it and hand a user a finished, permanent skill at the end.

Version 1.0 | 2026-08-04

---

## Section 0: What this recipe is actually building

Two files. Not a caption, not an analysis report. A permanent skill folder the user installs once:

1. **The voice skill itself**, filled from `voice-skill-template.md`. This is the file the user's agent reads every time they ask for a caption from now on.
2. **The style playbook**, filled from `style-playbook-template.md`. A companion reference the voice skill points to, the same way every skill in this catalog keeps its depth in a reference file instead of bloating the main one.

Everything in this rubric exists to fill those two files honestly, with real measurements, and to prove the result actually works before the user walks away with it. That proof is Section 5, the 3-test acceptance run, and it is not optional. A voice skill nobody tested is a guess with a folder structure.

---

## Section 1: Selecting the style-source posts and checking they are not one post wearing a disguise

**Compute every number in this analysis with code.** The selection cut, the concentration check, and every measurement in Section 3 follow that rule; a wrong number presented with confidence is worse than no number.

**Identical selection rule to `facebook-caption-writer/references/rubric.md` section 1.** This skill does not redefine it:

```
k = floor(N / 4)
```

Sort descending by engagement (reactions plus comments plus shares), take the first `k` posts, report `k` and the engagement value at the cut, including ties at the boundary.

**If `k < 5` (N < 20):** take the top 5 and label it "top 5", only if `N >= 15`. Below 15 posts total, run the qualitative path: read the posts you have directly, skip the ranked selection, and say plainly that this is a small-sample reading, not a measurement.

### 1.1 The concentration check, run on the style-source set as a whole

A voice profile built mostly off one viral post is not a profile of the creator's voice, it is a profile of one post's voice wearing the creator's name. Run all three parts of the concentration check in `references/foundations.md` section 4 (condensed from `_shared/engagement-math.md` section 5; full version in the bundle), applied to the style-source set as a single bucket rather than to a ranked archetype:

```
1. median_after = median of the style-source set with its single highest post removed
   flag if |median_after - median| / median > 0.20

2. top_share    = highest post's engagement / sum of the style-source set's engagement
   flag if top_share > 0.40

3. divergence   = mean / median
   flag if divergence >= 1.5
```

**If any part flags,** say so in the voice profile, name the post responsible, and note that its individual mechanics carry extra weight in what follows. This is a disclosure, not a stop condition. The post still won, and its habits still belong in the sample; the user just needs to know one post is doing more of the talking than the other fourteen.

**If none flag,** say that too, in one line, with the actual numbers. A profile built on 15 posts pulling roughly even weight is worth stating as plainly as a profile that is not.

---

## Section 2: The promo screen

**Why this is a heuristic and not a detector, stated once so it never has to be re-justified.** No PostSnag export, in any format, carries a sponsored or paid-partnership flag. Section 10 of `_shared/csv-contract.md` and section 10 of `_shared/engagement-math.md` both say this because it matters everywhere in this catalog, and it matters most here: a permanent voice skill that quietly absorbed a paid partner's tone into "the creator's voice" would keep producing that tone forever, on every future topic, with no way for the user to notice where it came from.

### 2.1 The marker list

Run these three checks against every post in the style-source set. A post can match more than one category. Record every match; do not stop at the first.

**A. Partnership and sponsorship language.** Case-insensitive substring match against `Content`, anywhere in the caption, not just the hook line:

```
sponsored, paid partnership, in partnership with, brand partner, ambassador,
gifted, thanks to @ (any @-mention immediately preceded by "thanks to"),
#ad, #sponsored, collab with, collaboration with
```

**B. Discount-code language.** Case-insensitive substring or pattern match:

```
% off, percent off, discount code, promo code, use code, coupon, "code:" (a colon directly after the word code)
```

**C. Link-out language.** Two separate tests, because they catch different things:

- **Structural:** `Type` equals `link`. Every link post is flagged, regardless of what the caption says, because the export's own `Type` column already told you this post points somewhere else.
- **Phrasing:** case-insensitive substring match against `Content` for `link in bio`, `shop now`, `shop the link`, `swipe up`, `click the link`, `linked below`, `link below`.

### 2.2 The mandatory manual review list

**This skill never silently excludes a post.** Every post that matched any marker in 2.1 goes on a review list, shown to the user, with:

- the post's date, type, and engagement
- which marker category matched and the exact phrase or field that triggered it
- the caption, or the relevant excerpt if it is long
- for structural link flags: the `Link_URL` domain, so the user can see at a glance whether it points to their own site or somewhere else

**The user confirms each one: keep in the style-source set, or exclude as promotional.** This skill does not make that call. It surfaces the evidence and gets out of the way. Report the confirmed exclusions, if any, and recompute the style-source set's mechanics on the confirmed set before moving to Section 3.

### 2.3 The false-positive risk, stated so nobody trusts this more than they should

The structural link-out test is the one most likely to over-fire. A creator who links to their own blog post, their own free download, or their own resource page gets flagged by `Type == link` exactly the same way a creator who links to a paid partner's storefront does, because the export's `Type` column does not distinguish "my own content" from "someone else's paid placement." The domain in `Link_URL` is the tell, and it is why the review list shows it: a `Link_URL` on the creator's own domain is a strong signal the post is self-promotion, not paid promotion, and the user can usually clear it in one glance.

The reverse failure mode is real too and cannot be fixed by this heuristic: a paid post that never uses any marker word and does not use the `link` post type at all (a photo post with a caption that never says "sponsored") will not be flagged. This screen catches language patterns, not payments. Say this in the output every time, not just in this rubric.

---

## Section 3: Extracting the voice markers

**This skill does not define its own mechanics.** `facebook-caption-writer/references/rubric.md` section 2 already defines the 9 caption mechanics with exact measurement rules, and inventing a second definition for the same 9 ideas would mean two skills in this catalog could measure the same export and disagree, which is worse than picking one system and citing it. Run those 9 measurement rules on the confirmed style-source set from Section 2.

**Condensed table, precedence order matches the source rubric exactly:**

| # | Mechanic | What it measures | Source |
|---|---|---|---|
| 1 | Opening-line pattern | Classifies each hook into one of the 12 archetypes in `references/hook-archetypes.md` (condensed from `facebook-hook-analyzer/references/rubric.md` sections 2 and 2.13; full version in the bundle); names the default opening move | caption-writer rubric 2.1 |
| 2 | Sentence-length rhythm | Median and range of words per sentence, tight/loose flag at 3.0-word standard deviation, plus observed word-count and hook-length ranges | caption-writer rubric 2.2 |
| 3 | Line-break and whitespace style | Dominant line count and structure, named exceptions | caption-writer rubric 2.3 |
| 4 | Emoji usage | Count and position, or the plain statement that there are none | caption-writer rubric 2.4 |
| 5 | CTA placement and phrasing | Explicit platform CTAs versus closing-imperative sentences, counted separately | caption-writer rubric 2.5 |
| 6 | Hashtag behavior | Count, repeats, position | caption-writer rubric 2.6 |
| 7 | Capitalization habits | Hook-line case, ALL-CAPS word count, numerals versus spelled-out numbers in two separate roles (hook lead, list marker) | caption-writer rubric 2.7 |
| 8 | Question frequency | Share of hooks with a question mark, cross-checked against mechanic 1 so it is not double-counted | caption-writer rubric 2.8 |
| 9 | First-versus-second person | Distribution across 1st, 2nd, mixed, and true third-person-about-someone-else if it occurs | caption-writer rubric 2.9 |

**If you already have a caption-writer run on the same export and the same style-source set, reuse its numbers.** Recomputing them from scratch risks a second, slightly different answer to the same question, and `example-run.md` in this skill demonstrates the reuse rather than re-deriving.

---

## Section 4: Filling the two templates

### 4.1 `voice-skill-template.md`, the permanent skill

Work through every bracketed slot in `references/voice-skill-template.md` in order. Each slot maps to a specific piece of Section 3's output:

- **Frontmatter slots** (`name`, `description`): the built skill's own install identity. Name it after the creator, kebab-case (`{creator-name}-voice-writer`). Write the description the same way every skill in this catalog writes one: what it does in one sentence, five or more real trigger phrases in the user's own words.
- **Voice-profile slots**, one per mechanic from Section 3, in the same order as the condensed table. Each slot gets the measured number and the plain-language read, not just the number alone.
- **Example slots**, 3 to 5 real posts from the style-source set, each with its engagement number attached as evidence (`{caption or excerpt} ({engagement} engagements)`). These are the model posts future drafts get built from, so pick ones that span more than one archetype and more than one structural pattern, the same selection order as `facebook-caption-writer/references/rubric.md` section 3.1.
- **Guardrail slots.** These are not optional and they do not get thinned out to save space. See 4.3.

### 4.2 `style-playbook-template.md`, the companion reference

- **Hook patterns section:** the archetypes the creator actually uses, named from Section 3 mechanic 1's classification (`references/hook-archetypes.md`, condensed from `facebook-hook-analyzer/references/rubric.md` sections 2 and 2.13), with counts. Do not redefine the archetypes in the produced playbook, and do not cite `facebook-hook-analyzer` or any other sibling skill by path inside it either: the produced file is a standalone artifact a user installs alone, and a dangling reference to a file they do not have is a defect, not a citation. Name the archetypes and move on.
- **Rhythm and structure section:** the sentence-rhythm band and line-break structure from Section 3 mechanics 2 and 3, written as instructions a future draft should follow, not just as measurements.
- **Vocabulary section:** capitalization habits and hashtag/emoji findings from mechanics 4, 6, and 7, written as rules ("no emoji, ever" rather than "0 emoji observed").
- **Never-do section:** the inverse of everything measured. If the creator never uses a platform CTA, that is a never-do line. If they never write in pure third person, that is a never-do line. This section is what keeps a future draft from drifting toward generic AI-caption habits the creator's own posts never show.

### 4.3 The guardrail slots, carried into every skill this recipe builds

Three guardrails are mandatory in `voice-skill-template.md`, not suggestions the user can skip:

1. **No literal sentence reuse.** The built skill must check every future draft against its own example posts using the three-word-sequence comparison demonstrated in `facebook-caption-writer/references/example-run.md` step 5: tokenize both texts, lowercase, strip punctuation, compare every three-word run in the draft against every three-word run in each example. Any match means rewrite that phrase before shipping. This is the Wave 1 lesson from this catalog's own build: a caption that reads like a match on a skim and shares whole phrases with its model is a copy, not a match, and the only check that catches it reliably is the mechanical one, not a self-read.
2. **The out-of-niche disclosure.** When a future topic has no evidence in the example posts and sits outside the niche those posts cover, the built skill says so before drafting, states plainly that it is applying structure with no content authority behind it, and labels the draft as untested territory. This guardrail exists because of what Section 5's third acceptance test finds, and it must ship in the template rather than be added later after a bad draft goes out under the creator's name.
3. **The 6-word originality guardrail**, this catalog's shared drafting backstop, sourced from `facebook-content-calendar-builder`'s rubric section 4.4: no draft reuses more than 6 consecutive words from any example post. Check it literally, sliding a 7-word window across the draft against every example post. The template is the structure; the nouns are new. (Working number, labeled: 6 is this catalog's shared threshold, not a platform fact. It sits just above the length of a common phrase and just below the length of a distinctive clause.) This sits alongside guardrail 1, not in place of it: the three-word check is the stricter of the two and catches a reused phrase early; the 6-word check is the coarser, catalog-wide floor every drafting skill in this catalog shares, kept here so this skill's output stays consistent with the others.

---

## Section 5: The 3-test acceptance run

**Do not hand over the two finished files without running this.** A voice skill that has never generated a single test draft is unverified, the same way a rubric that was never run against the synthetic data in this catalog would be unverified. Three tests, in this order:

### Test 1: a topic the creator covered

Pick a topic close to one of the style-source posts' subject matter, but not identical to any single post. Draft using the built skill's own rules. **What passing looks like:** the self-check from `facebook-caption-writer/references/rubric.md` section 4 (word count, rhythm band, hook length, line structure, emoji, hashtags, CTA behavior, capitalization, person voice, question-mark presence, no literal reuse) passes on all 11 items, and the draft's topic fit is native, meaning the example posts back it directly. This is the easiest test and it should pass clean. **Reconciling note, so this section and `voice-skill-template.md` do not disagree:** a single narrow miss on one item, disclosed in one line rather than hidden, is governed by `voice-skill-template.md`'s own self-check conclusion, not by this section, and still counts as PASS; two or more misses does not, and means the templates were filled wrong and the recipe needs to be re-run from Section 3, not patched at the draft level.

### Test 2: a topic the creator never covered, still inside their niche

Pick a topic with zero example posts behind it but that a reader of the account would find unsurprising. **What passing looks like:** the same 11-item self-check still passes, because the mechanics being tested are structural (rhythm, line breaks, capitalization, person voice), not topical, and a real voice skill transfers structure to a new subject without needing an example of that exact subject. If this test fails where Test 1 passed, the built skill has memorized specific posts instead of learning the pattern, and the templates need the example slots reworked to emphasize structure over content.

### Test 3: a topic outside the niche entirely

Pick a topic with no plausible connection to anything the creator's account covers. **This test is graded differently on purpose, and here is why: the mechanical self-check can pass this test even when the draft should not ship as written.** Word count, rhythm, and structure transfer to any subject; content authority does not. A drafted caption that confidently applies a home organizer's voice to, say, personal finance advice is structurally correct and substantively unearned, because nothing in the style-source set backs the creator's authority on that subject.

**What passing actually looks like for Test 3:** the built skill's out-of-niche disclosure guardrail (Section 4.3, item 2) fires before the draft, states plainly that this topic has no evidence behind it, and the draft itself is labeled as untested territory rather than shipped with the same confidence as Tests 1 and 2. **A draft that passes the 11-item mechanical check but ships with no disclosure has failed Test 3**, even though every mechanical box is checked, because the missing disclosure is the actual thing being tested. `example-run.md` shows this failing once, on the first attempt, and then shows the fix.

---

## Section 6: The maintenance habit

The source method for this whole catalog's build states it in one line: when an agent repeats a mistake, tell it once, and update the skill so it never happens again, because the skill file is the memory.

**Applied to the voice skill this recipe builds:** the first time a generated draft gets something wrong (a phrase that does not sound like the creator, a structural habit the measurement missed, a topic that needed the out-of-niche disclosure and did not get it), the fix is not "write it differently next time." The fix is opening `voice-skill-template.md` (now filled and installed) and adding one line to the relevant section: a never-do line in the style playbook, a correction to a voice-profile slot, an addition to the example set. **The skill only gets better if the correction lives in the file, not in the user's memory of having corrected it once.** State this to the user plainly at the end of every build: this is not a one-time artifact, it is a file you edit the first time it gets something wrong, and every edit compounds.
