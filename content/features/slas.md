---
title: SLAs (Service Level Agreements)
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_slas.jsonl, raw/docs/devrev-developer-docs.md, raw/docs/devrev-docs-scraped.md, raw/docs/devrev-agent-dump-settings.md]
related: [[entities/ticket]], [[features/analytics]]
last_updated: 2026-04-12
---

# SLAs (Service Level Agreements)

## What it does
The SLAs feature manages metric definitions and metric workflows that define and enforce service level agreements within DevRev. Metric definitions describe what to measure (e.g., time-based metrics on tickets), while metric workflows define the automated actions triggered when SLA conditions are met or breached. With 95 test cases, this feature covers CRUD operations and partial update semantics. The backend service is `us_slay`.

## Why it exists
Customer support teams need to track response and resolution times against committed SLAs. This feature provides the configuration layer for defining metrics, setting thresholds, and triggering automated workflows when SLAs are at risk or breached, ensuring teams can meet their service commitments.

## Key behaviors
- **Metric definitions**: Create, update, get, list, delete; types include `time`-based metrics
- **Applies-to targeting**: Metric definitions target specific object types (e.g., `ticket`)
- **Status management**: Metric definitions can be `active` or `inactive`; status transitions supported
- **Partial updates**: Sending only `id` and one field updates just that field without resetting others
- **Metric workflows**: Create, get, list, update, delete workflows
- **Workflow schema**: Required fields include id, display_id, created_date, modified_date, status, applies_to, subtype, resume_on_restart, metric_actions
- **Status as enum-value**: Status returned as object with id, label, ordinal fields

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespaces: `metric-definitions.*`, `metric-workflows.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `metric-definitions.create` | POST | Create metric definition |
| `metric-definitions.get` | GET | Get metric definition |
| `metric-definitions.list` | GET | List metric definitions |
| `metric-definitions.update` | POST | Update metric definition |
| `metric-workflows.list` | POST | List metric workflows |
| `metric-workflows.delete` | POST | Delete metric workflow |

## Core Metrics
SLAs track three primary metrics:
- **First response** -- time from ticket creation to first agent response
- **Next response** -- time between subsequent agent responses
- **Full resolution** -- time from ticket creation to ticket resolution

Each metric has breach and warning targets, calculable in **calendar hours** or **business hours**.

## Stage-Based Start/Stop
SLA timers start/stop based on ticket stage transitions. Configure under Settings > SLA.

## Creation Process (Step-by-Step)

**Navigation:** Settings > SLA

1. Go to **Settings > SLA** and click **+ Create**.
2. Provide a **name** and **description**.
3. Add policies to the SLA by clicking **+ Policy**.
4. Select **Ticket Policy** or **Conversation Policy**.
5. Under **Conditions**, select values for **Tag**, **Part**, and **Severity**.
6. Under **Metrics**, enable/disable:
   - **First response time** -- starts at ticket/conversation creation; ends when agent replies.
   - **Next response time** -- starts after customer replies post-agent response.
   - **Resolution time** -- starts at creation; ends when ticket moves to Closed state.
7. Each metric has a **breach target** and a **warning target**.
8. Choose **calendar hours** or **business hours** for calculation.
9. Click **Publish**.

Multiple policies can be added within each SLA. The system applies the policy with the highest priority when tickets match multiple conditions.

## Business Hours (Org Schedules)

**Navigation:** Settings > Support > Business Hours (or via API `org-schedules.create`)

- Define **timezone** (IANA format, e.g. `America/New_York`).
- Set **weekly schedules** (working days and hours).
- Define **holiday rules** -- exceptions for public holidays or company closures; take precedence over default schedule.
- SLA timers pause outside business hours and resume at the start of the next business period.

## Publishing and Assignment
SLAs must be published before customer assignment. Published SLAs **cannot be edited** after publishing. Assignment occurs through:
- **Assignment rules** -- Go to Assignment rules > + Create Rule; select account attributes and values.
- **Exceptions** -- Add specific customers who always adhere to an SLA regardless of assignment rules.
- **Default SLA** -- Automatically assigned to all accounts without an existing SLA.

## Breach Notifications
[gap] No explicit breach notification configuration found in current sources beyond SLA metric stages (Active, Close to breach, Breached, Paused, Completed). The "close to breach" stage implies a warning mechanism, but notification channel/recipient configuration details are not yet documented.

## Metric Stages
Active SLA metrics operate in these states:
- **Active** -- timer running
- **Close to breach** -- warning threshold reached
- **Breached** -- target exceeded
- **Paused** -- timer suspended (e.g., awaiting customer response)
- **Completed** -- metric fulfilled

## Troubleshooting
If no SLA runs on tickets, verify:
1. The **SLA Name** attribute is populated on the ticket
2. The ticket satisfies policy conditions (based on severity, tags, parts)

## Dashboards
- Ticket-SLA Analytics (`/docs/dashboards/ticket-sla-analytics`)
- Conversation-SLA Analytics (`/docs/dashboards/conversation-sla-analytics`)

See [[features/analytics]] for the full dashboard list.

## Related metrics
- [[glossary/csat]] — Customer satisfaction scores, a complementary customer-facing metric often tracked alongside SLA performance.
- [[glossary/ola]] — Operational-Level Agreements, the internal counterpart to SLAs. While SLAs are customer-facing commitments on tickets, OLAs define internal team commitments on issues.

## Related flows
- SLA configuration and activation flow (see "Creation Process" and "Publishing and Assignment" above)
- [gap] SLA breach escalation flow

## Related scenarios
- [gap] Scenarios to be created from 95 test cases

## Open questions
- [gap] How does `resume_on_restart` affect workflow behavior?
- [gap] What is the relationship between metric definitions, workflows, and trackers?
