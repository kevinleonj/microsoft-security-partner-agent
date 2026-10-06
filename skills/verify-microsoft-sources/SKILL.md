---
name: verify-microsoft-sources
description: Verifies every fact that can change about Microsoft 365, Microsoft Security and Microsoft partner programs against official Microsoft pages before the agent states it. Use it in every job that names a plan, product, add-on, price, promotion, date, limit, requirement, designation rule or product name, and whenever the user asks "is this true", "does X include Y", "is this still current", "check this claim" or "what is the official source".
---

# Verify Microsoft sources

This skill stops the agent from answering Microsoft licensing and product questions from memory. Model memory is a snapshot from a past date, and Microsoft changes plan contents, names, prices and partner rules every month. Memory feels as confident about an expired fact as about a current one. The defining rule: a fact that can change reaches the user only after the agent opened the official Microsoft page that states it in this conversation, and the answer links that page.

## When to use

- If a response will name a Microsoft plan, add-on, product, feature, price, promotion, date, limit, requirement or partner programme rule, use this skill before writing the response.
- If the user asks whether a claim is true or current, use this skill.
- If another skill asks for verification, use this skill and return the claim statuses to that skill.

## Inputs

- The claims the response is about to make, taken from the user's question, the user's draft, or the agent's own draft.
- Today's date from the system context.
- `references/01-microsoft-source-map.txt` for which page answers which question and the known traps.
- `references/07-glossary.txt` for term expansions and the German, French and Spanish equivalents users type.

## Procedure

1. **Anchor time.**
   - Goal: work from today, not from the training snapshot.
   - Action: read today's date from the system context. When the question involves fiscal periods, renewals or "this year", derive the Microsoft fiscal year: it runs from 1 July to 30 June and is named after the year in which it ends. Use the current year in search queries when a year is relevant.
   - Transition: go to step 2.

2. **Sort the claims.**
   - Goal: decide which claims need a search.
   - Action: split the response into claims and give each one a class.
     - Stable: how a technology works in principle, definitions, settled history. Answer from knowledge and mark it [model knowledge].
     - Changeable: plan contents, product names, prices, promotions, dates, limits, prerequisites, designation rules, availability, preview status. Search and open the official page.
     - User-world: the customer's plans, seat count, country, renewal date, budget, existing tools. Ask the user or take it from the message; never fill it from a typical case.
   - Transition: go to step 3 with the list of changeable claims.

3. **Search broad, then narrow, then open the page.**
   - Goal: reach the page that settles each changeable claim.
   - Action: for each changeable claim:
     - First search: the product or topic name alone, to see which official pages exist.
     - Second search: the exact plan name plus "service description", "licensing", "prerequisites" or "what's new".
     - Third search, when the first two fail: the user's own words, a former product name, or the term in English if the user wrote in another language.
     - Open the page that settles the claim. Read the relevant section. Record the page title, the full URL and the sentence that supports the claim.
     - Read the en-us version as the reference. Write the answer in the user's language.
   - Transition: go to step 4 when every changeable claim has either a supporting sentence or three failed searches.

4. **Rank the sources and resolve conflicts.**
   - Goal: decide which page wins when pages disagree.
   - Action: apply the source order from `references/01-microsoft-source-map.txt`:
     - Rank 1: Microsoft Product Terms for rights and prerequisites.
     - Rank 2: service descriptions on Microsoft Learn for plan contents.
     - Rank 3: product documentation on Microsoft Learn for how features work.
     - Rank 4: Microsoft product blogs for announcements and renames.
     - Rank 5: plan pages, pricing pages and comparison charts, only to find a fact that a higher rank confirms.
     - Not sources: forum posts, distributor blogs, training sites, partner decks, model memory.
     - When two official pages disagree, state both with their links and say which ranks higher. A typical cause is a rename that one page has not caught up with.
   - Transition: go to step 5.

5. **Give every claim a status.**
   - Goal: make the evidence visible.
   - Action: assign one status per claim.
     - Verified: an official page opened in this conversation states it.
     - User-supplied: the user provided it, such as their own price list, event date or customer situation. Check it against official pages for contradictions.
     - Not confirmed: no official page found after three searches. It becomes `[needs input: what is missing and where the user can find it]`.
     - Contradicted: an official page says otherwise. Replace it with the verified fact and tell the user what changed.
   - Transition: go to step 6.

6. **Challenge the answer before sending.**
   - Goal: catch the most likely error.
   - Action: state to yourself the strongest reason the answer could be wrong, such as a rename, a preview feature, a Business versus enterprise plan mix-up, or a Plan 1 versus Plan 2 confusion. If that reason holds, fix the answer. Recompute every number. If the user pushes back without new evidence, keep the verified answer and show the source again; change it when new evidence arrives.
   - Transition: return the result to the calling job, or deliver it with the output contract below.

## Partner economics rule

Partner prices, promotion terms, incentive rates and margin constructs sit behind partner sign-in in Partner Center. The agent states none of these figures, even when an opened page such as a Partner Center announcement shows one, and points the user to the Partner Center area where the partner reads them. A promotion is named with its end date and a link to the official page that announces it. A list price from a public Microsoft page is stated only for the market that page shows, with its currency, commitment term, billing plan and link.

## Output contract

Goal: an answer whose evidence the user can check in under a minute.
Format: prose with labelled blocks.
Sections, in order:
- Answer: direct, first, no preamble.
- Basis: which parts were verified today on official pages, which come from the user, which are model knowledge.
- Not confirmed: each missing fact as `[needs input: ...]`.
- Sources: page title and full URL for every page opened; only pages actually opened.
- Confidence: high, medium or low, and the single reason it is not higher.
Include: conflicts between official pages, with both links.
Exclude: pages not opened, partner economics figures, preview features presented as available.

## Resources in this skill

- `references/01-microsoft-source-map.txt`: the official page for each licensing question, the source order, search patterns and known traps.
- `references/07-glossary.txt`: terms, expansions and German, French and Spanish equivalents.

## Final check

Confirm: today's date came from the system; every changeable claim has a status; every verified claim has an opened page with title and URL; every not-confirmed claim is a `[needs input: ...]` marker; no partner economics figure appears; confidence has a reason. Revise, then send.
