---
title: Router node
devrev_id: ART-23384
parent_directory: Workflow engine
translation_group: rJS1COSx
modified_date: "2026-01-28T17:44:03.774Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/rJS1COSx"
tags: []
top_category: Computer by DevRev
wiki_match: overview
match_score: 0.519
last_updated: 2026-05-11
summary: "The Router node enables you to split a workflow into multiple parallel paths based on conditions."
---

# Router node

The Router node enables you to split a workflow into multiple parallel paths based on conditions. Instead of building deeply nested if-else structures, you can define routes where each route executes independently when its condition is met.

```
┌─ Trigger ─────────┐
│                   │
│    Router Node    │
│                   │
├─ Route 1 ──→ [Actions] (if condition matches)
├─ Route 2 ──→ [Actions] (if condition matches)
├─ Route 3 ──→ [Actions] (if condition matches)
└─ Default ──→ [Actions] (if no conditions match)
```

Each route evaluates independently. By default, all routes whose conditions are true will execute. This means if routes 1 and 2 both have conditions that evaluate to true, both will run.

Use the Router node in the following cases:

* You need to handle multiple different outcomes from a single trigger.
* Different [[entities/ticket|ticket]] states require different actions (such as "resolved" vs "open" vs "closed").
* You want cleaner, more maintainable [[features/workflows|workflows]] than nested conditionals.
* Multiple paths may need to execute simultaneously.

## Route definition

A route comprises the following attributes:

1. Name (required): A unique identifier for this route that becomes the output port name that downstream nodes connect to  
   Example: "urgent", "follow\_up\_needed", "escalate"
2. Description: Explains the purpose of this route and helps other users understand when this path executes.  
   Example: "Route high-severity [[features/tickets|tickets]] to the senior support team"
3. Condition (required): The logic that determines if this route executes. Multiple conditions can be combined with AND/OR logic.  
   The conditions are constructed from field values from previous steps (such as Ticket.severity, [[entities/issue|Issue]].status) and operators (such as Contains, Equals, Greater than, Less than).

   Example: Issue.title Contains "urgent" AND Issue.priority = "P0"

All fields and outputs from steps before the Router are accessible within every route. When you [[features/build|build]] conditions or add actions in any route, you can reference data from earlier workflow steps.

Example: If a trigger or previous step provides Ticket.severity, Ticket.priority, and Ticket.status, all routes can use these fields in their conditions and actions.

### Default Route

Every Router automatically has a Default route. This executes only if none of the other conditions are met. It acts as a fallback for edge cases or unclassified scenarios.

## Route execution

### Independent

By default, the Router evaluates all routes independently. When multiple routes have conditions that evaluate to true, all matching routes are executed.

```
Route 1: title = "bug"      ✓ TRUE  → Executes
Route 2: priority = "high"  ✓ TRUE  → Executes  
Route 3: status = "open"    ✗ FALSE → Does not execute
Default                             → Does not execute
```

Result: Routes 1 and 2 both execute

Take advantage of independent route execution when you need multiple unrelated actions to occur for the same change. For example, a ticket can be tagged as "urgent" AND sent to a specific team from the same event.

### Single route

Enable the **First Match Only** option in the Router configuration when you want only one route to execute, regardless of how many conditions match.

```
Route 1: title = "bug"      ✓ TRUE  → Executes (STOPS HERE)
Route 2: priority = "high"  ✓ TRUE  → Not evaluated
Route 3: status = "open"    ✗ FALSE → Not evaluated
Default                             → Not evaluated
```

Result: Only Route 1 executes. The Router stops evaluating after the first matching condition.

Enable single-route execution when only one outcome should occur per workflow execution, when routes represent mutually exclusive categories, or when you want to prevent duplicate or conflicting operations.

For example, a ticket should be categorized into exactly one queue—either "urgent" OR "standard" OR "backlog".

## Tips and best practices

✅ Do:

* Use descriptive route names that clearly indicate the path's purpose.
* Keep conditions simple and readable—break complex logic into multiple routes if needed.
* Add descriptions explaining when each route is used.
* Test with sample data to ensure conditions work as expected.
* Use "First Match Only" when routes are mutually exclusive.

❌ [[glossary/don|Don]]'t:

* Create overlapping conditions without considering parallel execution.
* Use overly complex nested condition logic, split into multiple routes instead.
* Forget to define the Default route, always have a fallback.
* Leave routes with empty names or descriptions.

## Router vs. nested if-else

```
If severity = P0
  → Send notification
  If priority = urgent
    → Escalate
    If status = open
      → Auto-assign
```

```
Router
├─ "p0_urgent_open" → Send notification, Escalate, Auto-assign
├─ "p0_urgent_closed" → Send notification, Escalate
├─ "p0_normal" → Send notification
└─ Default → Skip
```

## Source
- DevRev support [[entities/article|article]] [Router node](https://support.devrev.ai/en-US/devrev/article/rJS1COSx) (ART-23384)
