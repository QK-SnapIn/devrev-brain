---
title: Build your first AI agent
devrev_id: ART-26061
parent_directory: Agent Studio
translation_group: ZqvK4VT6
modified_date: "2026-04-22T00:37:49.541Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/ZqvK4VT6"
tags: []
top_category: Computer by DevRev
wiki_match: features/build
match_score: 0.85
last_updated: 2026-05-11
related: ['features/build']
summary: "Agent Studio is currently in beta only."
---

# Build your first AI agent

Agent Studio is currently in beta only.

**Prerequisites:**

* Access to DevRev with permissions to create [[features/agents|agents]].
* At least one knowledge source, for example, [[entities/article|articles]] or [[features/tickets|tickets]] in your DevRev workspace.
* If you plan to attach workflow skills, ensure you have already built the [[features/workflows|workflows]] you intend to use.

---

## Step 1: Open Agent Studio

In the DevRev sidebar, go to [**Settings > Agent Studio**](https://app.devrev.ai/?setting=airdrop%2Fagent-studio). The Agent Studio page displays a grid of agent cards, or an empty state if no agents exist yet.

---

## Step 2: Create a new agent

Click **Create New Agent** in the top-right corner of the Agent Studio page. You are taken to the **[[features/build|Build]]** tab for your new agent.

Your agent is created with a default name ("New Agent"), a default goal, and a default guardrail already enabled.

## Step 3: Name your agent and set a goal

At the top of the Build page, you see two editable fields:

1. **Agent name**: Click the name at the top and type a meaningful name for your agent, for example, Support Assistant.
2. **Agent goal**: Below the name, click the text area and describe what your agent should do. For example:

   You are a customer support assistant. Help users resolve their [[features/issues|issues]] by searching the [[features/knowledge-base|knowledge base]] and creating tickets when necessary.

The goal gives the agent its overall direction. Be specific about the agent's purpose.

---

## Step 4: Add knowledge sources

Knowledge sources tell the agent where to look when answering questions.

1. In the **Capabilities** section, find the **Knowledge** row and click **+ Add**.
2. In the **Add Knowledge** modal, select the object types you want the agent to [[features/search|search]]. Common choices include:

   * **[[entities/article|Article]]**: Knowledge base articles.
   * **[[entities/ticket|Ticket]]**: Support tickets.
   * **Question & Answer**: Q&A entries.
   * **[[entities/conversation|Conversation]]**: Past [[features/conversations-feature|conversations]].
3. Use the search bar to filter the list if needed, then click **Add** to confirm your selection.

Your selected knowledge sources appear as chips in the Knowledge row.

---

## Step 5: Attach skills

Skills give your agent the ability to take actions such as creating tickets, sending messages, or running workflows.

1. In the **Capabilities** section, find the **Skills** row and click **+ Add**.
2. In the **Add Skill** modal, browse or search using the tabs:

   * **All**: A combined view showing operations and workflows.
   * **Operations**: Built-in DevRev actions (e.g., create a ticket, update an [[entities/issue|issue]]).
   * **Workflows**: Custom automation workflows you have already built.
3. **For operations:** After selecting one, a configuration panel opens where you can:

   * Give the skill a **name** (letters, numbers, and underscores only).
   * Add a **description** of when the agent should use this skill.
   * Configure input fields: toggle **Auto-fill** to let the agent determine values from context, or set manual defaults.
   * Toggle **Execute as User** to run the operation on behalf of the end user rather than the agent.
   * Configure **Connections** if the operation requires external integrations or keyrings.
4. **For workflows:** Select the workflow to add it directly.
5. Confirm to add the skill.

Your attached skills appear as chips in the Skills row.

> 💡 **Tip**: If you do not see any workflows in the Workflows tab, you need to create them first before you can attach them as skills.

---

## Step 6: Review guardrails

Guardrails define boundaries for what the agent can and cannot do. A **Default Guardrail** is already enabled for every new agent. The Default Guardrail is always on and cannot be toggled off or deleted.

1. In the **Capabilities** section, find the **Guardrails** row. You see the Default Guardrail with an **Always on** label.
2. To add a custom guardrail, click **+ Add**:

   * Enter a **topic name**: a short label for the guardrail.
   * Select a **type**: the category of restriction.
   * Write a **description**: the rule the agent must follow (e.g., "Never share internal pricing information with customers").
3. Click **Create** to add it.

You can toggle custom guardrails on and off, edit them, or delete them at any time.

---

## Step 7: Write instructions

Instructions provide detailed guidance for how the agent should behave. Think of them as the agent's playbook.

1. Scroll down to the **Instructions** section.
2. Click the editor area and write your instructions using rich text. Use `@` to reference specific tools or skills directly in your instructions.

**Tips for good instructions:**

* Be specific about tone and style ("Always be polite and professional").
* Define escalation rules ("If the user asks about billing, create a ticket for the billing team").
* Specify what the agent should *not* do ("Do not make promises about delivery timelines").

---

## Step 8: Test your agent in the Playground

1. Click the **Test** tab at the top of the page. You see the **Preview Tests** sub-tab with a prompt to start testing.
2. Click **Start New Chat**. A chat panel opens on the right side of the screen.
3. Type a message to your agent and press Enter. Watch as the agent responds using the knowledge and skills you configured.
4. To inspect the agent's reasoning, click **View Trace** on any response. The execution trace shows which skills, knowledge sources, and guardrails the agent invoked and the decisions it made at each step.

Try a few different questions to see how your agent handles them. If the responses are not what you expect, go back to the **Build** tab and refine the goal, instructions, or skills.

---

## Step 9: Publish your agent

Once you are satisfied with your agent's behavior:

1. Go back to the **Build** tab and click **Publish** in the top-right corner.
2. In the confirmation dialog, review the version number that will be published, then click **Publish** to confirm.

Your agent is now live. The version status changes from **Draft** to **Live**. Any previously live version is automatically archived. You can view and restore archived versions from the version history.

---

## Next steps

Now that you have built and published your first agent, explore the following topics in the [[support-articles/computer-by-devrev/agent-studio-task-reference|Agent Studio task reference]]:

* **Run bulk tests** to evaluate your agent against a dataset of test cases.
* **Monitor performance** in the Observe tab to track [[features/analytics|analytics]] and review session traces.
* **Iterate with versions** to make improvements without disrupting the live agent.

For a complete field-level reference of every feature, see the [[support-articles/computer-by-devrev/agent-studio-reference|Agent Studio reference]].

## Related wiki nodes
- [[features/build]]

## Source
- DevRev support article [Build your first AI agent](https://support.devrev.ai/en-US/devrev/article/ZqvK4VT6) (ART-26061)
