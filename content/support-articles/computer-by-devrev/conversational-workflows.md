---
title: Conversational workflows
devrev_id: ART-21903
parent_directory: Workflow engine
translation_group: dlr74RiI
modified_date: "2025-12-10T06:56:52.841Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/dlr74RiI"
tags: []
top_category: Computer by DevRev
wiki_match: features/conversational-workflows
match_score: 1.0
last_updated: 2026-05-11
related: ['features/conversational-workflows']
summary: "In DevRev, you can automate your customer support conversations with our workflow engine."
---

# Conversational workflows

In DevRev, you can automate your customer support [[features/conversations-feature|conversations]] with our
workflow engine. You can either [[features/build|build]] an AI agent handle to handle all or [[features/parts|parts]]
of your customer support conversations, or you can also create deterministic
button-based flows.

## AI agents in your conversational workflow

To enable [[features/agents|AI agents]] for customer support, please contact us through the
chat widget.

### AI agents for conversations or tickets

1. Set the trigger for workflow to start with *[[entities/conversation|Conversation]] created* or *[[entities/ticket|Ticket]]
   created*.

   This trigger is whenever a conversation or ticket gets created by your
   customers from Portal or [[glossary/plug|Plug]], or any of your integration which supports
   conversation syncing, like Slack, WhatsApp, or email. You can find the
   integrations in our marketplace.
2. Add the *Talk to agent* step as the next action. Fill all the required values
   of this step. The values needed to fill here are explained below.
3. Deploy the workflow.

Now, your workflow runs whenever a conversation or a ticket gets created and it
assigns it to an AI agent, which handles the conversation. No brittle rules.

Find below a detailed explanation of all the fields needed to configure in the
"Talk to Agent" Step

|  |  |  |
| --- | --- | --- |
| Parameter | Type | Description |
| `agent` | String | ID of the AI agent to use. Use the dropdown to select one. |
| `object` | String | ID of the conversation or ticket where the agent operate.s |
| `visibility` | Dropdown | Visibility of agent comments: `internal` or `external`. For customer-facing use cases it is `external.` |
| `panel` | Dropdown | Panel for agent responses: `CustomerChat`. |
| `quick_replies` (optional) | Array[String] | Preset reply options that display to users. |
| `respond_to_user_types` | Array[String] | User types the agent engages with (for example, `customer`). For customer facing use cases it is `customer`. |
| `suspend_on_message_from` (optional) | String | User type that causes the agent to pause (for example, `DevUser`). |
| `additional_context` (optional) | String | Additional context you want to pass to the agent for more personalized responses. You can also use variables from previous steps here. |

* Each button creates a corresponding output port in the workflow.
* When a button is clicked, the original message is updated to remove the
  buttons.
* A confirmation message is added showing which option was selected.

## Related wiki nodes
- [[features/conversational-workflows]]

## Source
- DevRev support [[entities/article|article]] [Conversational workflows](https://support.devrev.ai/en-US/devrev/article/dlr74RiI) (ART-21903)
