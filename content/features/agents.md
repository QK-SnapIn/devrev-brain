---
title: AI Agents
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_agents.jsonl, raw/docs/devrev-developer-docs.md, raw/docs/devrev-agent-dump-agents.md]
related: []
last_updated: 2026-04-12
---

# AI Agents

## What it does
The AI Agents feature provides a comprehensive platform for creating, deploying, and managing AI-powered agents within DevRev. It covers agent lifecycle management (create, update, delete, deploy), agent versioning, skills management (create, update, parse, config overrides), memories (knowledge storage with bundle strategies), plans, sessions, events (sync/async execution, signals), suggestions, templates, callbacks, and AI assistant surfaces. With 1107 test cases, it is a major feature area covering the intelligent automation layer of DevRev.

## Why it exists
DevRev aims to augment human workflows with AI agents that can automate customer support, internal tasks, and development processes. This feature enables organizations to define, configure, version, and deploy AI agents with customizable skills and memories, providing intelligent assistance across the platform.

## Key behaviors
- **Agent CRUD**: Create, get, list, update, delete AI agents
- **Agent deployment**: Deploy agents to activate them in production
- **Agent versioning**: Create, get, list, update, delete, update-state for agent versions
- **Skills management**: Create and update skills; parse skills to validate them (returns `is_valid: true/false` rather than HTTP errors for invalid skills)
- **Skill config overrides**: CRUD for overriding default skill configurations per agent; 404 on double-delete (idempotency boundary)
- **Memories**: CRUD for agent memories with `strategy` field (asymmetric: request takes integer, response returns enum-value object with id/label/ordinal)
- **Plans**: CRUD for AI agent plans
- **Sessions**: Create, get, list agent sessions
- **Events**: Execute events synchronously or asynchronously; signal events
- **Suggestions**: Get agent suggestions
- **Templates**: Instantiate agents from templates
- **Callbacks**: Handle agent callbacks
- **Configs**: List agent configurations
- **AI assistant surfaces**: Register, deregister, get assistant surfaces
- **Recommendations**: Suggest parts based on AI analysis
- **Nullable-update pattern**: Sending `null` for `ai_agent_config` triggers field mask unset

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- All endpoints under `ai-agents.*`, `ai-agent.*`, and `ai-assistants.*` namespaces
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `ai-agents.create` | POST | Create AI agent |
| `ai-agents.get` | GET, POST | Get AI agent |
| `ai-agents.list` | GET, POST | List AI agents |
| `ai-agents.update` | POST | Update AI agent |
| `ai-agents.delete` | POST | Delete AI agent |
| `ai-agents.deploy` | POST | Deploy AI agent |
| `ai-agents.callback` | POST | Handle agent callback |
| `ai-agents.suggestions` | POST | Get agent suggestions |
| `ai-agents.configs.list` | GET, POST | List agent configs |
| `ai-agents.templates.instantiate` | POST | Instantiate from template |
| `ai-agents.versions.create` | POST | Create agent version |
| `ai-agents.versions.get` | GET, POST | Get agent version |
| `ai-agents.versions.list` | GET, POST | List agent versions |
| `ai-agents.versions.update` | POST | Update agent version |
| `ai-agents.versions.delete` | POST | Delete agent version |
| `ai-agents.versions.update-state` | POST | Update version state |
| `ai-agents.skills.create` | POST | Create skill |
| `ai-agents.skills.update` | POST | Update skill |
| `ai-agents.skills.parse` | GET, POST | Parse/validate skill |
| `ai-agents.skill-config-overrides.create` | POST | Create config override |
| `ai-agents.skill-config-overrides.get` | GET, POST | Get config override |
| `ai-agents.skill-config-overrides.list` | GET, POST | List config overrides |
| `ai-agents.skill-config-overrides.update` | POST | Update config override |
| `ai-agents.skill-config-overrides.delete` | POST | Delete config override |
| `ai-agents.memories.create` | POST | Create agent memory |
| `ai-agents.memories.get` | GET, POST | Get agent memory |
| `ai-agents.memories.list` | GET, POST | List agent memories |
| `ai-agents.memories.update` | POST | Update agent memory |
| `ai-agents.memories.delete` | POST | Delete agent memory |
| `ai-agents-plans.create` | POST | Create agent plan |
| `ai-agents-plans.get` | GET, POST | Get agent plan |
| `ai-agents-plans.list` | GET, POST | List agent plans |
| `ai-agents-plans.update` | POST | Update agent plan |
| `ai-agents-plans.delete` | POST | Delete agent plan |
| `ai-agent.sessions.create` | POST | Create agent session |
| `ai-agent.sessions.get` | GET, POST | Get agent session |
| `ai-agent.sessions.list` | POST | List agent sessions |
| `ai-agents.events.execute-async` | POST | Execute event async |
| `ai-agents.events.execute-sync` | POST | Execute event sync |
| `ai-agents.events.signal` | POST | Signal event |
| `ai-assistants.surfaces.register` | POST | Register surface |
| `ai-assistants.surfaces.deregister` | POST | Deregister surface |
| `ai-assistants.surfaces.get` | GET, POST | Get surface |
| `recommendations.parts.suggest` | POST | Suggest parts |

## Out-of-the-Box Agents

### Search Agent (Computer)
The Search Agent is DevRev's employee-facing AI assistant, surfaced as "Computer." It provides a unified conversational interface across all connected enterprise data.

**What it can search:**
- **Document Search** -- Knowledge base articles, PDFs, Google Drive, Confluence, SharePoint, Notion
- **DevRev Search** -- All DevRev objects: tickets, issues, enhancements, accounts, opportunities, conversations, parts, users
- **Meeting Search** -- Transcripts and meeting notes
- **Email Search** -- Gmail and connected email sources
- **Web Search** -- External internet search to supplement internal data
- **Conversational analytics** -- Natural language queries over structured data (Text-to-SQL)

**How users interact:**
- Via the Computer app (web, desktop, mobile)
- Via `Cmd+K` / `Ctrl+K` in the DevRev app for quick search
- Conversational follow-up questions are supported
- Users can upload files (PDFs, CSVs) and ask questions about them
- Supports co-creation: drafting emails, PRDs, brainstorming

**Search architecture:** Hybrid search combining BM25 keyword-based and vector (semantic) retrieval, with re-ranking. Syntactic and semantic indexing are both supported across objects.

### CX Agent (Turing AI Agent)
Customer-facing AI agent deployed on PLuG, WhatsApp, email, LinkedIn, and website chat. The Turing AI agent handles ticket deflection and multi-step customer requests. See [[glossary/turing]].

### Computer (AI Teammate)
Computer is DevRev's AI teammate -- an intelligent unit combining Instructions, Knowledge, Tools, and Memory to execute complex workflows.

**Capabilities:**
- Find information across all connected apps and DevRev objects
- Answer and summarize from multiple sources
- Run conversational analytics (Text-to-SQL)
- Take actions: create tickets, update records, run workflows
- Upload and analyze files
- Perform web searches
- Route to or invoke other specialized agents

**Surfaces:** Available in the DevRev app sidebar, as a desktop app, via `Cmd+K`, and embeddable via PLuG SDK. Enterprise customers can add custom skills, connect tools, and configure knowledge sources via Agent Studio.

## Agent Studio
**Access:** Settings > Agents (`app.devrev.ai/<org>/settings/agent`).

**Core components of an agent:**
1. **Instructions** -- system prompt defining agent behavior, role, scope, guardrails.
2. **Skills** -- operations the agent can perform:
   - **Tools** -- built-in DevRev API actions (e.g., CreateTicket, FetchObjectContext).
   - **Workflows** -- custom multi-step automation sequences.
3. **Knowledge** -- DevRev objects the agent can access (tickets, issues, articles, accounts, etc.). Adding objects to the agent's Knowledge section grants it access to fetch data from those object types. The agent uses semantic search over articles, Q&A pairs, tickets, and other DevRev objects.
4. **Guardrails** -- safety rules.

### Instructions Detail
All prompts are system-level (user never sees them). Four prompt locations:

| Location | Purpose | Format |
|---|---|---|
| Goal | One-line statement of what the agent is for | Plain text, 1-2 sentences |
| Instructions | Detailed behavioral playbook | Rich text with @ mentions |
| Guardrails | Hard rules the agent must follow | Structured (topic + description) |
| Skill Descriptions | When to invoke a given skill | Plain text per skill |

**Recommended instruction structure:** `## Role & Persona`, `## Scope of Responsibilities`, `## How to Respond`, `## When to Use Skills`, `## Escalation Rules`, `## Tone & Style`.

**Best practices:**
- Write clear, unidirectional instructions (one rule per instruction)
- Use affirmative language ("Respond with X" not "Don't respond with Y")
- Use `@` mentions in the instructions editor to bind instructions to specific skills and knowledge sources
- Define explicit escalation triggers

### Skills Detail

**Two types of skills:**

**Tools** -- Built-in DevRev API actions. Examples: `create_ticket`, `search_articles` / `search_knowledge`, `update_ticket_priority`, `escalate_ticket`, `update_account_notes`, `update_contact`, `route_to_team`. Each tool requires: Name, Description (the trigger condition), Input fields (Auto-fill or Manual), Execute as User toggle, and Connections (keyrings for external systems).

**Workflows** -- Custom multi-step automation sequences built in DevRev's workflow builder. Used when the process has 3+ sequential steps, branching logic, external integrations, delays, or error handling.

**Workflow node types:** Action nodes, Tool nodes (call Jira API, send Slack message), Trigger nodes (on ticket created, on SLA breached), Delay nodes (wait 24 hours), Condition nodes (if/else branching), AI nodes (LLM-powered decisions within the workflow).

**Adding a workflow as a skill:** Build the workflow in the workflow builder, then add it to the agent under Build > Skills > Workflows. No additional configuration required beyond the workflow itself.

**NL Skills (advanced):** Sub-agents that receive a specific task, have their own tools and instructions, and return a result. Currently configured via API only (not UI). Each NL Skill has a Skill Description (always in context) and Plan Guidance (loaded on activation).

**Custom API calls as skills:** Supported via external system integrations using keyrings (OAuth, API tokens). Supported external systems include Slack, Jira, Salesforce, GitHub, and any custom API with a base URL and auth header. Custom snap-in nodes can also be built for high-code integrations.

**Skill design best practice:** Limit to 5-8 skills per agent. More skills make it harder for the agent to choose correctly.

### Knowledge Detail

**Object types that can be added as knowledge:**

| Category | Types |
|---|---|
| Content | Article, Question & Answer |
| Work items | Ticket, Issue, Task, Enhancement, Incident |
| Product | Product, Feature, Capability, Component |
| People | Rev User, Dev User, Group |
| Organizations | Account, Rev Org |
| Conversations | Conversation, Direct Message |
| Other | Custom Object, Dashboard, Dataset, Meeting, Microservice, Opportunity, Tag, Widget, Linkable, Runnable, Vista, Service Account |

**How semantic search over knowledge works:**
- The agent searches configured knowledge sources in real time -- it does not memorize data.
- Uses **hybrid search**: BM25 keyword-based + dense vector (semantic) retrieval combined via hybrid fusion.
- Retrieval priority: FetchObjectContext (direct ID lookup) -> Targeted skill -> HybridSearch -> NL2SQL.

**Indexing and embedding details:**
- Every piece of searchable content is normalized into **Knowledge Nodes (KN)** stored in a Knowledge Node DB.
- A stateless consumer (Wisp) generates vector embeddings via an ML-Pod pool and bulk-upserts into **OpenSearch**.
- Embeddings use the open-source **E5 model** deployed in-house.
- Articles are split into chunks (sentence-500 transform) for better semantic granularity.
- Automatic indexing triggers after content extraction; objects with extracted content >1 MB are skipped.

### Guardrails Detail

**What they are:** Hard rules that override all other agent behavior, evaluated on every interaction. Currently only `topic_boundary` type is supported -- restricts the agent to a specific topic.

**Configuration fields:**

| Field | Required | Description |
|---|---|---|
| Type | Yes | Currently only `topic_boundary` |
| Topic Name | Yes | Short label |
| Description | Yes | Detailed definition of what is allowed |
| Applies To | Yes | `["input"]`, `["output"]`, or `["input", "output"]` |
| Default Message | No | Message shown to user when guardrail triggers |
| Enabled | Yes | Boolean on/off |

**Applies To options:**
- `["input"]` -- Check user messages before the agent processes them.
- `["output"]` -- Check agent responses before sending.
- `["input", "output"]` -- Check both stages.

**Limits:** Maximum 16 guardrails per agent. Default guardrails are added out-of-the-box ("Always on", cannot be toggled).

**API configuration:** Use `POST /internal/ai-agents.create` or `POST /internal/ai-agents.update` with the `guardrails` field. Feature flag: `neuron.agent_guardrails_enabled` in archon-policy.

**Example guardrail topics:** PII Protection, Identity Verification, Refund Limit, Scope Boundary.

## Agent Testing Methods

### Preview / Playground
- Access: **Test > Preview Tests > Start New Chat**
- Use for: quick iteration during development, debugging specific issues, exploratory testing
- After each message, review the **execution trace**

**Trace elements:**

| Element | What it tells you |
|---|---|
| Thought | Agent's internal reasoning |
| LLM Reasoning (intermediate) | Processing steps |
| LLM Reasoning (final) | Final decision before responding |
| Input | Data sent to a skill |
| Output | Data received from a skill |
| Guardrail Check | Whether guardrails triggered |
| Response Time | Latency per step |

### Bulk Tests
- Access: **Test > Bulk Tests > Create Bulk Test**
- Use for: pre-publish validation, regression testing, stakeholder demos

**Dataset format (CSV upload):**

| Column | Required | Description |
|---|---|---|
| Input | Yes | The question/request to send |
| Expected Output | Yes | The expected response |
| Remarks | No | Additional context for evaluators |

**Evaluators:**
- **Correctness** -- Whether the response accurately addresses the input
- **Completeness** -- Whether the response fully covers the expected output

### Analytics
- Access: **Observe > Analytics** (must be explicitly enabled per agent)
- **Agent Task Success (Task Completion):** Did the customer get their problem solved? Score: 0.0-1.0
- **Agent Accuracy (Faithfulness):** Is the information correct and sourced? Score: 1-5
- Defaults to last 7 days

### Sessions
- Access: **Observe > Sessions**
- Each session shows: Trigger, Members, Last message timestamp
- Click a session to see: full conversation history + step-by-step execution trace
- Use to: debug reported issues, find failure patterns, identify knowledge gaps, validate guardrails
- Recommended cadence: daily review for the first week post-publish, then weekly

## Agent Deployment & Versioning

**How to deploy:**
1. Build the agent in Agent Studio (Build tab: goal, instructions, skills, knowledge, guardrails).
2. Test in Playground and via Bulk Tests.
3. Click **Publish** in the Build tab -- this promotes the Draft to Live.
4. Deploy to a channel (PLuG, Slack, WhatsApp, email, internal surfaces) via workflows.

**Agent types and channels:**
- **Internal (coming soon):** Employees, internal surfaces.
- **CX (External):** End customers via Slack, WhatsApp, PLuG Chat, Email.

**Versioning states:**

| State | Description |
|---|---|
| Draft | Work-in-progress. Only one at a time. |
| Live (Published) | Active version. Only one at a time. |
| Archived | Previous live version. Preserved. |

| Action | Effect |
|---|---|
| Edit Live agent | Auto-creates new Draft |
| Publish | Draft -> Live, previous Live -> Archived |
| Restore | Creates new Draft from any previous version |

**Rollback:** One-click restore to any previous version via **Build > Version History > Restore**.

**A/B testing:** Supported -- compare different agent configurations and approaches. Gradual rollout and sandbox environments are available for safe testing before full deployment.

## Session Data Captured

Per session, the following data is captured:
- Trigger (what initiated the conversation)
- Members (participants)
- Last message timestamp
- Full message history
- Step-by-step execution trace (Thought, LLM Reasoning, Input/Output per skill, Guardrail checks, Response time)

**Session review:** Navigate to **Observe > Sessions** in Agent Studio. Filter by: Last message (time range), Trigger type. Click any session to open the detail view with full conversation + trace.

## Turing AI Agent Deflection Flow

When a customer sends a message on a supported channel (PLuG, email, WhatsApp, etc.), the Turing AI agent follows this deflection sequence:

1. **Search** -- The Turing AI agent searches the knowledge base and connected sources for relevant content.
2. **Suggest article** -- If a matching article is found, the agent suggests it to the customer.
3. **Suggest answer** -- If no single article suffices, the agent synthesizes an answer from available knowledge and presents it.
4. **Create ticket** -- If the customer's question cannot be resolved, the agent creates a ticket for human follow-up (or routes to a human agent, depending on org configuration).

Throughout this flow, the Turing AI agent tags resolved conversations as `turing_deflected` and unresolved ones as `turing_undeflected`.

**Triggers for routing to a human:**
- User explicitly requests a human agent
- The Turing AI agent cannot find a relevant answer after attempting knowledge base search
- The conversation matches a configured escalation scenario
- The Turing AI agent emits enter/exit events to manage handover between bot and human

**How the Turing AI agent uses the knowledge base:**
- Searches articles (Text, Markdown, PDF, HTML, DocX) and Q&A pairs
- Uses the full DevRev Knowledge Graph -- not just KB articles -- including tickets, website content, and any ingested external URLs
- Asynchronous pipeline: CUD events on KB articles trigger re-embedding and index updates

See [[glossary/turing]] for modes and metrics.

## AI Agent Ticket Resolution Flow
Workflow: `TicketCreated` trigger → `TalkToAgent` action → agent searches knowledge base → responds to customer → if unresolved, suspends on dev user message for human handoff.

## Related flows
- Agent creation and deployment flow (see "Agent Deployment & Versioning" above)
- [gap] Skill authoring and validation flow

## Related scenarios
- [gap] Scenarios to be created from 1107 test cases

## Open questions
- [gap] What are the available agent templates and how do they differ? (Pre-built patterns documented: Customer Support, Ticket Routing, Internal Knowledge -- but full template list not yet available)
- [gap] What event types can be signaled and what triggers async vs sync execution?
- Agent versions: Only one Live version serves traffic at a time. Draft is work-in-progress, Archived is preserved previous. Publishing promotes Draft to Live. See "Agent Deployment & Versioning" above.
- [gap] What is the complete list of strategy values for memories beyond "Bundle" (id=1)?
