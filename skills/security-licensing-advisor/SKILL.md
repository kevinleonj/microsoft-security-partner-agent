---
name: security-licensing-advisor
description: Answers Microsoft 365 and Microsoft Security licensing questions for partners and builds licensing recommendations with the stack, gap, path method - which plan or add-on includes a Microsoft Defender, Microsoft Entra, Microsoft Intune or Microsoft Purview capability, what a customer with a given licence mix is missing, how two plans differ, and what to propose before a renewal or a Microsoft 365 Copilot rollout. Use when the user asks "does Business Premium include", "what is the difference between", "what should we propose", "customer has E3, what next", "is this licensing correct", or describes a customer's licences and a security worry.
---

# Security licensing advisor

This skill turns a customer's current Microsoft licences and a stated risk into one recommended next step that a partner can defend in front of the customer. It is for partners selling to small and medium customers with mixed licensing: Microsoft 365 Business Basic, Business Standard, Business Premium, Microsoft 365 E3 and E5, with or without Microsoft 365 Copilot. The defining rule: the recommendation is the smallest licence change that closes the customer's stated risk, every entitlement in it is confirmed on the service description, and the answer says what the path still does not include.

## When to use

- If the user asks whether a plan includes a capability, use this skill.
- If the user asks how two plans or add-ons differ, use this skill.
- If the user describes a customer's licences and asks what to propose, use this skill.
- If the user pastes a licensing proposal or quote and asks whether it is correct, use this skill together with `technical-and-claim-review`.
- If the answer will become a customer email or a fact sheet, finish this skill first, then hand the verified result to `security-marketing-writer`.

## Inputs

- The customer facts from the user's message: plans, rough seat count, Microsoft 365 Copilot use, country, renewal month, other security vendors, the risk the customer worries about.
- `references/02-security-licensing-method.txt`: the method, the facts that change a recommendation, paths by base plan, coexistence framing, economics boundaries, answer shape.
- `references/03-security-product-map.txt`: what each product does in plain words and where its licensing is defined.
- `references/01-microsoft-source-map.txt`: which official page settles which licensing fact.
- The `verify-microsoft-sources` skill for every changeable claim.

## Procedure

1. **Collect the facts that change the answer.**
   - Goal: know enough to recommend without guessing.
   - Action: read the customer facts from the message. Ask at most three questions, and only for facts that would flip the recommendation: base plans and mix, seat band relative to the Business plan cap, Microsoft 365 Copilot yes or no, country, renewal month and term, other security vendors in place. When the user wants a quick answer, proceed with stated assumptions instead of asking.
   - Transition: go to step 2.

2. **Stack: write down what the customer licenses today.**
   - Goal: a precise starting point.
   - Action: list plan names exactly as Microsoft writes them, the rough seat count per plan, Copilot licences, and third-party tools. Flag mixed licensing: users on a lower plan lack per-user controls such as Conditional Access or endpoint protection.
   - Transition: go to step 3.

3. **Gap: find the missing capability for the stated risk.**
   - Goal: name the gap that matters, not every missing feature.
   - Action: translate the customer's worry into capabilities using `references/03-security-product-map.txt` (for example, "staff will find salary files through Copilot" becomes oversharing, sensitivity labels and Data Loss Prevention). Check the service description of the customer's current plan for each capability with `verify-microsoft-sources`. A capability the customer already owns but has not configured is a deployment gap, not a licensing gap; say so, because it changes the proposal.
   - Transition: go to step 4.

4. **Path: build two options and choose one.**
   - Goal: a defensible recommendation.
   - Action:
     - Option A: the smallest licence change, or a configuration project on licences already owned, that closes the gap.
     - Option B: the realistic alternative, often a broader suite or a different add-on.
     - For each option, confirm on the official page: the exact name, what it adds on top of which base plan, the prerequisites, and what it still does not include. Use `references/02-security-licensing-method.txt` for the documented paths by base plan.
     - Recommend one option and state why the other lost: cost, deployment effort, a missing prerequisite, mixed-licence complexity, or a mismatch with the stated risk.
     - When Microsoft Learn pages disagree on a name or content, report both pages and prefer the higher-ranked source.
   - Transition: go to step 5.

5. **Timing and economics.**
   - Goal: a proposal the partner can act on.
   - Action: tie the change to the customer's renewal date or Copilot rollout. When the renewal date is known, use code interpreter to compute the days until renewal and the Microsoft fiscal quarter it falls in (fiscal years run from 1 July to 30 June). Check the current new commerce rules for mid-term changes in the Partner Center documentation before promising one. Partner prices, promotion percentages, incentives and margins are not quoted, even when an opened page shows them; prices become `[needs input: partner price for <market>, from the partner's price list]`, and a promotion is named with its end date and official link. Before proposing a Microsoft Defender Suite for only some Business Premium users, state that Microsoft Learn says Defender for Business does not support mixed licensing, so the tenant stays on the Defender for Business experience until all users have Defender for Endpoint Plan 2.
   - Transition: go to step 6.

6. **Write the answer.**
   - Goal: complete answer in the output contract.
   - Action: write all sections in full. If the answer will not fit, split it into numbered parts and end each part with "Part k of N. Reply 'continue' for Part k+1."
   - Transition: run the final check, then send.

## Plan comparison requests

When the user asks how two plans or add-ons differ, build the comparison from the service descriptions, not from a chart. Structure: what both include; what only A includes; what only B includes; prerequisites of each; what neither includes; which customer situation fits each. Use a table when the comparison has more than three rows. Link each service description used.

## Output contract

Goal: a licensing recommendation or answer a partner can repeat to a customer without correction.
Format: labelled sections; a table for comparisons with more than three rows.
Detail level: complete. Both options are written out; no section is shortened to a single phrase.
Sections, in order:
- Answer: the recommendation in one or two sentences, with the exact plan or add-on name.
- Stack: what the customer has.
- Gap: the missing capability and the risk it leaves open.
- Path, option A (recommended): what it adds on top of which base plan, prerequisites, what it does not include.
- Path, option B: the alternative and why it lost.
- Timing: renewal or rollout moment, and any new commerce rule that applies.
- Not confirmed: every `[needs input: ...]` item.
- Sources: page title and full URL for every page opened.
- Confidence: high, medium or low, with the single reason it is not higher.
Include: deployment gaps on licences already owned; mixed-licence effects; coexistence with other vendors' tools.
Exclude: partner prices, promotion percentages, incentive rates, margins; United States list prices for European markets; preview features presented as available.

## Resources in this skill

- `references/02-security-licensing-method.txt`: stack, gap, path; the facts that change a recommendation; paths by base plan; Copilot and data security; renewal timing; coexistence; economics boundaries; answer shape.
- `references/03-security-product-map.txt`: plain-language product explanations, customer search words, licensing pages, common confusions.
- `references/01-microsoft-source-map.txt`: the official page per question and the known traps.

## Final check

Confirm: every section of the output contract is present; every plan and add-on name is current and complete; every entitlement has an opened service description or a `[needs input: ...]` marker; both options state what they do not include; the reason the losing option lost is stated; no partner economics figure appears. Revise, then send.
