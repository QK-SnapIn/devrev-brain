---
title: Conversations
type: feature
status: stable
sources: [raw/docs/devrev-docs-tickets-issues-conversations.md, raw/docs/devrev-agent-dump-part2.md, raw/docs/devrev-docs-scraped.md]
related: [[entities/conversation]], [[features/inbox]], [[features/tickets]], [[features/side-conversations]], [[features/slas]]
last_updated: 2026-04-12
---

# Conversations

## What it does
Conversations are synchronous or near-synchronous discussion threads between customers and support teams in the [[support-app]]. They serve as the initial point of contact before being converted to tickets, and are managed through the Inbox.

## Why it exists
Provides real-time customer communication across channels (PLuG widget, email, Slack) with intelligent routing, spam detection, and seamless conversion to tickets for formal tracking.

## Key behaviors
- Created via PLuG widget (Computer widget), email integration, or Slack integration
- Routed to customer org's default owner, or via support routing snap-in keyword matching
- Categorized in Inbox as **Primary** (verified customers), **Guest** (unverified), or **Spam**
- Stages: New → Waiting on User (WOU) / Needs Response (NR) / Hold (H) → Resolved → Archived
- Managed through the [[glossary/inbox]], DevRev's unified conversation hub
- Suspended stage for invalid/spam conversations; can be moved to "new" if valid
- Convert to ticket: title and description auto-populate from conversation
- "Needs response" flag auto-set when customer replies
- SLA tracking: time to initial response measured from creation to New → WOU transition
- Slash commands available by typing `/` in the response text box
- Support for rich text, attachments, @mentions, internal/external/private comment visibility
- Side conversations/threads for external collaboration (see [[features/side-conversations]])

## Entry points
- **Inbox:** Support > Inbox (Primary / Guest / Spam tabs)
- **PLuG Widget:** Customer initiates via embedded chat widget
- **Email:** Incoming email to configured email channel
- **Slack:** Via Slack snap-in integration
- **Quick Create:** `+` button or `Cmd+K` → Conversation
- **API:** Conversation API endpoints
- **Workflow:** `ConvertConversationToTicket` action

## Conversation sources & priority
- Conversations from verified customer orgs → **Primary** (higher priority)
- Conversations from unknown users → **Guest** (lower priority)
- Spam/malicious conversations → **Spam** (can be marked "Not spam")

## Detailed entity reference
See [[entities/conversation]] for complete stage list, routing behavior, and metrics.

## Related flows
- [[flows/critical-product-flows]] — Customer Portal Interaction, Communication
- [[flows/side-conversation-flow]] — Side thread lifecycle

## Related scenarios
[gap] Scenarios to be generated from test cases

## Open questions
- [gap] What keywords does the support routing snap-in match on?
- [gap] How are conversation priority levels determined beyond org identification?
- [gap] What slash commands are available in the conversation response box?
