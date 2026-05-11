---
title: Deploy agents to channels
devrev_id: ART-26062
parent_directory: Agent Studio
translation_group: XPm1n5YA
modified_date: "2026-04-22T00:41:58.514Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/XPm1n5YA"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/mcp
match_score: 0.431
last_updated: 2026-05-11
---

# Deploy agents to channels

You've built an agent, tested it, and published a version. Now what? Your agent is ready but not yet connected to any channel where users can actually talk to it. That's what deployment does. Deployment connects a published agent to one or more channels so real users can interact with it.

## Publishing vs. deploying

In Agent Studio, **publishing** and **deploying** are two separate steps:

* **Publishing** makes a version of your agent's configuration active.
* **Deploying** connects that published agent to a channel — Plug chat, email, Slack, or WhatsApp — so real users can interact with it.

Publishing prepares the agent; deploying opens the door.

## Prerequisites

### Channels must be active

Before your agent can receive messages from a channel, that channel must be set up and creating conversations in DevRev. The deployment workflow reacts to events like "Conversation Started." If no conversations are being created from a channel, the agent has nothing to respond to.

Make sure the channels you want to deploy on are active:

* **Plug**: Plug must be enabled and the Plug widget installed on your website or app. Configure this in [Settings > Plug & Portal](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration).
* **Email**: The Email snap-in must be installed and configured with your support email address. Install it from the DevRev Marketplace.
* **Slack**: The Slack snap-in must be installed and connected to your Slack workspace. Install it from the DevRev Marketplace.
* **WhatsApp**: The WhatsApp snap-in must be installed and configured with your WhatsApp Business account. Install it from the DevRev Marketplace.

Once a channel is active, it automatically creates Conversation objects in DevRev when users reach out. Those conversations are what your deployment workflow's trigger listens for.

If your agent isn't responding, first verify that conversations are actually being created from the channel. Navigate to the Conversations list in DevRev and confirm that incoming messages appear. If they don't, the channel setup is the issue, not the agent.

## How deployment works

### Workflow model

Deployment in DevRev is driven by **workflows**, not by a simple on/off toggle. A deployment workflow has two parts:

```
  TRIGGER                    TALK TO AGENT
  "When this event           "Route it to
   happens…"        ──────►   this agent…"
```

1. A **trigger** fires when something happens — a customer starts a conversation, or a ticket is created.
2. The **Talk to Agent** node receives that event and hands it to your agent, which then responds.

### Quick setup vs. manual setup

There are two ways to create a deployment workflow:

**Quick setup (Configure button)**

Agent Studio provides a **Configure** button that creates a ready-made deployment workflow with sensible defaults on the Plug channel. This is the fastest way to get your agent live. You can customize the workflow later.

**Manual setup**

You can build a deployment workflow from scratch in the [Workflows editor](https://app.devrev.ai/?view=workflows). This gives you full control: add conditions, route to different agents, or combine the Talk to Agent node with other actions.

Both approaches create the same kind of workflow. The Configure button saves you the manual steps, and you can customize the predefined template afterward.

### Talk to Agent vs. Ask Agent

The Talk to Agent node and the Ask Agent node serve different purposes:

* **Talk to Agent** is a one-way handoff. The workflow passes the conversation to the agent, and the agent takes over. Control does not return to the originating workflow.
* **Ask Agent** supports two-way communication using a session key. The workflow sends a query to the agent, receives a response, and can continue executing subsequent steps. Use Ask Agent when you need the agent's output as an intermediate step in a larger workflow.

Choose Talk to Agent for standard deployment scenarios where the agent owns the full interaction. Choose Ask Agent when the agent acts as a skill within a broader workflow.

### Advantages of workflow-based deployment

A simple "deploy" toggle would work for basic cases, but workflows provide capabilities that a toggle cannot:

* **Conditional routing**: Route VIP customers to a premium agent and everyone else to a standard agent.
* **Multi-step flows**: Create a ticket before handing the conversation to an agent, or send a CSAT survey after the agent exits the conversation.
* **Channel-specific behavior**: Deploy the same agent on Plug with external visibility and on DMs with internal visibility.
* **Gradual rollout**: Start with one channel, observe, then expand.

---

## Talk to Agent node reference

The Talk to Agent node is the core of every deployment. It bridges an incoming event and your agent. Each field is described below.

### Agent

Selects which agent handles the interaction. Pick the agent you want to deploy. Only published agents respond to real users — if the agent has only a draft version, it is not active.

### Object

Tells the agent what type of object the incoming event concerns.

* **Conversation**: Customer-facing interactions (Plug chat, email, Slack, WhatsApp).
* **Ticket**: Agent responding on a ticket thread, typically created via portal or email.

This must match the trigger. If your trigger fires on "Conversation Started," set the object to Conversation.

### Visibility

Controls who can see the agent's responses.

* **External**: Everyone, including customers. Use this for customer-facing agents.
* **Internal**: Only your team (users). Customers cannot see the response. Use this for internal assistants or when the agent drafts a response for a human to review before sending.

### Panel

Controls where in the conversation the agent's response appears.

* **Customer Chat**: The main conversation thread that customers see. This is the default and the right choice for most deployments.
* **Discussions**: The internal discussions panel, visible only to your team. Use this when the agent should assist your team behind the scenes.

### Respond to user types

Filters which users the agent responds to.

* **Customer**: Customer users. Choose this for customer-facing agents.
* **User**: Internal team members. Choose this for internal agents. Requires `access_level` set to `internal`.

If a message comes from a user type that doesn't match this setting, the agent ignores it.

### Suspend on message from

Pauses the agent when a specific type of user sends a message. This is the **human handoff** mechanism. The most common setup:

💡 **Tip**: Set **Suspend on Message From** to **User** so the agent responds to customer messages automatically but stops as soon as a human team member sends a message. This prevents both a human and an AI agent from replying at the same time.

The agent stays suspended for the remainder of that conversation. New conversations still go through the agent as normal.

### Quick replies

Adds preset clickable response buttons for the user. Quick replies are short, predefined options that appear as buttons below the agent's message. Instead of typing, the user can click one. Examples:

* "Yes, that helped"
* "No, I need more help"
* "Talk to a human"

Quick replies guide the conversation and reduce friction, especially for common paths.

### Additional context

Injects extra information into the agent's context before it responds. Use this to give the agent information it wouldn't otherwise have. For example:

* The customer's subscription tier.
* The page the customer was on when they started the chat.
* A specific instruction for this channel ("On this channel, always respond in Spanish").

This text is added to the agent's context alongside its goal, instructions, and knowledge, giving it a richer understanding of the situation.

## Deployment recipes

### Recipe 1: Deploy an agent on Plug chat

This is the most common deployment, a customer-facing agent that responds to incoming conversations.

1. Open Agent Studio and navigate to your published agent.

   Agent Studio is currently in beta only.
2. Click **Configure** to auto-create a deployment workflow, or create the workflow manually:

   1. Go to **Workflows** and create a new workflow.
   2. Add a **Conversation Created** trigger.
   3. Add a **Talk to Agent** node with the following settings:

      * **Agent**: Your agent
      * **Object**: Conversation
      * **Visibility**: External
      * **Panel**: Customer Chat
      * **Respond to User Types**: Customer
      * **Suspend on Message From**: User
3. Save and activate the workflow.

⚠️ **Warning**: A workflow that is not activated does not run. This is one of the most common reasons an agent does not respond. Always confirm the workflow status is **Active** before testing.

Whenever a customer starts a conversation on Plug, your agent responds. If a team member sends a message, the agent steps back.

### Recipe 2: Deploy the same agent on multiple channels

You want one agent to handle Plug chat *and* email conversations in a single workflow.

The **Conversation Created** trigger outputs a **Channel** attribute that indicates where the conversation originated (Plug, Email, Slack, etc.). Use **If/Else** nodes to branch based on this value.

```
  Conversation Created
        ↓
    ┌─────────┐
    │ If/Else │
    └────┬────┘
         ├── Channel = Plug ──► Talk to Agent (Visibility: External, Panel: Customer Chat)
         │
         ├── Channel = Email ──► Talk to Agent (Visibility: External, Panel: Customer Chat)
         │
         └── Otherwise ──► (no action, or a fallback)
```

1. Create a single workflow.
2. Add a **Conversation Created** trigger.
3. Add an **If/Else** node. In the condition, select the **Channel** attribute from the trigger output.
4. Add a branch for **Plug** and connect it to a Talk to Agent node configured for Plug.
5. Add a branch for **Email** and connect it to another Talk to Agent node configured for email. You may want different quick replies or additional context per channel.
6. Save and activate the workflow.

Keeping everything in a single workflow makes channel routing easier to manage and avoids the risk of duplicate workflows accidentally causing double responses.

💡**Tip**: If both channels use the exact same Talk to Agent configuration, have both If/Else branches point to the same Talk to Agent node. Only create separate nodes when the configuration differs per channel (for example, different visibility, quick replies, or additional context).

### Recipe 3: Set up human handoff

You want the agent to handle initial conversations but step aside when a human takes over.

In the Talk to Agent node, set **Suspend on Message From** to **User**.

The resulting flow:

1. Customer sends a message and the agent responds.
2. Customer asks for a human. The agent can create a ticket or notify your team if configured as a skill.
3. A team member sends a message in the conversation and the agent automatically stops responding.
4. The human handles the rest of that conversation. The agent remains suspended for the entire conversation and does not resume, even if the human leaves. New conversations still route to the agent normally.

### Recipe 4: Add quick replies for guided conversations

You want to guide customers through common paths without requiring them to type.

In the Talk to Agent node, add **Quick Replies**:

```
- "I have a billing question"
- "I need technical support"
- "I want to check my order status"
```

The customer sees these as clickable buttons after the agent's initial greeting. Clicking one sends that text as a message, and the agent responds accordingly. This works especially well for agents with clearly defined skill areas.

---

## How it all fits together

### What happens at runtime

Here is the full sequence when a customer sends a message on Plug chat:

```
1. Customer opens Plug widget and types a message
       ↓
2. DevRev creates a Conversation object
       ↓
3. "Conversation Created" trigger fires
       ↓
4. Workflow engine routes to the Talk to Agent node
       ↓
5. Talk to Agent checks configuration:
   - Is the message from a customer? (Respond to User Types check)
   - Has a user sent a message? (Suspend check)
       ↓
6. Agent receives the message with:
   - Its goal, instructions, and guardrails
   - Access to configured knowledge sources
   - Available skills
   - Any additional context from the node
       ↓
7. Agent reasons, searches knowledge, optionally invokes skills
       ↓
8. Agent sends a response back to the conversation
   (visible per the Visibility setting, in the configured Panel)
```

A successfully running deployment workflow shows a status of **Running**, not "Completed." The workflow remains active because it continues to listen for new conversations. A "Running" status is the expected healthy state and does not indicate a problem.

### Versioning and deployment

When you publish a new agent version, all new conversations automatically use the new version. Conversations already in progress continue with the version they started with. You can safely publish and iterate without breaking active conversations.

---

## Common pitfalls

The issues below are the most frequently encountered deployment problems.

* **Issue**: Agent responds twice to every message.

  **Solution**: Two active workflows deploy an agent on the same trigger and channel. Deactivate the duplicate. This often happens when the **Configure** button creates a workflow and a second manual workflow covers the same channel.
* **Issue**: The auto-created workflow from the **Configure** button behaves unexpectedly or needs modification.

  **Solution**: The **Configure** button creates a standard workflow with a **Conversation Created** trigger and a **Talk to Agent** node pre-filled with defaults (Visibility: External, Panel: Customer Chat, Respond to User Types: Customer). Find this workflow in your Workflows list to review, edit, or deactivate it. If you later create a manual workflow for the same channel, deactivate the auto-created one first.
* **Issue**: Agent does not resume after a human leaves the conversation.

  **Solution**: Suspension is permanent for the conversation. Once a user sends a message and the agent suspends, it does not respond again in that conversation. New conversations still route to the agent normally.
* **Issue**: Customers cannot see agent responses, or responses appear in the wrong panel.

  **Solution**: Verify that **Visibility** is set to **External** and **Panel** is set to **Customer Chat**. Setting Visibility to Internal makes responses visible only to your team. Setting Panel to Discussions routes responses to the internal sidebar.
* **Issue**: Agent does not respond to test messages sent by a team member.

  **Solution**: If **Respond to User Types** is set to **Customer**, the agent ignores messages from users. Test with a customer account or temporarily adjust the setting.
* **Issue**: Agent does not respond at all, and no workflow runs appear.

  **Solution**: Verify that the channel snap-in is installed and configured. The deployment workflow listens for events like "Conversation Created," but if the channel is not set up, no conversations are created and the workflow never fires. Confirm that Plug is enabled in **Settings > Plug & Portal**, or that the relevant Email, Slack, or WhatsApp snap-in is installed from the Marketplace and properly configured. Also confirm the workflow is **activated** — an inactive workflow does not run.
* **Issue**: Workflow changes do not seem to take effect.

  **Solution**: Updates to a deployment workflow (changed visibility, added quick replies, switched agents) apply to new conversations only. Conversations already in progress continue with their original configuration.

## Source
- DevRev support article [Deploy agents to channels](https://support.devrev.ai/en-US/devrev/article/XPm1n5YA) (ART-26062)
