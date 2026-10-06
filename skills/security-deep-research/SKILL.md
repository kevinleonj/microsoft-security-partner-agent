---
name: security-deep-research
description: Researches Microsoft 365 and Microsoft Security questions that need more than one fact - comparisons of plans or products, what changed for a product or for partners, customer meeting briefings, regulation questions and overviews of what Microsoft documents about a topic - by splitting the question into sub-questions, searching official Microsoft pages in passes, cross-checking, and reporting findings with sources, conflicts and gaps. Use when the user asks to compare, research, brief, summarise what changed, give an overview, prepare a meeting, or asks a question that names several products, countries or customer situations.
---

# Security deep research

This skill handles questions that one search cannot answer. It works in passes: plan the sub-questions, search broad, narrow to the deciding page, cross-check, and report. The defining rule: every finding comes from an official page opened in this conversation, conflicts between pages are shown rather than smoothed over, and what the sources say is kept apart from what the agent concludes.

## When to use

- If the user asks to compare two or more plans, products or approaches, use this skill.
- If the user asks what changed, what is new, or what was announced for a product or for partners, use this skill.
- If the user asks for a briefing before a customer meeting, use this skill and then `security-licensing-advisor` for the recommendation part.
- If the user asks how a European regulation relates to Microsoft Security capabilities in a named country, use this skill.
- If the question is a single fact, use `verify-microsoft-sources` alone instead.

## Inputs

- The research question from the user's message, with its constraints: products, countries, customer type, time frame.
- `references/05-research-method.txt`: decomposition patterns, search sequence, triangulation, recency, separating source from interpretation, report shape, stop condition.
- `references/01-microsoft-source-map.txt`: the official page per topic and the known traps.
- The `verify-microsoft-sources` skill for claim statuses.

## Procedure

1. **Frame the question.**
   - Goal: research the right thing.
   - Action: restate the question in one sentence with its constraints. If a missing constraint would change the research substantially, such as the country for a regulation question or the customer's base plan for a briefing, ask one question listing what is missing. Otherwise state the assumption and proceed.
   - Transition: go to step 2.

2. **Split into sub-questions.**
   - Goal: cover the whole question with independent parts.
   - Action: write two to six sub-questions using the decomposition patterns in `references/05-research-method.txt`. Each sub-question must be answerable from official pages. Show the list at the start of the answer so the user sees the plan.
   - Transition: go to step 3.

3. **Search in passes for each sub-question.**
   - Goal: reach the deciding page for each sub-question.
   - Action:
     - Pass one, broad: the product or topic name alone.
     - Pass two, narrow: the exact plan or product name plus "service description", "licensing", "prerequisites", "what's new" or "announcement".
     - Pass three, primary page: open the page that settles the sub-question and record title, URL and the supporting sentences.
     - Pass four, cross-check: open one more official page that should agree, such as the family service description for a fact found on a plan page, or the Partner Center announcement for a change found on a blog.
     - For "what changed" questions, read the Partner Center announcements for the current and previous month, the product's "what's new" page and the relevant product blog. Derive the current month from the system date. A Microsoft fiscal year runs from 1 July to 30 June and is named after the year in which it ends.
   - Transition: go to step 4 when each sub-question has an answer or three failed searches.

4. **Triangulate and resolve conflicts.**
   - Goal: findings the user can rely on.
   - Action: mark each finding as confirmed on two official pages, confirmed on one, or found only on a blog or chart. When pages disagree, report both with links and prefer the higher-ranked source from `references/01-microsoft-source-map.txt`. Mark preview features as preview.
   - Transition: go to step 5.

5. **Separate findings from interpretation.**
   - Goal: the user knows what Microsoft says and what the agent concludes.
   - Action: write findings as attributed statements ("The Microsoft Defender service description lists ..."). Write implications for the user's situation in a separate section labelled as interpretation.
   - Transition: go to step 6.

6. **Write the report.**
   - Goal: complete report in the output contract.
   - Action: write every section in full. If the report will not fit in one response, split it into numbered parts and end each part with "Part k of N. Reply 'continue' for Part k+1." Stop researching when every sub-question has an answer or a reported gap; more searching after that adds length, not accuracy.
   - Transition: run the final check, then send.

## Output contract

Goal: a research report that answers the question and shows its evidence.
Format: labelled sections; a table for comparisons with more than three rows.
Detail level: complete. Every sub-question gets its own findings section.
Sections, in order:
- Answer: the conclusion in two to four sentences.
- Sub-questions: the list from step 2.
- Findings: one section per sub-question, each finding attributed to its page.
- Conflicts and gaps: disagreements between pages, facts not found, preview features.
- Implications (interpretation): specific to the user's situation, labelled as interpretation.
- Not confirmed: every `[needs input: ...]` item.
- Sources: page title and full URL for every page opened.
- Confidence: high, medium or low, with the single reason it is not higher.
Include: what sits behind partner sign-in and where the partner finds it.
Exclude: partner incentive rates and margins; forum posts and distributor blogs as evidence; unattributed statistics.

## Resources in this skill

- `references/05-research-method.txt`: the research method in full.
- `references/01-microsoft-source-map.txt`: official pages, source order, search patterns, traps.

## Final check

Confirm: every sub-question has findings or a reported gap; every finding is attributed to an opened page; conflicts are shown with both links; interpretation is labelled; sources list only pages opened; confidence has a reason. Revise, then send.
