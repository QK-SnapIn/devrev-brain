---
title: "Side Conversation End-to-End Flow"
type: flow
status: draft
sources: ["raw/exports/Side Conversations<>PRD.md"]
related: ["features/side-conversations", "features/conversations", "features/stock-objects"]
last_updated: 2026-04-12
---

# Side Conversation End-to-End Flow

## Goal
Validate the complete lifecycle of side conversations: forwarding messages, starting side threads, external collaboration, multi-channel creation, SLA/CSAT tracking, analytics, visibility controls, and concurrent update handling.

## Preconditions
- User logged into DevRev with access to tickets
- At least one ticket with timeline entries and attachments exists
- Email channel enabled for email-based thread tests
- External email/user available for collaboration tests
- Automation rules configured for automation trigger tests
- SLA rules defined for SLA tracking tests
- Multiple user accounts for visibility and concurrency tests

## Steps

### Forwarding Messages (Test Cases 1-4)
1. Open a ticket with timeline entries
2. Select a timeline entry and click Forward > verify all messages and attachments from that point are included
3. Forward from a mid-timeline entry > verify all previous messages (backward context) are included for both Rev and Dev users
4. Forward a timeline with attachments > verify attachments are not corrupted and are downloadable
5. Measure forwarding UX > verify action completes in 3 clicks or fewer

### Starting Side Threads (Test Cases 5-6)
1. From an existing ticket, initiate a side thread > verify thread starts with correct context
2. Without selecting a ticket, start a side thread > verify empty/standalone thread is created successfully

### External Collaboration (Test Cases 7-8)
1. Share a side thread with an external non-customer user > verify external user receives the thread
2. External user responds > verify response appears in the same thread in DevRev

### Context & Linkage (Test Cases 8-9, 23-24)
1. Update a side thread > verify context is preserved and visible in the main ticket
2. Perform an action on the main ticket from within the side thread > verify action reflects on main ticket
3. Update the parent ticket > verify thread link remains intact
4. Receive multiple email replies > verify all messages grouped under the same thread

### Automation (Test Case 10)
1. Configure automation rules for side thread events
2. Update a side thread > verify automation triggers correctly

### Email Channel (Test Cases 11-12)
1. With email channel enabled, start a side thread via email > verify thread created successfully
2. With multiple channels configured, create threads across different channels > verify each channel creates threads independently

### Multiple Threads (Test Case 13)
1. From a single ticket, create multiple side threads > verify all operate independently

### Rich Text Editor (Test Case 14)
1. Open the email composer in a side thread
2. Format a message (bold, italic, links, etc.) > send
3. Verify formatting persists in the sent/received message

### Third-Party Sync (Test Case 15)
1. Forward a message to an external partner
2. Partner replies to the forwarded email
3. Verify the reply syncs back into the same side thread

### Duplicate Prevention (Test Case 16)
1. With an existing thread, attempt to create a duplicate
2. Verify system prevents or warns about duplication

### Analytics (Test Case 17)
1. With active side threads, navigate to analytics dashboards
2. Verify side thread metrics are visible and accurate

### SLA Tracking (Test Case 18)
1. With SLA rules defined, create/update a side thread
2. Verify SLA timers are tracked correctly for the thread

### CSAT Tracking (Test Case 19)
1. Close a side thread > verify feedback is requested
2. Submit CSAT feedback > verify it is captured correctly

### Visibility Control (Test Case 20)
1. Share a thread with specific users
2. Verify only authorized users can view/access the thread
3. Verify unauthorized users cannot see the thread

### Error Handling (Test Case 21)
1. Simulate a network/API failure during forwarding
2. Verify a proper error message is shown
3. Verify retry is possible after failure

### Performance - Large Data (Test Case 22)
1. Forward from a ticket with a large timeline (many messages)
2. Verify system handles without lag or failure

### Concurrency (Test Case 23)
1. Have multiple users update the same side thread simultaneously
2. Verify no data loss or overwrites occur

## Success criteria
- All 24 test cases pass
- Forwarding preserves complete context and attachment integrity
- Side threads maintain bidirectional linkage with parent tickets
- External collaboration works end-to-end with reply sync
- SLA and CSAT tracking function correctly for side threads
- Analytics capture side thread metrics
- Visibility controls enforce access permissions
- System handles errors gracefully with retry capability
- No data loss under concurrent updates or large data volumes

## Failure modes
- Forward omits messages or corrupts attachments
- Side thread loses context link to parent ticket
- External user cannot receive or respond to thread
- Automation fails to trigger on side thread updates
- SLA timers incorrect or missing for side threads
- CSAT not captured on thread closure
- Unauthorized users can access restricted threads
- Forward fails silently without error message
- System crashes or lags with large timelines
- Concurrent updates cause data loss or overwrites

## Locators touched
[gap] No locator page exists yet for the Side Conversations UI.

## API calls involved
[gap] API endpoints for side thread CRUD, forwarding, and email integration not yet documented.
