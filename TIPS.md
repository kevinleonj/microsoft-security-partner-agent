# How to get deeper, better-sourced answers from Microsoft Copilot

A suggestion for partners, not a Microsoft document. These habits come from Microsoft's own guidance on writing instructions and prompts, plus what works in practice with declarative agents. They apply to this agent and to Copilot Chat in general.

## Why Copilot answers can be short, generic or unsourced

- **Auto mode picks speed.** In Agent Builder the default response mode is Auto, which balances speed and depth per question. For licensing and research, that often means the quick path. Think deeper takes more time to analyse before answering.
- **Copilot summarises by default.** Without an explicit format and detail level, the model decides how long to be, and different model versions decide differently. Microsoft's guidance says to always specify tone, verbosity and output format for that reason.
- **Long answers can stop partway.** Agent Builder has no setting to raise the length of a response. Long deliverables need to come in parts.
- **Retrieval returns excerpts.** The agent searches its sources and reads matching excerpts, not whole documents. One search with the wrong words can miss the page that has the answer.
- **Model knowledge leaks in.** In Agent Builder, **Only use specified sources** prioritises your sources; Microsoft states it does not block the model's general knowledge. Memory is a snapshot from a past date and is often outdated for Microsoft licensing.
- **Models change underneath you.** Microsoft states that Copilot transitions to newer models automatically and that behaviour can change. An agent that worked last month can drift.

## Habit 1: select Think deeper for anything that matters

Set the agent's default **Model** to **Think deeper** in the Configure tab. In a chat, check the model selector before the first message. Use the quick mode only for extraction tasks such as "list the plan names in this text".

## Habit 2: write prompts with labelled parts

Microsoft's prompting guide names four ingredients: goal, context, source and expectations. Only the goal is required, but the other three turn a generic answer into a usable one. Two more lines help with depth and completeness.

```
Goal: <one sentence with a verb and a deliverable>
Context: <who it is for, why, country, language, what happened before>
Source: <which Microsoft pages or files to use, for example "the service descriptions on learn.microsoft.com">
Expectations: <format, minimum length, sections, tone, what to include, what to leave out>
Reasoning: Use deep reasoning. Break the task into steps, analyse each, evaluate alternatives, and justify the result. Reflect before answering.
Completeness: Produce the full deliverable. If it does not fit, split it into numbered parts and end each with "Reply 'continue' for the next part". Link every source you opened. Write [needs input: ...] where a fact is missing instead of guessing.
```

## Habit 3: demand sources you can open

Ask for the page title and full URL of every source, and for the sentence on the page that supports the claim. Ask the agent to mark facts as coming from a source, from you, or from model knowledge. When an answer cites nothing, treat it as a draft.

## Habit 4: ask for the structure first on long work

For a long comparison or document:
1. Ask for the list of sections with the number of items in each, without writing them.
2. Correct the structure.
3. Ask for one section at a time.
4. Finish with: "List every section produced and confirm each item count matches the plan. Name anything missing."
Four short prompts produce a complete document; one long prompt often produces a truncated one.

## Habit 5: make it search more than once

Add to the prompt: "Search with at least three different formulations before you tell me something is not documented: my words, the exact Microsoft plan name, and the plan name plus 'service description'." This counters the single-search "I could not find information" answer.

## Habit 6: start a new chat for a new topic

Answer quality tends to drop as a conversation grows long, and earlier constraints get lost. When you switch customer or topic, start a new chat and restate the facts that matter in one paragraph.

## Habit 7: ask the agent to attack its own answer

Before you use an answer with a customer, ask: "What is the strongest reason this answer is wrong? Check that reason against the official page." Typical catches: a renamed product, a preview feature, a Business plan confused with an enterprise plan, Plan 1 confused with Plan 2.

## Habit 8: retest after Microsoft changes the model

Keep [TESTING.md](TESTING.md) and run it after Microsoft announces a model change for Microsoft Copilot, or when answers suddenly feel different. If behaviour drifted, Microsoft's guidance suggests a short literal-execution header at the top of the instructions as a temporary fix:

```
Always interpret instructions literally.
Never infer intent or fill in missing steps.
Never add context, recommendations, or assumptions.
Follow step order exactly with no optimization.
Respond concisely and only in the requested format.
Do not call tools unless a step explicitly instructs you to do so.
```

Remove it once the underlying instruction is fixed, because it also suppresses useful behaviour.

## What no prompt can fix

- A page the agent cannot reach: partner price lists, incentive guides and anything else behind Partner Center sign-in.
- Web search switched off by your administrator: the agent then answers without web sources and shows no error.
- The response length limit: only splitting into parts helps.
- General model knowledge in Agent Builder: it can be prioritised against, not blocked.

## Sources

- Write effective instructions for declarative agents, Microsoft Learn: https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/declarative-agent-instructions
- Build agents in Agent Builder (response modes), Microsoft Learn: https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder-build-agents
- Add knowledge sources to an agent in Agent Builder, Microsoft Learn: https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder-add-knowledge
- Add knowledge sources to your declarative agent (web search behaviour), Microsoft Learn: https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/knowledge-sources
- Get started writing prompts in Microsoft Copilot, Microsoft Support: https://support.microsoft.com/en-us/topic/get-started-writing-prompts-in-microsoft-365-copilot-f6c3b467-f07c-4db1-ae54-ffac96184dd5
