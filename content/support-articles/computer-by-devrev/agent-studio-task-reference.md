---
title: Agent Studio task reference
devrev_id: ART-26059
parent_directory: Agent Studio
translation_group: H3uk-gXI
modified_date: "2026-04-22T00:34:11.318Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/H3uk-gXI"
tags: []
top_category: Computer by DevRev
wiki_match: entities/task
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/task']
summary: "This article is intended for workspace administrators and agent builders who configure agents through the Agent Studio UI."
---

# Agent Studio task reference

Agent Studio is in beta.

This [[entities/article|article]] is intended for workspace administrators and agent builders who configure [[features/agents|agents]] through the Agent Studio UI.

## Navigate to Agent Studio

To open Agent Studio, go to [**Settings > Agent Studio**](https://app.devrev.ai/?setting=airdrop%2Fagent-studio).

To open an existing agent, select it from the agent list on the Agent Studio landing page. The agent opens in the **[[features/build|Build]]** tab, where you can view and edit its configuration.

## Create an agent

1. In [**Settings > Agent Studio**](https://app.devrev.ai/?setting=airdrop%2Fagent-studio), click **Create New Agent** in the top-right corner. If your workspace supports multiple agent types, a dropdown appears with two options:

   * **Internal**: An agent that assists internal team members, for example, an IT helpdesk agent that answers employee questions.
   * **CX (customer-facing)**: An agent that interacts directly with customers, for example, a support agent embedded in your portal or chat widget. CX agents typically use customer-facing knowledge sources and enforce stricter guardrails around sensitive information.
2. In the **Build** tab, click the agent name at the top and replace it with a meaningful name, then edit the **goal** to describe the agent's purpose.

The agent is created in **Draft** state. A Draft agent is not live and does not respond to real user messages. Use *Draft* state to configure knowledge sources, skills, guardrails, and instructions, then test the agent in the Playground before publishing.

---

## Configure knowledge sources

Knowledge sources determine which DevRev data the agent can [[features/search|search]] to answer questions.

1. Open your agent in the **Build** tab and find the **Knowledge** row in the **Capabilities** section.
2. Click **+ Add**, browse or search for the object types you want, such as Article, [[entities/ticket|Ticket]], or [[entities/conversation|Conversation]], check the boxes next to each type, and click **Add** to confirm.

To remove a knowledge source, click the **×** on its chip in the Knowledge row.

**Recommended knowledge types by use case:**

* **Customer support agent**: Article, Question & Answer.
* **Internal IT helpdesk**: Article, Ticket, Conversation.

---

## Add and configure skills

Skills give your agent the ability to perform actions, not just answer questions. The Agent Studio UI supports two skill types: built-in operations and [[features/workflows|workflows]].

### Add a built-in operation

1. Open your agent in the **Build** tab and find the **Skills** row in the **Capabilities** section, then click **+ Add**.
2. In the modal, select the **Operations** tab, browse or search for the operation you need, and click it to open the configuration panel.
3. Fill in the required fields:

   * **Name**: A unique identifier using letters, numbers, and underscores only.
   * **Description**: When the agent should use this skill (for example, "Use when the customer's [[entities/issue|issue]] cannot be resolved from the [[features/knowledge-base|knowledge base]]").
4. Configure input fields: toggle **Auto-fill** on for fields the agent should determine from conversation context, and set fixed values for fields that should always be the same.
5. Optionally, under **Settings**, configure whether the skill should execute as the user and whether it requires human-in-the-loop approval.
6. Click **Add** to attach the skill.

### Add a workflow

1. Open your agent in the **Build** tab and find the **Skills** row in the **Capabilities** section, then click **+ Add**.
2. Select the **Workflows** tab and select the workflow you want to attach. If you [[glossary/don|don]]'t see a suitable workflow, click **Create New Workflow** and confirm in the dialog that appears. A new browser tab opens with the workflow editor. Build your workflow, then return to Agent Studio and add it.
3. The workflow is added immediately with no additional configuration needed.

### Remove a skill

Click the action menu on the skill chip and select **Remove**, then confirm the removal when prompted.

---

## Set up guardrails

Guardrails enforce rules the agent must follow in every interaction.

### Add a custom guardrail

1. Open your agent in the **Build** tab and find the **Guardrails** row in the **Capabilities** section, then click **+ Add**.
2. In the create guardrail modal, fill in:

   * **Topic name**: A short label (for example, "Pricing policy").
   * **Type**: The category of restriction. The only type available is `topic_boundary`, which restricts the agent to stay within defined topic areas. The schema is designed for extensibility, and additional types may be introduced in the future.
   * **Applies To**: Whether the guardrail applies to **input** (user messages), **output** (agent responses), or **both**. This field is required and determines when the guardrail is evaluated.
   * **Description**: The rule itself (for example, "Do not share custom pricing or discount information. Direct all pricing questions to the sales team.").
3. Click **Create**.

### Toggle a guardrail

Each guardrail has a toggle switch. Turn it off to temporarily disable the rule without deleting it. A toast notification confirms the change with an **Undo** option.

### Edit a guardrail

Click the guardrail name or the edit action to open it for editing. Update the fields and save.

### Delete a guardrail

Click the delete action on the guardrail and confirm the deletion when prompted. This action cannot be undone.

The Default Guardrail is always active and cannot be toggled off or deleted.

---

## Write effective instructions

Instructions are the detailed playbook that guides your agent's behavior.

1. Open your agent in the **Build** tab.
2. Scroll down to the **Instructions** section.
3. Click the editor and write your instructions.

## Best Practices

* **Be specific about behavior:** When a customer reports a bug, ask them to describe the steps to reproduce it before searching for known [[features/issues|issues]].
* **Define escalation paths:** If the customer has been waiting more than 3 messages without resolution, offer to create a support ticket and assign it to the engineering team.
* **Set tone and style:**  Always respond in a professional but friendly tone. Use the customer's name when available.
* **Use** `@` **references:** You can reference specific knowledge sources, tools, or skills in your instructions using `@`. This creates a direct link between your guidance and the agent's capabilities.
* **Specify what the agent must not do:** Do not speculate about timelines. If the customer asks when a feature will ship, say 'I don't have visibility into the roadmap' and offer to connect them with the product team.

---

## Test your agent with the Playground

The Playground lets you have a live conversation with your agent to verify its behavior. For a comprehensive overview of testing capabilities and evaluation methodology, refer to the Testing & Evaluation Guide.

1. Navigate to your agent's **Test** tab, and under **Preview Tests**, click **Start New Chat**.
2. Type a message in the chat panel and press Enter, then review the agent's response.
3. Continue the conversation to test different scenarios.

### View execution traces

After the agent responds, click **View Trace** on the message. The trace view shows the agent's step-by-step reasoning:

* **Thought**: The agent's internal reasoning.
* **Input/Output**: What was sent to and received from each skill.
* **Guardrail Check**: Which guardrails were evaluated and their results.
* **Response Time**: How long each step took.
* **Token Consumed**: Input and output tokens consumed. This field appears in the UI trace view; availability may vary by agent version.

To clear the conversation and start over, click **Reset Session** in the Playground header.

---

## Run bulk tests

Bulk tests run your agent against a dataset of predefined inputs and evaluate the responses automatically.

You need at least one dataset with test entries before running a bulk test.

For detailed information, see **Manage datasets.**

### Run a test

1. Navigate to your agent's **Test** tab, click **Create Bulk Test** (top-right) or switch to the **Bulk Tests** sub-tab and click **Create Bulk Test**.
2. Fill in the test configuration:

   * **Test name**: A short description of the test's purpose.
   * **Agent**: The base agent (pre-selected if you started from an agent).
   * **Agent Version**: The version to test against.
   * **Dataset**: The dataset to use.
   * **Evaluators**: Check which evaluators to apply. **Correctness** measures whether the response accurately addresses the input. **Completeness** measures whether the response fully covers the expected output.
3. Click **Start Test**.

### View results

1. Go to **Test > Bulk Tests** and click a completed test to see results.
2. Each test entry shows:

   * **Status**: Queued, Running, Completed, or Errored.
   * **Input**: The test question.
   * **Expected Output**: What you expected.
   * **Output**: What the agent produced.
   * **Correctness** and **Completeness** scores with explanations.
   * **Latency**: Response time.

## Manage datasets

Datasets are collections of test cases used for bulk testing.

### View datasets

1. On the **Agent Studio** list page, click the **settings gear icon** in the header, then select **Datasets**.
2. The Datasets page shows all datasets with columns for Name, Description, Entries, Test Runs, Created By, and Date Created.

### Import a dataset

1. On the Datasets page, click **Import Dataset**.
2. In the import modal:

   * **Download the template** to see the expected CSV format.
   * **Upload your file** by dragging and dropping or clicking to browse. The file must be a CSV. The modal displays the maximum allowed file size; uploads that exceed this limit are rejected.
   * **Name**: Give the dataset a descriptive name.
   * **Description** (optional): Add context about what this dataset tests.
3. Click **Import** to upload.

The maximum dataset file size is shown in the import modal and may vary. If your file exceeds the displayed limit, split it into smaller datasets before importing.

### View dataset entries

1. Click a dataset name to open its detail page.
2. The **Entries** tab shows all test cases with columns:

   * **Input**: The user message to test.
   * **Expected Output**: The ideal agent response.
   * **Remarks**: Additional notes.

### Run a test from a dataset

1. On the dataset detail page, click **Run Test**.
2. This opens the Create Bulk Test form with the dataset pre-selected.

---

## Publish an agent version

Publishing makes your draft configuration live.

1. Open your agent in the **Build** tab and ensure you have finished editing the draft.
2. Click **Publish** in the top-right corner.
3. A confirmation dialog shows the version number being published and the draft label.
4. Click **Publish** to confirm.

The version state changes from **Draft** to **Live**. The previously live version is automatically archived.

---

## Deploy an agent to a channel

After publishing, create a deployment workflow to connect your agent to a channel where customers can interact with it.

### Deploy a customer-facing agent

1. Click the **Configure** button in Agent Studio to auto-generate a workflow, or navigate to **Workflows** in DevRev to create one manually.
2. Add a **Conversation Created** trigger node. This fires whenever a customer starts a new conversation (via [[glossary/plug|Plug]] chat, email, or another channel). To filter by channel, add an if/else node immediately after the trigger.
3. Add a **Talk to Agent** action node and connect it to the trigger.
4. Configure the Talk to Agent node:

   * **Agent**: Select your published agent.
   * **Object**: Conversation.
   * **Visibility**: External.
   * **Panel**: Customer Chat.
   * **Respond to User Types**: customer.
5. (Optional) Configure advanced settings:

   * **Suspend on Message From**: Set to **user** to pause the agent when a human team member joins the conversation.
   * **Quick Replies**: Add preset response buttons the customer can click.
   * **Additional Context**: Inject extra information for the agent to use.
6. Save and activate the workflow.

---

## Restore a previous version

If a published version introduces issues, you can restore an earlier version.

1. Open your agent in the **Build** tab.
2. In the top-right corner, locate the **clock** icon to the left of the **Publish** button. Click it to open the **Version History** panel.
3. Browse the timeline of all versions, then click the version you want to restore.
4. Select the **Restore** action.
5. A confirmation dialog shows the version details. Click **Restore**.

This creates a new draft based on the selected version's configuration. Review the draft and publish it when ready.

Restoring does not delete or modify the existing version history. It creates a new draft.

---

## Monitor agent performance

The **Observe** tab provides [[features/analytics|analytics]] and session history for your agent.

### Enable analytics

1. Open your agent and go to **Observe > Analytics**.
2. If metrics collection is not yet enabled, click **Enable Evaluation** to start collecting data.

Once enabled, the Analytics page displays a dashboard of performance metrics filtered to your agent. The default time range is the last 7 days.

### View session history

1. Go to **Observe > Sessions**.
2. The sessions table lists all [[features/conversations-feature|conversations]] with columns for Trigger, Members, and Last Message. Use the filters at the top to narrow results by time range or trigger type.
3. Click a session to view its full detail and execution trace.

---

## Investigate a session trace

Session traces show exactly how the agent processed a conversation.

1. Navigate to **Observe > Sessions** and click a session.
2. The session detail page shows participants, timestamps, trigger information, and the full message history.
3. Click any agent message to inspect its trace:

   * **LLM Reasoning**: The agent's thought process.
   * **Skill invocations**: Which skills were called, with their inputs and outputs.
   * **Knowledge retrieval**: What information the agent found.
   * **Guardrail checks**: Which guardrails were evaluated and whether they passed.
   * **Response time**: Duration of each step.

Use traces to diagnose unexpected responses, verify that skills are invoked correctly, and identify [[entities/opportunity|opportunities]] to improve instructions or guardrails.

---

## Delete an agent

1. Open the agent you want to delete.
2. Click the **more options menu** (three-dot icon) in the agent header, then select **Delete**.
3. A confirmation dialog appears. Confirm the deletion.

⚠️ **Warning**: Deleting an agent is permanent and cannot be undone. All versions, test history, and session data for this agent are removed. Any active conversations that rely on the deleted agent lose access to its configuration and skills; those conversations can no longer receive agent-generated responses. Ensure the agent is not serving live traffic before deleting it, or reassign active workflows to another agent first.

## Related wiki nodes
- [[entities/task]]

## Source
- DevRev support article [Agent Studio task reference](https://support.devrev.ai/en-US/devrev/article/H3uk-gXI) (ART-26059)
