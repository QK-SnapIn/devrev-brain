---
title: Incident Management
type: feature
status: draft
sources: []
related: ["entities/incident", "entities/ticket", "features/slas"]
last_updated: 2026-04-12
---

# Incident Management

## What it does
Provides tools for creating, tracking, and resolving service incidents ([[glossary/incident]]). Includes on-call scheduling, broadcast/alerting, and incident-specific analytics.

## Why it exists
Enables teams to respond to service disruptions in a structured way, coordinate responders, and communicate status to stakeholders.

## Key behaviors

### Incident creation and lifecycle
- [gap] How are incidents created? Manual, API, automation trigger?
- [gap] What stages does an incident go through?
- [gap] Severity levels and their definitions
- [gap] Can incidents be linked to existing tickets automatically?

### On-call scheduling
- [gap] How are on-call rotations configured?
- [gap] Escalation policies — time-based? Severity-based?
- [gap] Integration with external paging tools (PagerDuty, Opsgenie)?

### Broadcast / alert features
- [gap] How are stakeholders notified of incidents?
- [gap] Broadcast channels (email, Slack, PLuG widget?)
- [gap] Status page integration?

### Incident analytics
- [gap] What dashboards exist for incidents?
- [gap] MTTR, MTTA, incident frequency metrics?
- [gap] Post-incident review / post-mortem support?

## Entry points
- [gap] Left nav location
- [gap] Quick Create support?
- [gap] URL route pattern

## Related flows
- [[flows/critical-product-flows]] (incident management listed as critical flow)

## Related scenarios
(none yet)

## Open questions
- [gap] Is this available in all org tiers or specific bundles?
- [gap] How do incidents relate to SLAs?
- [gap] Workflow triggers available for incident state changes?
