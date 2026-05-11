---
title: Agent Studio (Beta)
devrev_id: ART-26058
parent_directory: Agent Studio
translation_group: LhjCUxm2
modified_date: "2026-04-22T00:28:57.784Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/LhjCUxm2"
tags: []
top_category: Computer by DevRev
wiki_match: features/stock-objects
match_score: 0.467
last_updated: 2026-05-11
---

# Agent Studio (Beta)

Agent Studio is in beta. Functionality described in this article reflects the current beta release.

Agent Studio is [Computer](https://app.devrev.ai) interface for building, testing, and monitoring AI agents. An AI agent is an automated assistant that can understand natural language, search your workspace's knowledge, and take actions on behalf of users.

Unlike simple chatbots that follow rigid scripts, agents in Agent Studio are goal-driven. You define what the agent should accomplish and how it should behave, and the agent uses its configured knowledge and skills to determine the best way to respond to each interaction.

To access Agent Studio, go to [**Agent Studio**](https://app.devrev.ai/agent-studio) in the DevRev app.

## Agent lifecycle

Agent Studio is organized around three phases that form a continuous improvement loop:

![agent-lifecycle.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/12351744&key=2d806031578000a45e22ac590e9a5d7dd700c5acfbbd6ba39a50be38134a81f8)

**Build**

The Build phase is where you define your agent's identity and capabilities. You set a goal, attach knowledge sources and skills, establish guardrails, and write detailed instructions. This is the creative, configuration-heavy phase.

**Test**

The Test phase lets you validate your agent before putting it in front of real users. You can have ad-hoc conversations through the Playground, or run structured bulk tests against datasets of pre-defined inputs and expected outputs. Testing catches issues early and gives you confidence before publishing.

**Observe**

The Observe phase provides visibility into how your agent performs in the real world. Analytics dashboards show aggregate metrics, while session traces let you drill into individual conversations to understand exactly what the agent did and why. Observations from this phase drive the next round of improvements back in Build.

## Agent configuration

An agent's configuration is built from five distinct elements that work together: goal, knowledge, skills, guardrails, and instructions.

### Goal

The goal is a high-level statement of purpose that answers the question "What is this agent for?" The goal orients the agent's behavior across all interactions. A well-written goal is specific enough to guide decisions but broad enough to handle varied requests.

**For example:** Help customers troubleshoot product issues by searching the knowledge base, and escalate to a human agent when the issue cannot be resolved.

### Knowledge

Knowledge sources tell the agent what it knows. When a user asks a question, the agent searches the configured knowledge sources to find relevant information. You select which DevRev object types the agent can search — articles, tickets, conversations, and more.

The agent does not memorize your data. Instead, it searches knowledge sources in real time, which means it always works with the latest information available.

### Skills

Skills tell the agent what it can do. Without skills, an agent can only answer questions. With skills, it can take action, creating tickets, updating issues, sending messages, or running custom workflows.

There are three types of skills:

* **Tools**: Built-in DevRev actions with configurable parameters. Each operation has input fields that the agent can auto-fill based on conversation context, or that you can set to fixed values.
* **NL Skills**: Natural Language Skills that act as sub-agents with their own plan-based reasoning. An NL Skill receives a natural-language objective, decomposes it into steps, and executes those steps autonomously. Use NL Skills when the task requires multi-step reasoning or dynamic decision-making that goes beyond a single tool call.
* **Workflows**: Custom automation sequences built in DevRev. These represent more complex multi-step processes that follow a predetermined sequence of actions.

When the agent determines that an action is needed, it selects the most appropriate skill, fills in the required parameters, and executes it.

Skills run under the **Execute as User** permission model: the agent performs actions with the permissions of the user it is acting on behalf of, ensuring that existing access controls are respected.

Agents can also connect to external systems through the **Model Context Protocol (MCP)**, extending their capabilities beyond built-in DevRev actions.

### Guardrails

Guardrails define the agent's boundaries — what it must or must not do. They are safety rules that override other behavior. Every agent starts with a default guardrail that is always active.

The guardrail type available is `topic_boundary`, which constrains the agent to respond only within defined topics. For example:

* Never disclose internal employee information.
* Always verify the customer's identity before making account changes.
* Do not process refunds over $500 without escalating to a manager.

Guardrails are evaluated on every interaction. Guardrail configuration is API-only; you create and manage guardrails through the DevRev API rather than the Agent Studio UI.

### Instructions

Instructions are your detailed playbook for the agent. While the goal sets the direction and guardrails set the boundaries, instructions fill in everything in between, tone, style, escalation procedures, edge-case handling, and preferred responses.

Instructions support rich text and can reference specific knowledge sources, tools, or skills using `@` mentions. This lets you create precise, context-aware guidance.

## Versioning

Agent Studio uses a draft-and-publish versioning model. You can make changes to your agent without affecting the live version.

### Version lifecycle

![version-lifecycle.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/12351805&key=e2d2ede13271c7651ef1eb0d7e47971ab05751bea747395bc6e5c9f968d00e44)

* **Draft**: A work-in-progress version. You can freely edit a draft. Only one draft can exist at a time.
* **Published (Live)**: The active version that serves real users. Publishing a new version automatically archives the previous one.
* **Archived**: A previous version that is no longer active but is preserved for history.

### Automatic draft creation

When you edit any field on a published agent, Agent Studio automatically creates a new draft version. You do not need to manually create a draft, start editing and the system handles it. This ensures the live version remains untouched until you explicitly publish.

### Restoring previous versions

If a new version introduces problems, you can restore any previous version. Restoring creates a new draft with the selected version's configuration, which you can then review and publish. The original version history is preserved, nothing is overwritten.

Versioning provides a safety net: you can experiment freely in drafts, knowing that your live agent is not affected. It also provides an audit trail so you can see who changed what and when, and understand how your agent evolved over time.

## Testing approaches

Agent Studio provides two complementary testing approaches.

### Preview testing (Playground)

The Playground is an interactive chat panel for real-time conversations with your agent. It is suited for exploratory testing, verifying that skills work correctly, checking responses to specific inputs, or evaluating tone and style. Each Playground conversation creates a session you can revisit later, including an execution trace that shows how the agent processed each request.

### Bulk testing

Bulk testing provides structured, repeatable evaluation. You create datasets containing input–output pairs, then run your agent against the entire dataset at once. The system evaluates each response using configurable evaluators:

* **Correctness** — Whether the agent's response accurately addresses the input.
* **Completeness** — Whether the response fully covers what was expected.
* **Task Success** — A score from 0.0 to 1.0 measuring whether the agent accomplished the intended task.
* **Accuracy/Faithfulness** — A score from 1 to 5 measuring how faithfully the response reflects the source knowledge.

Bulk testing is especially valuable when you are about to publish a new version and want to verify it does not regress, when you have changed instructions or skills and want to measure the impact, or when you need to demonstrate agent quality to stakeholders.

## Observability and analytics

Once your agent is live, the Observe tab provides two views into its performance.

### Analytics

The Analytics dashboard shows aggregate metrics over time, including conversation volume, Task Success, and Accuracy/Faithfulness scores. This serves as a high-level health check for your agent. Analytics must be explicitly enabled for each agent. Once enabled, metrics are collected automatically and displayed on a dashboard that you can filter by time range.

### Sessions

The Sessions view shows individual conversations between your agent and real users. Each session includes:

* **Trigger** — What initiated the conversation.
* **Members** — Who participated.
* **Timestamps** — When the conversation happened.
* **Session trace** — A step-by-step breakdown of the agent's reasoning, including which skills it invoked, what knowledge it retrieved, guardrail evaluations, and the final response.

Session traces are invaluable for debugging unexpected behavior. When a user reports a problem, you can find their session, follow the agent's thought process, and identify exactly where things went wrong.

## Internal vs. external agents

Agent Studio supports two access levels for agents:

* **Internal agents** — Intended for internal teams, assisting employees with internal workflows, knowledge retrieval, and operational tasks. Internal agents are coming soon.
* **Customer experience agents** — Designed for customer-facing interactions. These agents interact directly with your customers through support channels. Supported channels: Slack, WhatsApp, Plug Chat, and Email.

The access level determines the agent's scope of visibility and the channels it can operate in. Choose the appropriate type when creating a new agent based on who interacts with it.

## Key concepts summary

| Concept | Purpose |
| --- | --- |
| **Goal** | High-level statement of what the agent should accomplish |
| **Knowledge** | Data sources the agent can search for information |
| **Skills** | Actions the agent can perform (tools + workflows) |
| **NL Skill** | A natural-language skill that maps user intents to specific agent actions |
| **Guardrails** | Safety rules and boundaries the agent must follow |
| **Instructions** | Detailed behavioral guidance and playbook |
| **Version** | A snapshot of the agent's configuration (Draft → Live → Archived) |
| **Dataset** | A collection of test inputs and expected outputs for bulk testing |
| **Evaluators** | Automated checks (Correctness, Completeness, Task Success, Accuracy/Faithfulness) applied to bulk test results |
| **Session** | A single conversation between the agent and a user |
| **Session Trace** | A step-by-step record of the agent's reasoning, skill invocations, and guardrail evaluations within a session |

## Source
- DevRev support article [Agent Studio (Beta)](https://support.devrev.ai/en-US/devrev/article/LhjCUxm2) (ART-26058)
