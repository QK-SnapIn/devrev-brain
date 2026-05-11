---
title: Agent Studio reference
devrev_id: ART-26060
parent_directory: Agent Studio
translation_group: kIjLyjeT
modified_date: "2026-04-22T00:36:07.568Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/kIjLyjeT"
tags: []
top_category: Computer by DevRev
wiki_match: features/agents
match_score: 0.387
last_updated: 2026-05-11
---

# Agent Studio reference

Agent Studio is in beta.

## Agent Studio list page

**Location:** [Settings > Agents](https://app.devrev.ai/?setting=agents)

The list page displays all agents in your workspace as a card grid.

### Agent card

Each card shows:

* **Name**: The agent's display name.
* **Goal**: The agent's high-level objective (truncated).
* **Version**: Current version label (for example, "Version: Draft" or "Version: 1.0").

### Header actions

* **Create New Agent**: Creates a new agent with default configuration.
* **Settings (gear icon)**: Opens a menu with access to the Datasets page.

### Pagination

The list uses cursor-based pagination. Navigation controls appear at the bottom when there are more agents than fit on one page.

---

## Build tab

**Location:** [Settings > Agents](https://app.devrev.ai/?setting=agents) > [Agent Name] > Build

The Build tab is where you configure all aspects of your agent.

### Agent identity

* **Agent Name**: Display name shown to users. Click to edit; saved on blur.
* **Agent Goal**: High-level objective. Auto-resizing text area, saved on blur. Reverts if left empty.

### Capabilities section

The Capabilities section contains three configurable areas: Knowledge, Skills, and Guardrails.

### Knowledge

Defines which DevRev object types the agent can search.

**Available object types:**

| Category | Types |
| --- | --- |
| **Content** | Article, Question & Answer |
| **Work items** | Ticket, Issue, Task, Enhancement, Incident |
| **Product** | Product, Feature, Capability, Component |
| **People** | Customer, User, Group |
| **Organizations** | Account, Workspace |
| **Conversations** | Conversation, Direct Message |
| **Other** | Custom Object, Dashboard, Dataset, Meeting, Microservice, Opportunity, Tag, Widget, Linkable, Runnable, Vista, Service Account |

Each knowledge source appears as a chip showing the object type's icon and name. Click **×** to remove.

### Skills

Defines the actions the agent can perform.

**Skill types:**

| Type | Description | Configuration |
| --- | --- | --- |
| **Tools** | Built-in DevRev API actions | Requires name, description, and input field configuration |
| **Workflows** | Custom automation workflows | Added directly with no additional configuration |

**Operation configuration fields:**

| Field | Required | Description |
| --- | --- | --- |
| **Name** | Yes | Unique identifier. Must match `^[a-zA-Z0-9_]+$` (letters, numbers, underscores only) |
| **Description** | Yes | When the agent should use this skill |
| **Input fields** | Varies | Each field can be set to Auto-fill (agent determines value) or Manual (fixed value) |
| **Execute as User** | No | Toggle under Settings. When on, the skill runs with the user's permissions. Default: on |
| **Needs Approval** | No | Toggle under Settings. When on, the agent requests user confirmation before executing the skill. Default: off |
| **Connections** | Varies | If the operation requires external connections, you must select the appropriate keyrings |

### Guardrails

Defines rules and boundaries the agent must follow.

**Guardrail fields:**

| Field | Required | Description |
| --- | --- | --- |
| **Topic Name** | Yes | Short label for the guardrail |
| **Type** | Yes | Category of restriction. The only supported value is `topic_boundary` |
| **Description** | Yes | The rule the agent must follow |

**Guardrail states:**

* **Enabled**: Guardrail is actively enforced.
* **Disabled**: Guardrail exists but is not enforced.
* **Always on**: Cannot be toggled off (Default Guardrail only).

**Default Guardrail:** Every agent has a built-in Default Guardrail that is always active. It provides baseline safety behavior and cannot be disabled or deleted.

### Instructions section

A rich text editor for writing detailed behavioral guidance.

* **Rich text formatting**: Supports Markdown-style formatting.
* **`@` mentions**: Reference specific knowledge sources, tools, or skills inline.
* **Auto-save**: Changes are saved automatically as you type.

### Top-line controls

Controls that appear in the Build tab header:

* **Version status badge**: Shows the current state—Draft or Live.
* **Version History toggle**: Opens the version history side panel.
* **Playground toggle**: Opens the chat playground side panel.
* **Publish button**: Publishes the current draft version.
* **More options menu**: Agent-level actions (Duplicate, Delete).

---

## Test tab

**Location:** [Settings > Agents](https://app.devrev.ai/?setting=agents) > [Agent Name] > Test

The Test tab provides tools for validating agent behavior.

### Preview tests sub-tab

Interactive testing through the Playground.

* **Start New Chat**: Opens a fresh Playground conversation.
* **Test session list**: Shows previous test conversations.
* **View Trace**: Opens the execution trace for a session.

Clicking a test session row opens the Playground loaded with that session's conversation.

### Bulk tests sub-tab

Structured testing against datasets.

* **Create Bulk Test**: Opens the bulk test creation form.
* **Bulk test list**: Shows all bulk tests with status and results.

### Create bulk test form

| Field | Required | Description |
| --- | --- | --- |
| **Test name** | Yes | Short description of the test's purpose |
| **Agent** | Yes | Base agent to test (pre-selected from context) |
| **Agent Version** | Yes | Specific version to test |
| **Dataset** | Yes | Dataset to run the test against |
| **Evaluators** | No | Correctness and/or Completeness |

### Evaluators

* **Correctness**: Measures whether the agent's response accurately addresses the input. Returns a score from 0.0 to 1.0 with an explanation.
* **Completeness**: Measures whether the response fully covers the expected output. Returns a score from 0.0 to 1.0 with an explanation.

### Bulk test results columns

| Column | Description |
| --- | --- |
| **Status** | Queued, Running, Completed, or Errored |
| **Input** | The test input sent to the agent |
| **Expected Output** | The expected response from the dataset |
| **Output** | The agent's actual response |
| **Latency** | Time taken to generate the response |
| **Correctness** | Score (0.0–1.0) and explanation |
| **Completeness** | Score (0.0–1.0) and explanation |

### Bulk test statuses

* **Queued**: Test entry is waiting to be processed.
* **Running**: Agent is processing this test entry.
* **Completed**: Test entry finished successfully.
* **Errored**: Test entry failed to complete.

---

## Observe tab

**Location:** Agent Studio > [Agent Name] > Observe

The Observe tab provides monitoring and analysis tools for agent performance and conversation history.

### Analytics sub-tab

The Analytics sub-tab displays a performance dashboard for the agent. The dashboard has three possible states:

* **Not enabled**: Shows "Metrics collection for this agent is not enabled" with an **Enable Evaluation** button.
* **Enabling**: Shows a loading state while analytics is being set up.
* **Active**: Displays the analytics dashboard filtered to this agent, defaulting to the last 7 days.

### Sessions sub-tab

The Sessions sub-tab shows all conversations the agent has participated in.

**Session list columns:**

* **Trigger**: What initiated the conversation (not sortable).
* **Members**: Participants in the conversation (sortable).
* **Last message**: Timestamp of the most recent message (sortable).

**Session list filters:**

* **Last message**: Filter by time range.
* **Trigger**: Filter by conversation trigger type.

### Session detail view

Clicking a session opens its detail page, which contains the following sections:

* **Session header**: Participants, timestamps, and trigger information.
* **Conversation**: Full message history.
* **Execution trace**: Step-by-step agent reasoning for each message.

### Trace elements

Each execution trace can contain the following elements:

* **Thought**: The agent's internal reasoning process.
* **LLM Reasoning (intermediate)**: Reasoning steps during processing.
* **LLM Reasoning (final)**: Final reasoning before responding.
* **Input**: Data sent to a skill or knowledge source.
* **Output**: Data received back from a skill or knowledge source.
* **Guardrail Check**: Guardrail evaluation results.
* **Response Time**: Duration of each processing step.
* **View Workflow**: Link to view the executed workflow, if applicable.

---

## Version management

### Version states

* **Draft**: Work-in-progress version that is freely editable. Only one draft exists at a time.
* **Live (Published)**: The active version serving users. Only one live version exists at a time.
* **Archived**: A previously published version, preserved for history.

### Version actions

* **Edit**: Modify any field on a draft version. Editing a live version auto-creates a new draft.
* **Publish**: Promote the current draft to live. This archives the previous live version.
* **Restore**: Create a new draft from any previous version's configuration.

### Version history panel

Access the version history panel via the version history toggle in the Build tab header. The panel contains:

* **Version timeline**: Chronological list of all versions.
* **Version label**: Displayed in the format "V{number} · {status}".
* **Status events**: Created, Edited, Published, and Archived — each with the user and timestamp.
* **View Older History**: Loads more versions beyond the initial set.
* **Actions menu**: Per-version actions such as Restore.

### Publish confirmation dialog

When publishing, a confirmation dialog appears with the following elements:

* **Version number**: The version being published.
* **Current draft label**: Identifies the draft being promoted.
* **Publish button**: Confirms and publishes the version.
* **Cancel button**: Returns without publishing.

### Restore confirmation dialog

When restoring, a confirmation dialog appears with the following elements:

* **Target version**: The version being restored, including its number and state.
* **Description**: Explains that a new draft will be created from this version.
* **Restore button**: Confirms and creates the new draft.

---

## Datasets

**Location:** Agent Studio > Settings (gear) > Datasets

Datasets contain collections of test cases used for bulk testing of agents.

### Datasets list

* **Name**: Dataset name.
* **Description**: Optional description.
* **Entries**: Number of test cases.
* **Test Runs**: Number of bulk tests run against this dataset.
* **Created By**: User who created the dataset.
* **Date Created**: Creation timestamp.

### Import dataset dialog

To import a dataset, provide the following fields:

* **File** (required): CSV file upload via drag-and-drop or browse. The file must not exceed the maximum size limit. The CSV must contain three columns: `Input`, `Expected Output`, and `Remarks`. A downloadable CSV template is provided in the dialog to show the expected format.
* **Name** (required): Display name for the dataset.
* **Description** (optional): Context about what the dataset tests.

The file and name fields are required. The uploaded CSV file must not exceed the maximum size limit.

### Dataset detail page

The detail page contains two tabs:

* **Entries**: List of test cases showing Input, Expected Output, and Remarks columns.
* **Completed Tests**: Bulk tests that have been run against this dataset.

Available actions on the detail page:

* **Run Test**: Opens the Create Bulk Test form with this dataset pre-selected.
* **Owned By**: Shows the dataset owner.

---

## Agent types

| Type | Description | Audience | Available channels |
| --- | --- | --- | --- |
| **Internal** [Coming soon] | For employees and internal workflows | Internal teams | — |
| **CX (External)** | For customer-facing interactions | End customers | Slack, WhatsApp, Plug Chat, Email |

Agent type is selected during creation and determines the agent's access level and available channels.

## Source
- DevRev support article [Agent Studio reference](https://support.devrev.ai/en-US/devrev/article/kIjLyjeT) (ART-26060)
