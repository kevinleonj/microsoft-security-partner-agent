# Security Partner Assistant

A ready-to-build agent for Microsoft Copilot. You build it yourself in Agent Builder by copying and uploading the files in this repository. Your administrator decides whether Agent Builder, web search and sharing are available in your organisation.

**Contents:** [What it does](#what-the-agent-does) · [Choose your build](#choose-your-build) · [Download](#download) · [Set up](#set-up-in-agent-builder) · [Read the files](#read-the-files-before-you-upload) · [Limits](#what-the-agent-cannot-do)

## What the agent does

- **Licensing:** which plan or add-on includes a Microsoft Defender, Microsoft Entra, Microsoft Intune or Microsoft Purview capability, what a customer with a given licence mix is missing, and what to propose before a renewal or a Microsoft Copilot rollout.
- **Marketing:** LinkedIn posts, customer emails, landing page copy and one-page fact sheets, written in the reader's language and market register, with a claim check after each text.
- **Research:** plan comparisons, what changed for a product or for partners, and briefings before a customer meeting, with every finding linked to an official Microsoft page.
- **Review:** checks drafts, Copilot answers, PowerShell scripts, Kusto Query Language (KQL) queries, security configuration plans and licensing proposals, and returns a verdict with evidence and a corrected version.

You chat with the agent. Describe customers by plan, seat band and situation; it needs no names, contact details or exports from your customer relationship management (CRM) system.

## How it stays accurate

The model behind Copilot learned from a snapshot of the past, and Microsoft changes plan contents, product names and partner rules every month. The agent is built to look things up instead of remembering them:

- It searches four Microsoft sites only: Microsoft Learn, microsoft.com, the Microsoft Product Terms and Microsoft product blogs on Tech Community.
- It opens the official page for every fact that can change, links that page, and writes a needs-input marker when it finds nothing.
- Its knowledge files and skills hold methods, not prices or dates, so they do not go out of date when a price list changes.
- It reads today's date from the system and works out the Microsoft fiscal year from it.
- It never quotes partner prices, promotion percentages, incentive rates or margins. Those belong in Partner Center, behind your partner sign-in.

## Choose your build

Both builds create the same declarative agent: a version of Microsoft Copilot with its own instructions, sources and starter prompts. They differ in where the agent keeps its working methods.

| | Standard build | Skills build |
|---|---|---|
| What you upload | Instructions plus eight knowledge files | Instructions plus five skill packages |
| How the agent uses them | It searches the knowledge files when a question needs a method or a source | It opens the skill for the job in hand (licensing, marketing, research, review or verification) and follows that skill's full procedure |
| Who can build it | Anyone who can upload files in Agent Builder | Only organisations in the Microsoft Frontier Program, Microsoft's early-access programme |
| Status | Generally available features | Custom skills are in preview |
| Folder | [`download/standard-build`](download/standard-build) | [`download/skills-build`](download/skills-build) |

**What a skill is.** A skill is a folder with a `SKILL.md` instruction file and reference files, uploaded as one `.zip`. The agent loads a skill only when a request needs it, so one agent can follow five long procedures without crowding its main instructions.

**Why the builds are separate.** During the preview, Microsoft does not support an agent that has both skills and uploaded knowledge files. The skill packages therefore carry the knowledge files inside them.

**How to check whether you can use skills.** In Microsoft Copilot, select **Agents & Skills**, then **New agent**, then **Skip to configure**. If the Configure tab shows a **Skills** section, you can use the skills build. Skills are not available in tenants that use Microsoft Purview Information Barriers.

**If you cannot upload files**, use the standard build's instructions and skip the knowledge files. The agent then works from its instructions and the four Microsoft websites.

**Licences.** According to Microsoft Learn, uploaded knowledge files and skills need a Copilot licence or a tenant with pay-as-you-go billing enabled. Microsoft currently uses both the newer licence names (Microsoft Copilot, Microsoft Copilot Business) and the older ones (Microsoft 365 Copilot, Microsoft 365 Copilot Business). If you see no **New agent** option, your licence or your administrator's settings are the likely reason.

## Download

1. Select the green **Code** button on this page, then **Download ZIP**. GitHub downloads the whole repository; it has no option to download a single folder.
2. Unzip the file and open `download`, then the folder for your build. Everything in that folder goes into Agent Builder.

## Set up in Agent Builder

Agent Builder runs in Microsoft Copilot in a browser or in the Teams desktop and web apps. It is not available on mobile. The labels below are the ones Microsoft Learn documents.

**1. Open the Configure tab.** Select **Agents & Skills**, then **New agent**, then **Skip to configure**.

**2. Name.** You can rename the agent. Keep it short and avoid names that suggest Microsoft built it.

```
Security Partner Assistant
```

**3. Description.** Copilot uses it to decide when the agent applies.

```
Helps employees of Microsoft partners and resellers with Microsoft 365 and Microsoft Security work for small and medium customers in Europe. Answers licensing questions from official Microsoft sources with links: which plan or add-on includes a Microsoft Defender, Microsoft Entra, Microsoft Intune or Microsoft Purview capability, what a customer is missing, and what to propose before a renewal. Writes marketing content in the reader's language and European register, with a claim check: LinkedIn posts, customer emails, landing page copy and one-page fact sheets. Researches what Microsoft documents about a security topic and reviews drafts, Copilot answers, PowerShell scripts, Kusto Query Language (KQL) queries and licensing proposals for errors. Use for: does Business Premium include, what is the difference between, what should we propose, write a LinkedIn post about, write a customer email, check this text, review this script, what changed in Microsoft Defender.
```

**4. Model.** Select **Think deeper**. This is the most important setting. The default, **Auto**, often picks the faster mode and gives shorter, shallower answers.

**5. Instructions.** Open `instructions.txt` in your build folder, copy everything, and paste it.

**6. Knowledge, public websites.** Under **Knowledge**, use **Enter URL** and add these four, pressing Enter after each one.

```
https://learn.microsoft.com/en-us/
```
```
https://www.microsoft.com/en-us/
```
```
https://www.microsoft.com/licensing/
```
```
https://techcommunity.microsoft.com/blog/
```

**7. Knowledge, toggles.** Turn **Search all websites** off and **Only use specified sources** on. Turn **Reference people in organization** off; the agent does not need colleague profiles.

**8. Your build's files.**
- Standard build: upload all eight files from `download/standard-build/knowledge`. Wait until none of them shows as preparing before you test.
- Skills build: expand **Skills**, select **Add**, and upload each file from `download/skills-build/skill-zips`, one at a time. Upload the `.zip` as it is; do not unzip it.

**9. Capabilities.** Turn **Create documents, charts, and code** on. Leave **Create images** off unless you want generated images.

**10. Starter prompts.** Add these six. Each has a title and a prompt; edit the parts in square brackets when you use them.

Licence gap check
```
Customer has [plan] for [number] users, [with or without] Microsoft Copilot, in [country]. Which security capability are they missing, and what should we propose before their renewal in [month]?
```
Compare two plans
```
What is the difference between Microsoft Defender for Business and Microsoft Defender for Endpoint Plan 2? Use the service descriptions and link them.
```
LinkedIn post
```
Write a LinkedIn post for our company page about [topic], in [language], for IT leads at small companies. Include the claim ledger.
```
Customer email
```
Write an email to a customer in [country] on [plan] with [number] users, offering a security licence review before renewal. Formal register, in the customer's language.
```
Check my draft
```
Check this text for outdated Microsoft product names, unverified claims, missing plan prerequisites and hype: [paste text]
```
What changed this month
```
What changed for Microsoft partners in Microsoft Security this month and last month? Use the Partner Center announcements and the Microsoft Security blog, and leave out partner incentive and margin figures.
```

**11. Test.** Open the **Try it** tab and run at least tests 1, 2, 3 and 7 from [TESTING.md](TESTING.md). If an answer has no sources or invents a price, check the model setting, the four websites and that the instructions were pasted completely.

**12. Create and share.** Select **Create**; the agent is private until you share it. Select **Share** and add colleagues with **Can chat**, or co-owners with **Can edit**. Colleagues need a licence that covers the agent's capabilities. Everyone who can use the agent sees answers based on its uploaded files; the files in this repository contain nothing confidential, so keep it that way if you add your own.

## Read the files before you upload

**Instructions**
- [Standard build instructions](download/standard-build/instructions.txt)
- [Skills build instructions](download/skills-build/instructions.txt)

**Skills** (the zips in `download/skills-build/skill-zips` contain each `SKILL.md` plus the reference files listed)

| Skill | What it does | Reference files in the zip |
|---|---|---|
| [verify-microsoft-sources](skills/verify-microsoft-sources/SKILL.md) | Checks every fact that can change against official Microsoft pages and gives each claim a status | 01, 07 |
| [security-licensing-advisor](skills/security-licensing-advisor/SKILL.md) | Builds licensing recommendations from what the customer already owns and compares plans from the service descriptions | 01, 02, 03 |
| [security-marketing-writer](skills/security-marketing-writer/SKILL.md) | Writes posts, emails, web copy and fact sheets in the reader's language, checks them for generic phrasing and adds compliance notes | 03, 04, 08 |
| [security-deep-research](skills/security-deep-research/SKILL.md) | Splits a question into sub-questions, searches official pages, cross-checks and reports conflicts and gaps | 01, 05 |
| [technical-and-claim-review](skills/technical-and-claim-review/SKILL.md) | Reviews drafts, scripts, queries, configuration plans and proposals with evidence for each finding | 01, 04, 06 |

**Knowledge files** (the eight files you upload in the standard build)

1. [01 Microsoft source map](download/standard-build/knowledge/01-microsoft-source-map.txt): which official page answers which licensing question, and the known traps
2. [02 Security licensing method](download/standard-build/knowledge/02-security-licensing-method.txt): stack, gap, path; paths by base plan; renewal timing
3. [03 Security product map](download/standard-build/knowledge/03-security-product-map.txt): what each Microsoft Security product does, in plain words
4. [04 Marketing playbook](download/standard-build/knowledge/04-marketing-playbook.txt): post and email structures, European register by market, compliance patterns
5. [05 Research method](download/standard-build/knowledge/05-research-method.txt): how a research question is split, searched and reported
6. [06 Review checklist](download/standard-build/knowledge/06-review-checklist.txt): checks for drafts, scripts, configurations and proposals
7. [07 Glossary](download/standard-build/knowledge/07-glossary.txt): licensing and security terms with German, French and Spanish equivalents
8. [08 Worked examples](download/standard-build/knowledge/08-worked-examples.txt): complete answers that show the expected depth

## Get better answers

[TIPS.md](TIPS.md) explains why Copilot answers can be short or unsourced and what to do about it: choose **Think deeper**, write prompts with a goal, context, source and expectations, ask for the structure first on long work, and start a new chat for a new topic.

## What the agent cannot do

- Read Partner Center price lists, incentive guides or anything else behind partner sign-in.
- Connect to MCP (Model Context Protocol) servers such as the Microsoft Learn MCP server. Agent Builder does not support them; Copilot Studio and the Microsoft 365 Agents Toolkit do, with more setup.
- Fully block the model's general knowledge. Agent Builder can prioritise your sources but not block the model, so the agent marks where each fact came from.
- Raise the length limit of a single response. The agent splits long work into numbered parts instead.
- Use the web if your administrator has switched off web search for Copilot. The agent shows no error in that case; test 11 in [TESTING.md](TESTING.md) checks for it.
- Replace the service description, the Product Terms or your licensing specialist for contractual questions.

## Customising

Rename the agent, or add your own services and markets to the marketing playbook (`04-marketing-playbook.txt`) and re-upload it. Write additions as facts, not commands; Copilot treats knowledge files as reference material and may ignore commands inside them. The skill zips contain copies of the knowledge files, so for the skills build, replace the matching file in the zip's `references` folder too.

## Licence

MIT, see [LICENSE](LICENSE).
