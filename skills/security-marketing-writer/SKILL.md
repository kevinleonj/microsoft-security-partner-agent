---
name: security-marketing-writer
description: Writes and edits Microsoft 365 and Microsoft Security marketing content for European partners - LinkedIn posts, customer emails and short sequences, landing page and web copy, one-page plan fact sheets - composed in the reader's language and market register, with every product claim verified on official Microsoft pages and a claim ledger, compliance flags and sources after the asset. Use when the user asks to write, draft, rewrite or shorten a post, email, newsletter item, landing page, web text, one-pager or fact sheet, or asks for content "in German", "in Spanish", "for the Nordics" or any other market.
---

# Security marketing writer

This skill writes partner marketing about Microsoft Security that a sceptical European reader trusts. European IT buyers read enthusiasm as a warning sign; they respond to a specific fact, a named product, proof they can check and one clear next step. The defining rule: nothing the reader could catch as wrong, inflated or translated enters the asset. Claims are verified first, the text is composed in the reader's language and register, and the asset passes an eight-point gate before it is delivered.

## When to use

- If the user asks for a LinkedIn post, a customer email, a short email sequence, landing page copy, web text, a one-pager or a fact sheet about Microsoft 365 or Microsoft Security, use this skill.
- If the user pastes marketing copy and asks to improve, shorten or localise it, use this skill.
- If the content depends on a licensing recommendation, run `security-licensing-advisor` first and write from its verified result.

## Inputs

- The brief from the user's message: topic, reader, market and language, channel, the one action the reader should take.
- `references/04-marketing-playbook.txt`: readers, claim statuses, structures per format, European register by market, composing in the market language, words and patterns to remove, Microsoft naming and trademark rules, email consent patterns, personalisation, Article 50 of the EU Artificial Intelligence Act, works council rules, regulation hooks, data residency.
- `references/08-worked-examples.txt`: complete examples at the expected depth, including a LinkedIn post and a German customer email.
- `references/03-security-product-map.txt`: plain-language product explanations for the body copy.
- The `verify-microsoft-sources` skill for every product claim.

## Procedure

1. **Settle the brief.**
   - Goal: know who reads, in which language, and what they should do.
   - Action: identify the reader (customer or peer, role, company size), the market and language, the channel, the one action and the success measure (reply, booked call, click, comment). If two of these are missing and cannot be inferred, ask once, listing all missing items. Otherwise state the assumption and proceed.
   - Transition: go to step 2.

2. **Build the claim ledger before drafting.**
   - Goal: decide what may be said.
   - Action: list every factual claim the asset will make: product contents, plan names, prerequisites, numbers, dates, regulations. Verify each with `verify-microsoft-sources`. Statuses: verified, user-supplied, not confirmed, contradicted. Only verified and user-supplied claims enter the asset. A not-confirmed claim stays out and becomes a `[needs input: ...]` item after the asset. A contradicted claim is replaced by the verified fact, and the user is told.
   - Transition: go to step 3.

3. **Draft in the target language and register.**
   - Goal: a send-ready asset.
   - Action: use the structure for the format from `references/04-marketing-playbook.txt`.
     - LinkedIn post: first line carries the point; 80 to 200 words, up to 300 for a lesson with steps; paragraphs of two to four sentences; evidence; a stated boundary; close with a question a peer can answer from experience or one concrete next step; three hashtags at most.
     - Customer email: three subject lines under 50 characters; one preheader; opening that says who writes and why; the customer's situation, then the mechanism with exact product names; proof; what is not included; one call to action; footer placeholders for sender, address and unsubscribe.
     - Landing page: outcome headline under ten words; mechanism subheading; problem; what the partner does; included and not included; proof; one call to action with consent wording.
     - Fact sheet: exact plan name; required base plan; what it adds; what it does not include; who it fits; how the partner deploys it; the confirming Microsoft page.
     - Compose directly in the target language, with the market's address form: formal "Sie" in Germany, Austria and Switzerland; formal and warm in Spain, Italy and Portugal; relationship-first "vous" in France; short with first names in the Nordics and the Netherlands; direct with understatement in the United Kingdom and Ireland.
     - Full Microsoft product names on first mention, exactly as Microsoft writes them; never "M365"; every acronym expanded on first use in body copy.
     - Partner-side items go in square brackets: [partner name], [logo], [booking link], [postal address], [unsubscribe link], [designation badge, only if held].
   - Transition: go to step 4.

4. **Run the eight-point gate.**
   - Goal: remove the patterns that make copy read as generic or machine-written.
   - Action: read the draft sentence by sentence against these eight checks and fix each failure:
     1. Fragment then explain: a sentence of six words or fewer that only sets up the next one.
     2. Repeated shape: three or more consecutive sentences with the same opening word or structure.
     3. Colon reveal, "not X, it's Y", or "Not a. Not b. A c." patterns.
     4. Metadiscourse: sentences that tell the reader something is important or worth noting.
     5. Ending: a kicker line or a recap instead of the last concrete fact.
     6. Characters: any emoji, exclamation mark or em dash.
     7. Portability: a sentence that would fit any other vendor or partner unchanged.
     8. Claims: every fact verified or user-supplied.
   - Transition: go to step 5.

5. **Add compliance flags.**
   - Goal: tell the partner what to confirm before publishing or sending.
   - Action: one line per applicable item, using `references/04-marketing-playbook.txt`: the email consent pattern for the recipient's country, with the note that the national regulator decides; sender identity, postal address and unsubscribe present; open-tracking consent where relevant; images generated by artificial intelligence (AI) and the labelling test under Article 50 of the EU Artificial Intelligence Act; Microsoft trademark and logo use; works council or employee consultation when the content promotes features that can monitor employees in Germany or Austria; regulation hooks such as the Network and Information Security Directive 2 (NIS2) only after the national transposition status is confirmed. Write "none" when nothing applies.
   - Transition: go to step 6.

6. **Deliver.**
   - Goal: complete output in the contract below.
   - Action: deliver the asset first, then the blocks after it. If the user asked for variants, deliver exactly that number.
   - Transition: run the final check, then send.

## Output contract

Goal: a send-ready asset and the evidence behind it.
Format: the asset as plain text with labelled parts (subject lines, preheader, body for emails; headline, sections for pages); then labelled blocks.
Detail level: complete. No outline when finished text was asked for.
Sections, in order:
- The asset: no citations, status tags or notes inside it.
- Claim ledger: claim, status, source or missing document.
- Compliance flags: one line each, or "none".
- Not confirmed: every `[needs input: ...]` item and the document that would fill it.
- Sources: page title and full URL for every page opened.
- Gate line: "Gate: 8/8." or "Gate: 7/8, fixed <check> in <place>."
Include: what the plan does not include; the boundary of the claim.
Exclude: partner prices, promotion percentages, incentive rates and margins; statistics without a named source; invented customer stories or quotes; urgency without a real, sourced date.

## Resources in this skill

- `references/04-marketing-playbook.txt`: structures, register, naming, compliance patterns.
- `references/08-worked-examples.txt`: full-length examples of a licensing answer, a LinkedIn post, a German customer email and a script review.
- `references/03-security-product-map.txt`: product explanations in plain words.

## Final check

Confirm: the asset is in the target language and register; every claim inside it is verified or user-supplied; product names are complete and current; one call to action; the boundary is stated; the gate line is present; compliance flags are written. Revise, then send.
