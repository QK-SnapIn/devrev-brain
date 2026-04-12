---
title: Ticket
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md, raw/docs/devrev-docs-tickets-issues-conversations.md, raw/docs/devrev-agent-dump-part1.md]
related: [[features/stock-objects]], [[entities/issue]], [[entities/conversation]], [[features/slas]], [[entities/part]]
last_updated: 2026-04-12
---

# Ticket

## Description
A ticket is a customer-facing work item representing a support request, bug report, or inquiry. Tickets are the primary object in the [[support-app]] (Computer for Support Teams).

## Stages

| Group | Stage | Code |
|-------|-------|------|
| Open | Queued | Q |
| In Progress | Work In Progress | WIP |
| In Progress | Awaiting Product Assist | APA |
| In Progress | Awaiting Customer Response | ACR |
| In Progress | Awaiting Development | AD |
| In Progress | In Development | ID |
| Closed | Canceled | C |
| Closed | Accepted | A |
| Closed | Resolved | R |
| Closed | Archived | -- |

## Priority Levels

| Priority | Numeric Value |
|----------|--------------|
| P0 | 0 (Urgent) |
| P1 | 1 (High) |
| P2 | 2 (Medium) |
| P3 | 3 (Normal) |
| P4 | 4 (Low) |

## Severity Levels

| Severity | Description |
|----------|-------------|
| Low | Minor impact |
| Medium | Moderate impact |
| High | Significant impact |
| Blocker | Critical, service-stopping impact |

## Stock Attributes

**Assignment & Ownership:**
- **Owner:** Person responsible for the ticket (engineer, PM, designer, team member)
- **Created by:** User who initiated the ticket (auto-populated)
- **Modified by:** User who last made changes (auto-populated)
- **Reported by:** Customer experiencing the issue; multiple reporters possible from email threads

**Categorization:**
- **Part:** Product or service the issue relates to (see [[entities/part]])
- **Group:** Group assignment for ticket organization
- **Tags:** Categorical labels for filtering
- **Subtype:** Custom ticket categories (bugs, feature requests, questions)

**Priority & Urgency:**
- **Severity:** Low, medium, high, or blocker classification
- **Target close date:** Expected resolution deadline

**Tracking & Status:**
- **Stage:** Current lifecycle state
- **Display ID:** Auto-generated identifier in [[glossary/don]] format
- **Created date:** Timestamp of ticket creation
- **Modified date:** Last modification timestamp
- **Close date:** Resolution timestamp
- **Needs response:** Boolean flag set true when customer message arrives

**Communication:**
- **Customer workspace:** Associated workspace/account
- **Email members:** Active email thread participants (auto-updates)
- **CCed members in email:** Added as reporters if workspace contacts
- **Subscribers:** Users receiving updates (requires DevRev contact)
- **Source channel:** Creation origin (email, portal, Slack, etc.)
- **Channel:** Customer communication medium

**System Users:**
- **Shadow users:** Non-access tracking users created by data imports ([[glossary/shadow-user]]). These users have no app access and are created automatically when data is imported via AirSync.

## Creation Methods
1. **Quick Create** -- `+` button or `Cmd+K` / `Ctrl+K`
2. **PLuG widget** -- customer submits via [[glossary/plug]]
3. **Email channel** -- incoming email auto-creates ticket
4. **Conversation conversion** -- convert a conversation to a ticket
5. **Workflow action** -- `CreateTicket` workflow action
6. **API** -- `works.create` endpoint
7. **Airdrop/AirSync** -- imported from external systems
8. **Follow-up ticket** -- auto-created when customer responds to archived ticket

## Creation UI Flow
1. Navigate Support > Tickets
2. Click "New Ticket"
3. Enter title and description (file attachments supported)
4. Select related part
5. Assign attributes: owner, severity, tags, workspace
6. Optionally link related records via "Link Records"
7. Optionally select "Create multiple" for batch creation
8. Click Create

**From Conversation:** Title and description auto-populate from existing conversation.

**Child Issue Creation:** Click "+ Link issue" > "Add a child issue". Create new or link existing issue. Fields auto-populate with manual edit capability.

**Internal Tickets:** Create external ticket dropdown > select "Create internal ticket". Invisible to customers until explicitly converted external. "Customer Messages" tab unavailable. Conversion permanent via "Convert to External".

## Assignment Methods
- Manual assignment (owner field)
- Group-based assignment
- Workflow-based auto-assignment
- AI agent suggestion (SuggestPart)

## Linking Types
- `is_dependent_on` -- links ticket to issue
- `LinkConversationWithTicket` -- links conversation
- `LinkIncidentWithIssue` -- links incident
- `LinkMeetingWithTicket` -- links meeting

## Duplicate Merging
**Eligibility:** Same workspace, matching reporters, unclosed status.
**Process:** Open primary ticket -> select merge option from side panel -> review suggested duplicates -> confirm.
**Post-merge:** Primary ticket retains all key fields. Duplicate tickets become immutable. Subscribers/reporters from duplicates added to primary. Merge is irreversible.

## Internal vs External Tickets
- External tickets are customer-facing (created via PLuG, email, portal).
- Internal tickets are team-only.
- Comment visibility options: `external`, `internal`, `private`.

## Follow-up Tickets
Created automatically when a customer responds to an archived/immutable ticket.

**Trigger Scenarios:**
- Customer communication on archived ticket via email
- Customer communication on merged primary (also archived)

**Auto-Populated Fields:** Part, channel, account, workspace, reported by, description, title, custom fields, subtype.

**Messaging Behavior:** Customer sees responses in original email/Slack thread. Agent responds on new follow-up ticket.

## Turing Suggests AI
Proactive AI feature displayed on each ticket view that recommends similar tickets and relevant knowledge base articles. Includes a user feedback mechanism (thumbs up/down) for AI training. See [[glossary/turing]].

## Attachment Management
Centralized Attachments section on each ticket that aggregates files from the description, discussion, and customer message areas into a single view.

## Custom Fields & Subtypes
Custom fields configured via Settings > Object customization > Ticket. See [[features/customization]].
Subtypes allow different field schemas per ticket category.

## Relationships
- Linked to [[entities/issue]] via `is_dependent_on` -- when an issue closes, linked tickets can be auto-updated.
- Created from [[entities/conversation]] via conversion.
- SLA tracked via [[features/slas]].
- Belongs to [[entities/account]].
