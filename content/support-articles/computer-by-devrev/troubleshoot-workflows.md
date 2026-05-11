---
title: Troubleshoot workflows
devrev_id: ART-33224
parent_directory: Workflow engine
translation_group: Jg_gNHsv
modified_date: "2026-05-05T20:56:42.988Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Jg_gNHsv"
tags: []
top_category: Computer by DevRev
wiki_match: features/conversational-workflows
match_score: 0.565
last_updated: 2026-05-11
---

# Troubleshoot workflows

Workflows in DevRev automate actions based on triggers and conditions. When a workflow doesn't behave as expected, the issues usually fall into one of a few predictable categories.

> 📝 **Note**: The **Runs** tab and most workflow management features are visible only to users with admin access. If you cannot see the Runs tab or certain settings, confirm your role with your workspace administrator.

## Workflow isn't triggering

* **Issue**: Trigger conditions are too restrictive.

  **Solution**: If you've set filters on the trigger (such as a specific part, tag, or severity), the event may not match. Review your trigger conditions and temporarily remove filters to confirm the workflow fires at all, then re-add conditions one at a time.
* **Issue**: The subtype filter on `issue_updated` doesn't restrict which updates fire the trigger.

  **Solution**: The subtype input on the `issue_updated` trigger surfaces custom fields for that subtype but does not restrict which updates fire the trigger. To limit execution to a specific subtype, add an **If/Else** node immediately after the trigger and check the subtype field there. Note that this behavior differs from `issue_created`, where the subtype input does act as a filter — only issues of the selected subtype trigger the workflow.
* **Issue**: A queue backlog is causing a delay.

  **Solution**: Under high load, workflow executions can queue. If your workflow eventually fires but with a delay, this is likely the cause. To distinguish a queued run from a workflow that never triggered, open the [Runs tab](https://app.devrev.ai/?setting=workflows) and look for the run's status. A queued run appears in the list with a pending status; if no run appears at all, the trigger itself did not fire.
* **Issue**: The workflow is not published.

  **Solution**: Draft workflows do not execute. Confirm the workflow status is **Published** in [Settings > Workflows](https://app.devrev.ai/?setting=workflows).

## Workflow runs but produces unexpected results

* **Issue**: The **If/Else** node routes to the wrong path.

  **Solution**: This is a known UI issue where both output paths can appear mapped to the same node, causing the wrong branch to execute. Delete the connections from the **If/Else** node and reconnect them carefully, ensuring the correct node is attached to each path.
* **Issue**: Conditions are case-sensitive and don't match expected values.

  **Solution**: Workflow conditions match text exactly, including capitalization. If a condition like `stage = "In Progress"` isn't matching, check for case differences. Use **Contains Any** with all expected variations as a workaround.
* **Issue**: A custom field used in the workflow doesn't exist in this workspace.

  **Solution**: Custom fields must be defined in your workspace before they can be used in a workflow. If a field is missing, the node fails silently or skips. Verify the field exists under [Settings > Object customization](https://app.devrev.ai/?setting=object-customization).
* **Issue**: A third-party node is missing after importing a workflow.

  **Solution**: If you imported a workflow from another workspace, any nodes provided by snap-ins (such as Slack nodes) are missing if the corresponding snap-in isn't installed. Install the required snap-in from [Settings > Snap-ins](https://app.devrev.ai/?setting=snap-ins), then re-open the workflow to restore the node.

## Node failing with an error

* **Issue**: Timeout (30 seconds per node).

  **Solution**: Each node has a 30-second execution limit. External API calls that take longer fail. Optimize the external call or split the workflow into smaller steps.
* **Issue**: Rate limit (HTTP 429).

  **Solution**: The workflow is making too many API calls in a short period. Add a delay node between calls, or reduce the frequency of the trigger.
* **Issue**: Permission error.

  **Solution**: The workflow may lack the necessary permissions to perform the action. Confirm that you have admin access — admin access is required both to view the Runs tab and to manage workflow service accounts. Verify that the workflow's service account has the required role for the action it performs.

To prevent errors from stopping the entire workflow, add an **error path** to any action node by clicking the three-dot menu on the node and selecting **Set Error Path**. This lets the workflow continue even if that step fails.

### Investigate a failure with the Runs tab

1. Go to [Settings > Workflows](https://app.devrev.ai/?setting=workflows) and open the workflow.
2. Click the **Runs** tab in the top-left corner of the canvas to see a list of recent executions.
3. Click a failed run to see which node errored, along with its input values, output values, and error message. Click the **star icon** on the failed node for an AI-generated explanation of the error.

> 📝 **Note**: The Runs tab is visible only to admins. If you do not have admin access, use the fallback method below.

### Debug without the Runs tab

If you cannot access the Runs tab (for example, because you lack admin access), insert an **add\_comment** node at various points in your workflow. Configure each node to post a distinctive comment on the relevant object (such as the triggering issue). This functions like a `console.log` statement — when you trigger the workflow, the comments indicate which nodes executed and in what order, helping you isolate the failing step.

## Slack node isn't appearing or isn't working

* **Issue**: Slack-related nodes don't appear in the workflow builder.

  **Solution**: Slack nodes only appear if the **Slack snap-in** is installed in your workspace. Install it from [Settings > Snap-ins](https://app.devrev.ai/?setting=snap-ins).
* **Issue**: A Slack connection isn't appearing in the node's dropdown.

  **Solution**: Slack nodes in workflows only accept **public** Slack connections. Open the connection settings and set its visibility to **Public**.

## Known limitations

The following are platform constraints to be aware of when designing workflows.

* **Maximum execution time** is 5 minutes per workflow run.
* **Maximum size** of a workflow is 100 nodes and 8 MB as represented in JSON.
* **Minimum timer interval** for scheduled (cron) triggers is 10 minutes. This minimum may vary by workspace if a feature flag override is in place.
* **Field values cannot be cleared.** Workflows can only set or modify field values, not empty them.
* **No arithmetic operations** are supported natively. Use the **Execute Code** node for calculations.
* **Multiple triggers** cannot share the same execution path in a single workflow. If you need the same logic to run from two different triggers, duplicate the workflow.
* **Looping nodes (`for_each`)** are not generally available. If you see `for_each` in your workspace, it has been enabled for your workspace specifically. A general-purpose looping construct is not available.
* **The `go_back` node** can only return to an `ask_options` node. It cannot target other node types.
* **The `update_ticket` node Tags fields** display both "Tags to Add" and "Tags to Remove" as mandatory in the UI, but only one is required.
* **Control nodes require explicit saving.** Unlike action nodes, which auto-save, control nodes (such as If/Else and Switch) must be saved manually. Unsaved changes to control nodes are lost when you navigate away.
* **The "insert variable" menu** sometimes fails to display configuration options on the first click. Refresh the page and try again.
* **Several nodes are behind feature flags** and may not appear in every workspace. These include `for_each`, `oasis_sql_execute`, `talk_to_agent`, and `ask_agent`. If an expected node is missing and the relevant snap-in is installed, the node may require a feature flag. Contact DevRev support for enablement.
* **Scheduled events cannot be unscheduled via workflows.** Once a scheduled event is created, it cannot be canceled or modified through a workflow action.

## Source
- DevRev support article [Troubleshoot workflows](https://support.devrev.ai/en-US/devrev/article/Jg_gNHsv) (ART-33224)
