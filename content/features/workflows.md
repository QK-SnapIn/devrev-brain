---
title: "Workflow Builder"
type: feature
status: draft
sources: [raw/exports/Sample.md, raw/docs/devrev-agent-dump-workflows.md]
related: ["features/stock-objects", "features/agents", "flows/workflow-builder-crud"]
last_updated: 2026-04-12
---

# Workflow Builder

## What it does
The Workflow Builder is a visual canvas-based tool in DevRev Settings that allows users to create, edit, deploy, and manage automated workflows. Workflows consist of triggers, control steps, and action steps that are linked together on a drag-and-drop canvas. It supports ticket and issue automation, AI-native steps (spam checker, sentiment evaluator), get functions, and import/export of workflow definitions.

## Why it exists
Enables support and development teams to automate repetitive processes without writing code. Common use cases include automatic ticket routing, spam detection, sentiment analysis on resolved tickets, and cross-object data retrieval (get workspace, get account, get customer).

## Key behaviors

### CRUD Operations
- Create new workflows from Settings > Workflow Builder via "+Workflow" button
- Edit title and description (autosaved)
- Add and delete workflow steps on the canvas
- Delete entire workflows (both active and paused)
- Paused workflows can be edited and redeployed; active workflows cannot be edited without pausing first

### Canvas & Toolbar
- Zoom in/out controls
- Fit to screen and reset layout buttons
- Lock button (locks editing but allows panning)
- Undo/Redo functionality
- Cut (Ctrl+X), Copy (Ctrl+C), Paste (Ctrl+V) with keyboard shortcuts
- Manual node linking via drag from circular connector

### Workflow Execution Combinations
- **Ticket flows:** Trigger (Ticket Updated) > Control (Create Ticket) > Action (Add Comment) > Action (Link Ticket to Issue)
- **Issue flows:** Trigger (Issue Updated) > Action (Create Issue) > Action (Link Issue to Ticket) > Action (Add Comment)
- Variable selector picks data from previous steps

### AI-Native Steps
- **Spam Checker:** Ticket Created > Object Spam Checker > If-Else condition > Add comments for spam/not-spam
- **Sentiment Evaluator (Tickets):** Ticket Updated (Stage = Resolved) > Evaluate Sentiment > Add Comment with score. No action for unresolved.
- **Sentiment Evaluator (Conversations):** Issue Updated (Stage observed) > Evaluate Sentiment > Add Comment. No action for unresolved.

### Get Functions
- **Get Workspace & Get Account:** Ticket Created > Get Workspace (via Ticket ID) > Get Account (via Account details) > Update Ticket with workspace + comment with account
- **Get Customer:** Conversation Updated > Get Customer (via Conversation ID) > Update Ticket with customer workspace details

### Import / Export
- Export workflow as JSON via button on top right corner
- Import workflow JSON when creating a new workflow
- Cross-org import supported (export from Org 1, import into Org 2)

### List Page
- Filters: Status (Active, Paused, Draft), Created By, Created Date, Modified Date
- Filters work individually and in combination
- Customize button to show/hide columns (Status, Description, Created By)
- Workflow ID and Title maintain sequence even after deletions

### UI/UX
- Supports Light and Dark mode
- Supports Old and New Side Panel experience
- Cross-browser: Chrome, Safari, Firefox

### Display Name & Icon
- Paused workflows: Display Name and Icon can be updated, deployed, and verified in list + detail views
- Active workflows: Editing Display Name and Icon should be disabled or show an error

## Entry points
- Settings > Workflow Builder (list page)
- "+Workflow" button (top right) to create new
- Click any workflow in the list to open canvas

## Related flows
[[flows/workflow-builder-crud]]

## Related scenarios
[gap] No scenario pages created yet for individual workflow test cases.

## Complete Triggers List

| Trigger | Description |
|---------|-------------|
| `ticket_created` | New ticket created |
| `ticket_updated` | Ticket updated |
| `ticket_linked_with_object` | Ticket linked to another object |
| `ticket_sla_tracker_updated` | Ticket SLA stage changed |
| `issue_created` | New issue created |
| `issue_updated` | Issue updated |
| `issue_linked_with_object` | Issue linked to another object |
| `issue_sla_tracker_updated` | Issue SLA stage changed |
| `enhancement_created` | Enhancement created |
| `enhancement_updated` | Enhancement updated |
| `conversation_created` | Conversation created |
| `conversation_updated` | Conversation updated |
| `conversation_sla_tracker_updated` | Conversation SLA stage changed |
| `account_created` | New account created |
| `account_updated` | Account updated |
| `contact_created` | Contact (rev user) created |
| `contact_updated` | Contact updated |
| `incident_created` | Incident created |
| `incident_updated` | Incident updated |
| `opportunity_created` | Opportunity created |
| `opportunity_updated` | Opportunity updated |
| `meeting_created` | New meeting created |
| `meeting_updated` | Meeting updated |
| `meeting_deleted` | Meeting deleted |
| `meeting_linked_with_object` | Meeting linked to object |
| `article_created` | Article created |
| `article_updated` | Article updated |
| `question_answer_created` | Q&A created |
| `question_answer_updated` | Q&A updated |
| `feature_created` | Feature created |
| `csat_response_received` | CSAT response received |
| `dev_user_created` | Dev user created |
| `dev_user_updated` | Dev user updated |
| `task_updated` | Task updated |
| `timeline_comment_created` | Timeline comment created |
| `dm_created_or_updated` | DM created/updated (only if workflow's service account is a member) |
| `invoice_created` | Invoice created |
| `invoice_updated` | Invoice updated |
| `widget_created` | Widget created |
| `widget_updated` | Widget updated |
| `airdrop_sync_run_started` | AirSync run started |
| `airdrop_sync_run_status_updated` | AirSync run status updated |
| `workspace_created` | Workspace created |
| `nudge_buttons_clicked` | User clicks a button you defined |
| `ai_agent_skill_trigger` | Trigger for an AI agent skill |
| `timer_trigger` | Scheduled -- interval or cron |
| `manual_trigger` | Manually triggered by a user |
| `api_trigger` | Triggered via API call |

### Trigger Filter Conditions
Each trigger supports filter conditions on specific fields. Example for `ticket_created` / `ticket_updated`: `applies_to_part`, `tags`, `priority_v2`, `owned_by`, `rev_org`, `stage`. For `ticket_updated`, you can additionally filter on *what changed* (e.g. stage transition from "in-progress" to "resolved").

## Action Categories

### Object Creation
`CreateAccount`, `CreateContact`, `CreateIncident`, `CreateIssue`, `CreateMeeting`, `CreateOpportunity`, `CreateTicket`, `ConvertConversationToTicket`

### Object Retrieval ("Get" Functions)
`GetAccount`, `GetConversation`, `GetCustomer`, `GetEnhancement`, `GetFeature`, `GetIncident`, `GetIssue`, `GetMeeting`, `GetOpportunity`, `GetOrgUser`, `GetOrgUserPreference`, `GetPart`, `GetTicket`, `GetWorkspace`, `GetAirdropSyncUnit`, `FetchObjectContext`

### Object Updates
`UpdateAccount`, `UpdateContact`, `UpdateConversation`, `UpdateEnhancement`, `UpdateIncident`, `UpdateIssue`, `UpdateMeeting`, `UpdateOpportunity`, `UpdateQuestionAnswer`, `UpdateTicket`

### Object Linking
`LinkConversationWithTicket`, `LinkIncidentWithIssue`, `LinkIssueWithIssue`, `LinkTicketWithIssue`, `ListObjectsLinkedToIssue`, `ListObjectsLinkedToTicket`

### Communication
- `AddComment` (visibility: `external`/`internal`/`private`)
- `AskOptions` (interactive buttons)
- `NudgeButtonsClicked`
- `SendNotification`

## AI-Native Nodes

| Node | Description |
|------|-------------|
| Spam checker (`ObjectSpamChecker`) | Determines if ticket/conversation is spam |
| Suggest part (`SuggestPart`) | Suggests relevant product part for a ticket/issue |
| Sentiment evaluator (`EvaluateSentiment`) | Assesses customer sentiment (Delighted, Happy, Neutral, Unhappy, Frustrated, Unknown) |
| Ask AI (`AskAi`) | Custom LLM prompt for content generation |
| Classify object (`ClassifyObject`) | AI-based categorization into defined categories |
| Talk to agent (`TalkToAgent`) | Deploys an AI agent into a conversation |

## Control Steps -- If/Else & Router

The `if_else` node branches the workflow into **True** and **False** output ports.

**How to configure:**
1. Select a value for the LHS (left-hand side) -- use the variable selector to pick any field from a previous step.
2. Select an operator (equals, contains, greater than, less than, is empty, etc.).
3. Enter or select a value for the RHS -- can be a literal value or a reference from a previous node.

Multiple conditions can be combined with **AND/OR** logic.

**Router node** -- splits into multiple parallel paths. Each route has a name, description, and condition. By default all matching routes execute; enable **First Match Only** to stop at the first match. A **Default** route always exists as a fallback.

## Delay Steps

| Node | Behaviour | Configuration |
|------|-----------|---------------|
| `sleep_for` | Pauses for a fixed duration | Set duration (seconds, minutes, hours, days) |
| `sleep_until` | Pauses until a specific date/time | Set absolute timestamp; supports offset (add/subtract duration). If the time is already in the past, resumes immediately |
| `watch_ticket_for_updates` | Pauses until the specified ticket is updated | Provide ticket ID |

Blocking nodes pause execution without consuming resources. Existing workflow runs in a waiting state continue on the version they started with.

## Utility Operations

### ExecuteCode / RunCode
- **Runtime**: Python, sandboxed environment.
- **Structure**: Must define a `run(inputs)` function that returns a dictionary.
- **Available libraries**: `json`, `datetime`, `re`, `math`, `requests`, `collections`, `itertools`, `functools`, `string`, `random`, `decimal`, `uuid`, `base64`, `csv`, `hashlib`, `zoneinfo`, and many more.
- **Blocked libraries**: `os`, `sys`, `subprocess`, `threading`, `pickle`.
- **Inputs**: Defined in the "Input Values" section; accessed as `inputs["key"]` or `inputs.get("key", default)`.
- **Outputs**: Must be declared in the "Output Schema" section with name and type (Text, Number, Boolean, Array, Timestamp, ID) -- otherwise downstream nodes cannot access them.
- **Timeout**: Default 30 seconds, configurable up to 120 seconds. Memory limit: 256 MB.

### Http Action
- **Methods**: GET, POST, PUT, DELETE.
- **Auth methods**: Bearer token (via a saved connection), Basic, or None.
- **Configuration**: URL (static or dynamic via variable references), method, auth token connection, headers, request body.
- **Response handling**: Provide a sample JSON response to auto-generate the output schema, making response fields available to downstream steps.
- **Connections**: Go to Settings > Account > Personal Access Tokens to create a token, then add it as a connection in the HTTP step.

### Other Utility Operations
- `Echo` -- echo input values
- `GetTime` -- get current time with timezone support (returns `unix_seconds`, `timestamp`, `day`, `hour`, `minute`, `date`, `month`, `year`)
- `GoBack` -- redirects execution back to a named step, creating a loop. Use with `if_else` for exit conditions (retry logic, polling loops).
- `OasisSQLExecute` -- runs SQL against the DevRev data warehouse (same tables available in analytics/dashboards)
- `SerengetiJobExecute`

## Variable Selector
Available via the **Insert variable** button, or by typing `{{` in any text field. References outputs from previous nodes.

**Expression syntax (JSONata):**
```
$get('step_reference_key').field_name
$get('step_reference_key', 'output_port_name').field_name
$get_variable('variable_step_ref', 'variable_name')
```

**Text template syntax (for string fields):**
```
"Ticket #{% expr $get('ticket').display_id %} - {% expr $get('ticket').title %}"
```

**Error access:**
```
$get('create_issue', 'error').message
$get('create_issue', 'error').type
```

## Error Handling

### Per-step error paths
- Click the **three-dot menu** on any step > **Add error path**.
- Define a sequence of steps to execute if that step fails (e.g. send a notification, log the error).
- When a step fails, subsequent steps in the *main* path do not execute; only the error path runs.

### Retry logic
The workflow platform (Temporal-based) automatically retries retryable steps. For snap-in-based operations, retry behaviour is configurable via `max_retries` and `min_interval` in the snap-in manifest.

### Debugging
- Use the **Runs tab** to find failed runs (filter by status = "errored").
- Click a failed run > click the errored step (red X) > view Input Values and Error Details.
- Use the **dry run** feature to test a workflow with sample inputs before deploying.

### Workflow Limitations
- Default operation timeout: 30 seconds (configurable up to 120 seconds for Code node).
- Rate limits apply to external API calls.
- Custom fields must be defined before use in workflows.

## Workflow Testing
- **Dry run**: Test a workflow with sample inputs before deploying. Available from the workflow canvas.
- **Runs tab**: Top-left of the workflow. Shows all execution history with status badges (green = completed, red = errored, yellow = running, purple = waiting, grey = cancelled). Click any run to see step-by-step execution with inputs/outputs.

## Workflow Versioning

DevRev uses **semantic versioning** (e.g. `1.2.3`).

**Version states:**
- **Draft**: Unpublished working copy. Only one draft can exist at a time. Shown with a purple banner: "This is an unpublished version of the workflow."
- **Published**: The active version running in production. Marked with a "Published" tag in the version history panel.
- **Paused**: Deactivated but preserved.

**How it works:**
- All changes stay in draft until you click **Publish**.
- Publishing creates a new version; the previous version continues running for any in-flight executions.
- New runs always use the latest published version.
- All past versions are retained in the version history panel (right side of the UI) with timestamps and author info.

**Rollback:** Open a previous version in the history panel and publish it as a new version.

**Access control:** By default, only admins can edit/deploy workflows. The **Agents and Automation Admins** group has full access. Custom roles can be created at Settings > User Management > Roles.

## Conversational Workflows

DevRev also supports a distinct workflow type called **Conversational Workflows**, designed specifically for automating customer-facing conversations (as opposed to the standard event-driven workflows described above). Conversational workflows support interactive user input nodes (buttons, forms, carousels), AI agent handoff via the "Talk to Agent" step, and can be triggered by PLuG nudge events.

See [[features/conversational-workflows]] for full details.

## Open questions
- [gap] Are there limits on the number of steps in a single workflow?
- [gap] What happens when a workflow references a deleted ticket or issue?
- [gap] What are the exact rate limits for workflow execution?
