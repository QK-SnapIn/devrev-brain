---
title: Conversational Workflows
type: feature
status: draft
sources: []
related: ["features/workflows", "features/plug-widget", "features/agents"]
last_updated: 2026-04-12
---

# Conversational Workflows

## What it does
Conversational Workflows are a distinct workflow type in DevRev designed for automating customer-facing conversations. Unlike standard event-driven workflows (which react to object changes), conversational workflows guide interactive, multi-step dialogues with customers through the PLuG widget, Slack, WhatsApp, email, and portal channels.

## Why it exists
Standard workflows automate back-office processes (routing, updates, notifications). Conversational workflows solve a different problem: structuring the customer-facing conversation itself — collecting information, presenting options, escalating to AI agents, and routing to the right resolution path — all without requiring a human agent to intervene at every step.

## Key behaviors
- **Triggers:** Conversation created or Ticket created (from Portal, PLuG, Slack, WhatsApp, email)
- **Two modes:**
  - **AI agent-driven:** Uses the "Talk to Agent" step to hand off to an AI agent mid-conversation
  - **Deterministic button-based flows:** Presents structured choices (buttons, forms, carousels) for the customer to navigate
- **User input nodes:** Buttons, forms, carousels, calendar pickers, sliders
- **Transfer to AI agent:** Mid-flow handoff to an AI agent for free-form conversation
- **Dynamic output ports:** Branching based on user selections
- **Looping:** Can loop back to earlier nodes for retry or re-collection of information
- **Nudge triggers:** Can be triggered by PLuG [[glossary/nudge]] events (e.g., user clicks a nudge button)

## Entry points
- Settings > Workflow Builder (select "Conversational" type when creating)
- Triggered automatically when a conversation or ticket is created via configured channels
- Triggered by PLuG nudge button clicks
- Documentation: https://docs.devrev.ai/product/conversational-workflows

## Related flows
[[flows/workflow-builder-crud]]
[gap] No dedicated flow page for conversational workflow creation and testing.

## Related scenarios
[gap] No scenario pages created yet for conversational workflow test cases.

## Open questions
- [gap] Can conversational workflows be imported/exported like standard workflows?
- [gap] What happens if a customer abandons mid-conversation — is there a timeout or fallback?
- [gap] Are there limits on the number of user input nodes in a single conversational workflow?
- [gap] How does versioning work — same semantic versioning as standard workflows?
- [gap] Can a single conversation trigger both a standard workflow and a conversational workflow?
