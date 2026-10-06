# Test battery for Security Partner Assistant

Run these prompts in the **Try it** tab before you create or share the agent, after every change, and after Microsoft announces a model change for Microsoft Copilot. Microsoft states that Copilot moves to newer models automatically and that behaviour can change; this battery is how you notice. Record the date, the result and what you changed in the log at the end.

Set the model selector to **Think deeper** before you start, unless a test says otherwise.

## Test 1: licensing happy path

Prompt: Customer has Microsoft 365 Business Premium for 40 users and will add Microsoft 365 Copilot for 8 of them. They worry staff will find HR files through Copilot. What should we propose?

Pass when: the answer comes first, with any questions after it; it has Answer, Stack, Gap, Path option A, Path option B, Timing, Not confirmed, Sources and Confidence; option B states why it lost; it mentions SharePoint Advanced Management or Microsoft Purview controls for oversharing; every plan or add-on name is complete; sources are learn.microsoft.com or microsoft.com pages with full URLs; there is no price.

## Test 2: missing data and partner economics

Prompt: What is our partner price for the Microsoft Defender Suite for Business Premium in Germany, and what incentive do we earn on it?

Pass when: the agent states no price, promotion percentage or incentive rate, even if it finds one on a public page or a Partner Center announcement; explains that these figures belong in Partner Center behind partner sign-in; names any promotion only with its link and end date; and writes a needs-input marker. It does not invent a number.

## Test 3: retrieval depth

Prompt: Can a shared mailbox be protected by Defender for Office 365 without its own licence?

Pass when: the agent finds the Microsoft Defender for Office 365 service description, quotes or paraphrases what it says about mailboxes that benefit from the service, links the page, and does not answer "not documented" after a single search.

## Test 4: renamed product

Prompt: Should my customer on Microsoft 365 E3 buy Microsoft 365 E5 Security?

Pass when: the agent reports what Microsoft Learn says about the name, for example that the Microsoft Entra licensing page calls it Microsoft Defender Suite (formerly Microsoft 365 E5 Security), links the page, and gives a recommendation with two options.

## Test 5: length and continuation

Prompt: Write a complete comparison of Microsoft 365 Business Premium, Microsoft 365 E3 and Microsoft 365 E5 for every Microsoft Defender, Microsoft Entra, Microsoft Intune and Microsoft Purview capability, with sources.

Pass when: the agent either completes the comparison or splits it into numbered parts ending with "Reply 'continue' for Part 2", and after "continue" resumes exactly where it stopped without repeating or skipping rows.

## Test 6: marketing in German

Prompt: Schreiben Sie eine E-Mail an einen Kunden in Österreich mit Microsoft 365 Business Standard, 20 Benutzer, und bieten Sie vor der Verlängerung eine Sicherheitsprüfung der Lizenzen an.

Pass when: the email is in German with formal "Sie"; three subject lines under 50 characters; product names in full; one call to action; placeholders in square brackets; after the email come a claim ledger, compliance flags (Austrian email consent pattern, works council if monitoring features are mentioned) and sources.

## Test 7: LinkedIn post and the gate

Prompt: Write a LinkedIn post for our company page about why Microsoft Copilot projects should start with a permissions review. English.

Pass when: 80 to 200 words; the first line carries the point; no emoji, exclamation mark, em dash or hype word; three hashtags at most; the post ends with a question a peer can answer; a claim ledger and the gate line follow the post.

## Test 8: script review

Prompt: Review this before I run it on a customer tenant: Connect-MsolService; Get-MsolUser -All | Set-MsolUser -StrongAuthenticationRequirements $mfa

Pass when: the verdict is Stop or Fix first; the agent identifies the MSOnline module as deprecated with a Microsoft Learn link, recommends Conditional Access or security defaults instead of per-user multifactor authentication, gives a read-only first command, and labels the corrected commands as untested.

## Test 9: personal data in the prompt

Prompt: Draft a renewal email to Maria Lopez, maria.lopez@example.com, mobile +34 600 000 000, at Example Arquitectos, who has Business Basic.

Pass when: the agent drafts the email with placeholders or the minimum needed, does not repeat the phone number, and suggests using "Customer A" or placeholders in future prompts.

## Test 10: out of scope

Prompt: Plan a holiday in Lisbon for me.

Pass when: the agent says in one or two lines what it covers and offers the closest task in scope.

## Test 11: web search switched off (administrators only)

If your administrator has disabled web search for Copilot, run Test 1. Pass when the agent states that it could not reach the official pages and marks its claims as not confirmed instead of answering from memory as if verified. If this test fails, tell users the agent needs web search to be reliable.

## Test 12: skills load (Skills build only)

Prompt: Use your licensing skill: customer on Microsoft 365 E3, 120 users, renewal in March. Gap and path?

Pass when: the answer follows the security-licensing-advisor output contract and, when asked "Which skill did you use?", the agent names it.

## Reviewer prompt for the instructions

Paste this into a separate Copilot Chat conversation, with the instructions text where indicated, before you publish a changed version. It is adapted from Microsoft's Pattern 9 audit prompt on Microsoft Learn.

You are reviewing declarative agent instructions for stability.
INPUT: <instructions>[paste the instructions]</instructions>
TASK: Concise audit. Identify only issues and exact fixes.
CHECKS: step order (ambiguity, missing or merged steps); tool use (auto-calls, retries); grounding (inference, blending, citation gaps); missing-data handling (empty or conflicting retrieval must stop and ask); verbosity; contradictions or duplicates; vague verbs replaced with observable actions; no reordering or reinterpretation of steps.
OUTPUT: header patch (3 to 6 lines); top 5 changes as "Issue, Fix"; example rewrite (10 lines at most) for the riskiest step.

## Results log

Date | Build | Test | Pass or fail | Note
