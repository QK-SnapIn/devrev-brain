---
title: Turing
type: glossary
status: stable
sources: [raw/docs/devrev-agent-dump-agents.md]
last_updated: 2026-04-12
---

# Turing AI Agent

DevRev's customer-facing AI support agent (also called CX Agent). Deployed on PLuG, WhatsApp, email, LinkedIn, and website chat. The Turing AI agent handles ticket deflection and multi-step customer requests by searching the knowledge base ([[features/knowledge-base]]) and Q&A objects.

**Capabilities:**
- Answers customer queries using articles and Q&A pairs
- Operates within the [[glossary/plug]] widget and across multiple channels (email, WhatsApp, LinkedIn)
- "Turing suggests" feature on ticket view proactively shows similar tickets and related articles
- Uses the full DevRev Knowledge Graph -- not just KB articles -- including tickets, website content, and ingested external URLs
- Asynchronous pipeline: CUD events on KB articles trigger re-embedding and index updates

## Modes

- **Suggest mode (Assist):** The Turing AI agent suggests a response to the human agent, who can edit and send it. Uses the `/assist` command.
- **Auto-response mode (Automated):** The Turing AI agent replies directly to the customer without human intervention.

## Deflection Flow

When a customer sends a message on a supported channel, the Turing AI agent follows this deflection sequence:

1. **Search** -- The Turing AI agent searches the knowledge base and connected sources for relevant content.
2. **Suggest article** -- If a matching article is found, the agent suggests it to the customer.
3. **Suggest answer** -- If no single article suffices, the agent synthesizes an answer from available knowledge and presents it.
4. **Create ticket** -- If the customer's question cannot be resolved, the agent creates a ticket for human follow-up.

Throughout this flow, the Turing AI agent tags resolved conversations as `turing_deflected` and unresolved ones as `turing_undeflected`.

**Triggers for human routing:** user explicitly requests a human; the Turing AI agent cannot find a relevant answer; conversation matches a configured escalation scenario. The agent emits enter/exit events for handover management.

## Metrics

- **Deflection rate** -- % of queries resolved without human involvement
- **Number of queries handled**
- **Overall success rate**
- **First response time** and **total response time**
- `turing_deflected` and `turing_undeflected` tag counts
- CX Agent-specific: total messages processed, P90 latency (TTFT), deflection %

See [[features/agents]] for the full agent architecture.
