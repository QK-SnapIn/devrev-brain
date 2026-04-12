---
title: "Side Conversations"
type: feature
status: draft
sources: ["raw/exports/Side Conversations<>PRD.md"]
related: ["features/conversations", "features/stock-objects", "flows/side-conversation-flow"]
last_updated: 2026-04-12
---

# Side Conversations

## What it does
Side Conversations allow support agents to create secondary threads (side threads) from existing tickets to collaborate with external non-customer users, forward messages with context, and manage multi-channel communication (email, Slack, etc.) -- all while maintaining linkage to the parent ticket. The feature supports SLA tracking, CSAT collection, analytics, visibility controls, and rich text editing in the email composer.

## Why it exists
Support workflows often require collaboration with third parties (vendors, partners, internal teams) that should not be visible to the end customer. Side Conversations provide a structured way to fork discussions from a ticket, preserve context, and bring resolution data back to the main thread without exposing internal communication.

## Key behaviors

### Message Forwarding
- Forward messages and attachments from a selected timeline entry
- Include backward context (all previous messages before the selected point) for both Rev and Dev users
- Attachments forwarded without corruption; remain downloadable
- Minimal-click UX (3 clicks or fewer to complete forwarding)

### Thread Management
- Start a side thread from an existing ticket with correct context
- Start a side thread with empty context (standalone, no ticket selected)
- Create multiple independent side threads per ticket
- Prevent duplicate thread creation (system warns or blocks)

### External Collaboration
- Share threads with external non-customer users via email
- External users can receive and respond to threads
- Sync updates from partner/third-party (3P) replies back into the same thread

### Context & Linkage
- Maintain context between main ticket and side thread
- Perform actions on the main ticket from within a side thread (reflected on main ticket)
- Thread linking consistency: link remains intact when ticket is updated
- Email threading consistency: multiple replies grouped under same thread

### Multi-Channel Support
- Create side threads via email channel
- Support multiple channels (email, Slack, etc.) for thread creation
- Threads created per channel independently

### Automation & Integration
- Automation rules trigger correctly on side thread updates
- [gap] Which specific automation triggers are supported for side threads?

### Email Composer
- Rich Text Editor (RTE) support for formatting in email composer
- Formatting persists correctly in sent messages

### SLA & CSAT Tracking
- SLA timers tracked correctly for side threads
- CSAT captured correctly when thread is closed and feedback requested

### Analytics
- Side thread metrics visible in analytics dashboards

### Comment Visibility Options
- **External** -- visible to customers and agents.
- **Internal** -- visible to internal team only, hidden from customers.
- **Private** -- visible to specific users only.

### Security & Visibility
- Visibility control: only authorized users can view/access threads
- [gap] Exact permission model for thread visibility not documented

### Error Handling & Performance
- Error handling for failed forwarding: proper error message shown, retry possible
- Large data handling: system handles bulk messages without lag or failure
- Concurrent updates: multiple users updating thread simultaneously without data loss or overwrite

## Entry points
- Ticket timeline view > Forward action or "Start side thread" action
- [gap] Exact UI entry point names and locations not documented

## Related flows
[[flows/side-conversation-flow]]

## Related scenarios
[gap] No scenario pages created yet for individual side conversation test cases.

## Open questions
- [gap] What channels besides email are supported for side conversations?
- [gap] What is the maximum number of side threads per ticket?
- [gap] How does side conversation SLA tracking interact with the parent ticket's SLA?
- [gap] Can side threads be merged or closed independently of the parent ticket?
- [gap] What permissions are required to start a side conversation?
