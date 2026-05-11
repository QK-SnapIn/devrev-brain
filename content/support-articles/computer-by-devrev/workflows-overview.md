---
title: Workflows Overview
devrev_id: ART-21836
parent_directory: Workflow engine
translation_group: JXCETTW_
modified_date: "2026-04-28T20:59:17.726Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/JXCETTW_"
tags: []
top_category: Computer by DevRev
wiki_match: features/workflows
match_score: 0.647
last_updated: 2026-05-11
summary: "A workflow is a series of triggers, actions, and conditions designed to achieve a specific goal or outcome."
---

# Workflows Overview

A workflow is a series of triggers, actions, and conditions designed to achieve a specific goal or outcome. Depicted as a flowchart or diagram, it illustrates how various triggers and actions interconnect.

DevRev’s workflow engine automates tedious [[entities/task|tasks]], providing precise control and efficiency. Leveraging AI through Computer, it creates adaptive, real-time [[features/workflows|workflows]] that handle complex tasks with minimal human intervention. [[features/agents|AI agents]] interpret and execute tasks based on fuzzy inputs, enhancing productivity and efficiency. This shift from rigid workflows to adaptive automation aims to improve organizational processes and outcomes.

The workflow engine is a highly flexible solution enabling users to [[features/build|build]] personalized workflows tailored to their organization’s needs. Catering to both high-code and no-code users, it simplifies the creation of complex automations.

With our pre-built library of workflow nodes for common tasks, users can quickly implement powerful functions without writing custom code.

This combination of flexibility and a robust pre-built library ensures that you can easily design workflows that perfectly fit your organizational requirements.

## Key features

- **AI-powered automation**: Utilize out-of-the-box AI-based nodes and AI generation capabilities for intelligent automation that enhances productivity.
- **No middleware**: Our workflow engine is natively built into the CRM system, eliminating the need for third-party tools and additional training.
- **Scalable performance**: Handle thousands to millions of executions per day effortlessly with our scalable workflow engine.
- **Automations on one schema**: Our [[glossary/airsync|AirSync]] feature automatically transforms data from different sources. It enables you to create workflows natively in DevRev without the need to create fetch nodes or manually transform data.

## Components

- Workflow canvas: The field where you connect and visualize different steps in your workflow.
- Steps: The building blocks of your workflow, shown on the canvas.
- Variable selector: Used to insert variables into your steps during configuration. The variable selector is available through the **Insert variable** button. Entering double open curly braces (`{{`) in the text field is a shortcut to a compact list of available variables.
- Toolbar: Located at the bottom of your screen, it provides tools to add new steps, align steps, zoom in/out, and more.

## Workflow steps

Workflow steps are categorized into the following types:

- Trigger: The event that initiates a particular process.
- Action: Tasks that modify one or more objects in the system.
- Control: Conditional (if-then) blocks to determine which actions to take based on an operand (variable) and an operator.
- Delay: Wait to take an action.

## AI nodes

We provide several native AI nodes out of the box to enhance your workflows.

**Spam checker**

The spam checker takes the ID of a [[entities/ticket|ticket]] or object and determines whether the ticket or [[entities/conversation|conversation]] is spam. You can use this output in your workflows as needed. For example, if the ticket is found to be spam, you can automatically add a comment to the ticket.

**Suggest [[entities/part|part]]**

Often, your integrations create [[features/tickets|tickets]] or [[features/issues|issues]] associated with a default part. The suggest part takes the ID of a ticket or [[entities/issue|issue]] and suggests a relevant part. You can use this to route your tickets or issues to the most appropriate part of the product. For example, when a ticket is created, you can find a relevant part and update the ticket with the suggested part.

**Sentiment evaluator**

The sentiment evaluator takes the ID of a ticket and assesses the customer's sentiment based on their comments. Sentiment values can be *Delighted*, *Happy*, *Frustrated*, *Neutral*, *Unhappy*, or *Unknown*. It also provides justification for the sentiment values. These values are only generated if there is a customer conversation on the ticket. For example, you can listen to a ticket update event, evaluate the sentiment, and send a comment to the [[entities/account|account]].

**Ask AI**

Write your own LLM prompt to generate content that can be used in various contexts. For example, you can request a summary of a ticket based on the title and description.

## Creating a workflow

1. Go to **[Settings](https://app.devrev.ai/?setting=workflows)**[ > ](https://app.devrev.ai/?setting=workflows)**[Workflows](https://app.devrev.ai/?setting=workflows)**. A canvas appears.
2. Enter a name for your workflow.
3. Select the steps you want to include by selecting them from the button toolbar.
4. Set your triggers. You can have multiple triggers within a single workflow.
5. To configure your workflow, utilize the data reference pane to select values from previous nodes.
6. Connect steps with multiple paths as needed, allowing for the management of complex workflows on one canvas.
7. To add conditional logic, use a control step.Select a value for the LHS; select the appropriate operator; and enter or select a value for the RHS, which can be a literal value or one from a previous node.
8. Click **Deploy**.
9. If you need to modify the workflow after is has been deployed, click **Pause**, edit the workflow, then click **Deploy** to reactivate it.

## Workflow example: Ticket auto-response

![Workflow Engine Example Diagram](don:core:dvrv-us-1:devo/0:artifact/4099829)

## Source
- DevRev support [[entities/article|article]] [Workflows Overview](https://support.devrev.ai/en-US/devrev/article/JXCETTW_) (ART-21836)
