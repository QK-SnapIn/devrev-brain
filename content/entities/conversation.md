---
title: Conversation
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md, raw/docs/devrev-docs-tickets-issues-conversations.md, raw/docs/devrev-docs-scraped.md]
related: ["features/conversations", "entities/ticket", "features/side-conversations", "features/inbox"]
last_updated: 2026-04-12
---

# Conversation

## Description
A conversation is an object type that tracks any synchronous or near-synchronous discussions. Conversations may be initiated by customers, builders, or the system automatically. They are the entry point for customer interactions and can be converted into tickets.

## Types
- **Support conversations** -- customer-facing, created via PLuG, email, Slack, portal.
- **Internal discussions** -- team-only, on tickets/issues.
- **Side conversations/threads** -- sub-threads within a ticket or conversation.

## Routing
New conversations are routed to the customer org's default owner unless they match keywords in the support routing snap-in configuration. Conversations from unidentified customer organizations receive lower priority than those from established customers.

## Stages

| Group | Stage | Code | Description |
|-------|-------|------|-------------|
| Open | New | -- | Initial stage for valid conversations; transitions to WOU when support responds |
| Open | Suspended | -- | Initial stage for invalid/spam conversations; can be moved to New if deemed valid |
| In-Progress | Waiting on User | WOU | Support awaits customer response; used for initial responses and resolution validation |
| In-Progress | Needs Response | NR | Customer responded; support engineer must review and respond or resolve |
| In-Progress | Hold | H | Resolution depends on external dependencies (SME review, tickets, issues, etc.) |
| Closed | Resolved | R | Customer concerns addressed; conversation remains visible in end-user widget |
| Closed | Archived | -- | Final stage for conversation |

## Inbox Categorization
The Inbox (see [[features/inbox]]) sorts conversations into three categories:
- **Primary** -- Conversations started by verified customers
- **Guest** -- Conversations started by a user that is not verified as a customer
- **Spam** -- Conversations that appear to be malicious, fraudulent, or otherwise invalid. Users can mark erroneously categorized spam as "Not spam."

## Tags
Available tags: Stalled, Priority/Escalated, Fast/Slow Moving, Blocked, Resolution: [value].

## Key Metrics
**Time to initial response** is calculated between the conversation created timestamp and the time the stage transitions from _New_ to _Waiting on User_.

## Actions
- Create, get, list, count conversations
- Convert conversation to ticket (`ConvertConversationToTicket`)
- Link conversation with ticket (`LinkConversationWithTicket`)
- Add comments with visibility control (`external`/`internal`/`private`)
- Update conversation properties

## PLuG Widget Relationship
Customer messages via the [[glossary/plug]] widget create conversations in DevRev Inbox (see [[features/inbox]]). The AI agent ([[glossary/turing]]) can handle initial deflection before human handoff.

## Email Channel Relationship
Incoming emails create conversations. Configured via Settings > Integrations > Email. Email threads map to ticket reporters and email members. Supports ReplyTo addresses.

## Slack Integration
Conversations can also be initiated through Slack integration.

## Conversion to Ticket Flow
1. From within a conversation, click the convert option.
2. Title and description are auto-populated from the conversation.
3. Workflow alternative: `ConvertConversationToTicket` action (input: conversation_id; output: ticket_id).

## Fields
Known fields: Members (always present in responses), Display ID, ID (DON format), owned_by, type, stage, tags, part, created date, modified date.
