---
title: Conversations
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_conversations.jsonl, raw/docs/devrev-developer-docs.md]
related: []
last_updated: 2026-04-12
---

# Conversations

## What it does
The Conversations feature manages support conversations within DevRev. It provides operations for creating, retrieving, listing, counting, and converting conversations. With 80 test cases, this feature covers conversation lifecycle management with a focus on the dual-persona model (dev users vs rev users) and the distinct access patterns each persona has. The backend service is `us_codexv2`.

## Why it exists
Customer support interactions need structured conversation objects that track the full lifecycle from initial contact through resolution. Conversations connect customers (rev users) to support agents (dev users) and provide the foundation for DevRev's support workflows.

## Key behaviors
- **Conversation CRUD**: Create, get, list, count conversations
- **Conversation conversion**: Convert conversations between types
- **Members array**: Always present in responses (required schema field), even if empty
- **ID matching**: Response `conversation.id` exactly matches requested id (byte-for-byte, no aliasing or normalization)
- **Rev user filter override**: When a rev user calls `conversations.count`, the `owned_by` filter is silently ignored and replaced with `MemberIds: [rev_user_don]` -- rev users can only count their own conversations
- **Display ID**: Human-readable identifier present alongside DON-format id

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `conversations.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `conversations.create` | POST | Create conversation |
| `conversations.get` | POST | Get conversation by ID |
| `conversations.list` | POST | List conversations |
| `conversations.count` | POST | Count conversations |
| `conversations.convert` | POST | Convert conversation type |

## Conversation Types
- **Support conversations** -- customer-facing, created via PLuG, email, Slack, portal.
- **Internal discussions** -- team-only, on tickets/issues.
- **Side conversations/threads** -- sub-threads within a ticket or conversation. See [[features/side-conversations]].

## PLuG Widget
Customer-facing chat widget embedded in your product. Creates conversations in DevRev Inbox. Configured under Settings. Supports AI agent ([[glossary/turing]]) for deflection. See [[glossary/plug]].

## Email Channels
Incoming emails create Conversations. Configured via Settings > Integrations > Email. Supports ReplyTo addresses. Email threads map to ticket reporters and email members.

## Conversation-to-Ticket Conversion
- **UI:** From within a conversation, click the convert option.
- **Workflow:** `ConvertConversationToTicket` action (input: conversation_id; output: ticket_id).
- Title and description are auto-populated from the conversation.

## Messaging Features
- Rich text / Markdown formatting.
- File attachments.
- @mentions of users.
- Comment visibility options: `external`, `internal`, `private`.

## Related flows
- [gap] Support conversation lifecycle flow

## Related scenarios
- [gap] Scenarios to be created from 80 test cases

## Open questions
- [gap] How does the members array get populated (auto-added or explicit)?
- [gap] What fields differ between dev user and rev user conversation views?
