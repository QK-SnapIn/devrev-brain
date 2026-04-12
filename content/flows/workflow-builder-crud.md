---
title: "Workflow Builder CRUD Operations"
type: flow
status: draft
sources: [raw/exports/Sample.md, raw/docs/devrev-agent-dump-workflows.md]
related: [[features/workflows]], [[features/stock-objects]]
last_updated: 2026-04-12
---

# Workflow Builder CRUD Operations

## Goal
Validate full lifecycle of workflow management: creation, reading/listing, updating, deploying, and deleting workflows, including canvas interactions, execution combinations, AI steps, get functions, import/export, and UI/UX cross-browser/theme coverage.

## Preconditions
- User logged into DevRev with permissions to access Settings > Workflow Builder
- For execution tests: at least one ticket and one issue must exist in the workspace
- For AI steps: AI capabilities (spam checker, sentiment evaluator) must be enabled
- For import/export: access to a second org for cross-org import testing
- Required role: Admin or member of the **Agents and Automation Admins** group (Settings > User Management > Roles)

## Steps

### Create a New Workflow
1. Navigate to Settings > Workflow Builder
2. Click "+Workflow" button (top right) > new canvas opens
3. Add a trigger step (e.g., Ticket Updated)
4. Add control and action steps using "+" button under nodes or "+Step" in toolbar
5. Edit title and description > verify autosave
6. Deploy the workflow

### Edit an Existing Workflow
1. Open a Paused workflow from the list
2. Edit/delete steps on the canvas
3. Change title, description, status
4. Deploy and trigger to verify execution reflects changes
5. Open an Active workflow > verify editing is blocked

### Execute Ticket Flow
1. Create: Trigger (Ticket Updated) > Control (Create Ticket) > Action (Add Comment) > Action (Link Ticket to Issue)
2. Use variable selector to reference previous step data
3. Deploy and trigger > verify all steps execute sequentially

### Execute Issue Flow
1. Create: Trigger (Issue Updated) > Action (Create Issue) > Action (Link Issue to Ticket) > Action (Add Comment)
2. Use variable selector for linking
3. Deploy and trigger > verify execution

### AI Spam Checker Flow
1. Create: Trigger (Ticket Created) > Object Spam Checker > If-Else > Add Comment (spam) / Add Comment (not spam)
2. Deploy > create a ticket > verify correct comment added

### AI Sentiment Evaluator (Tickets)
1. Create: Trigger (Ticket Updated, Stage = Resolved) > Evaluate Sentiment > Add Comment with sentiment score
2. Deploy > resolve a ticket > verify sentiment comment added
3. For unresolved state: no action should execute

### AI Sentiment Evaluator (Conversations)
1. Create: Trigger (Issue Updated, Stage observed) > Evaluate Sentiment > Add Comment
2. Deploy > update issue stage > verify sentiment comment
3. For unresolved state: no action should execute

### Get Workspace & Get Account
1. Create: Trigger (Ticket A Created) > Get Workspace (Ticket ID) > Get Account (Account details) > Update Ticket B (workspace + account comment)
2. Deploy and trigger > verify sequential data flow

### Get Customer
1. Create: Trigger (Conversation Updated) > Get Customer (Conversation ID) > Update Ticket (Customer workspace details)
2. Deploy and trigger > verify data reflects

### Canvas Toolbar
1. Test Zoom In/Out, Fit to Screen, Reset Layout
2. Test Lock button (edit locked, panning allowed)
3. Test Undo/Redo with multiple steps
4. Test Cut/Copy/Paste via toolbar and keyboard shortcuts (Ctrl+X/C/V)

### Import / Export
1. Create a workflow with trigger, control, action > verify functional
2. Export via button > download JSON
3. Create new workflow > Import the JSON > verify functionality
4. Export from Org 1 > Import into Org 2 > verify no breakage
5. Validate the exported JSON structure

### Delete Workflow
1. Open a workflow > click Delete (top right) > confirm in popup
2. Navigate back to list > verify workflow no longer exists
3. Trigger the deleted workflow's action > verify no execution

### List Page Filters & Customization
1. Filter by Status (Active, Paused, Draft) individually
2. Filter by Created By (users with/without workflows)
3. Filter by Created Date and Modified Date (calendar picker)
4. Combine multiple filters > verify results
5. Remove all filters > verify all workflows displayed
6. Verify Workflow ID and Title sequence after deletions
7. Customize button: toggle Status, Description, Created By columns

### Error Handling
1. Open any step > click three-dot menu > **Add error path**
2. Add steps to the error path (e.g. send notification, log error)
3. Trigger the workflow with data that causes the step to fail
4. Verify: main path stops at the failed step; error path executes
5. Check the **Runs tab** > filter by status "errored" > click the failed run > verify Input Values and Error Details are shown on the errored step (red X)

### Versioning & Rollback
1. Create and publish a workflow (version 1.0.0)
2. Pause the workflow > make edits > verify purple draft banner appears ("This is an unpublished version of the workflow")
3. Publish again > verify new version appears in the **Version history panel** (right side) with timestamp and author
4. While a run is in-flight, publish a new version > verify the in-flight run continues on the old version
5. Open Version history panel > click a previous version > publish it as a new version (rollback test)
6. Verify only one draft can exist at a time

### Dry Run / Testing
1. Open a workflow in draft > use the **dry run** feature
2. Provide sample inputs > execute > verify step-by-step results match expectations
3. Verify the dry run does not create real objects (tickets, issues, etc.) [gap] Confirm if dry run is fully sandboxed

### Exploratory: Edge Cases
1. Remove intermediate steps (delink) > execute > verify only linked steps run
2. Create duplicate workflows > trigger > verify both execute
3. Create, verify, delete, then re-trigger > verify no execution

### UI/UX Validation
1. Validate Light and Dark mode rendering
2. Validate Old and New Side Panel experience
3. Validate across Chrome, Safari, Firefox

### Display Name & Icon
1. Paused workflow: update Display Name and Icon > deploy > verify in list and detail views
2. Active workflow: attempt update > verify editing is disabled/error shown

### Manual Node Linking
1. Create trigger, action, and control nodes
2. Remove a node's link, create a new unlinked node
3. Drag from previous node's connector to new node > verify link

## Success criteria
- All CRUD operations complete without errors
- Workflow execution follows the linked chain exactly
- AI steps produce correct spam/sentiment results
- Get functions retrieve and pass data correctly between steps
- Import/export preserves workflow structure and functionality cross-org
- Canvas toolbar controls all function correctly
- Filters and list page behave correctly individually and combined
- UI renders correctly across themes, side panel modes, and browsers

## Failure modes
- Workflow fails to save or deploy
- Active workflow allows editing (should be blocked)
- Variable selector fails to reference previous step data
- AI steps produce incorrect or no results
- Deleted workflow continues to execute
- Import corrupts workflow structure
- Canvas controls (undo/redo, zoom) malfunction
- Filters return incorrect results
- Error path does not execute when a step fails
- In-flight runs break when a new version is published
- Rollback publishes incorrect version
- Dry run creates real objects instead of being sandboxed

## Locators touched
[gap] No locator page exists yet for the Workflow Builder UI.

## API calls involved
[gap] API endpoints for workflow CRUD, execution, and AI steps not yet documented.
