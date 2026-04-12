---
title: Incident
type: entity
status: draft
sources: []
related: [[entities/ticket]], [[features/incidents]]
last_updated: 2026-04-12
---

# Incident

## What it is
A first-class object in DevRev for managing service disruptions and outages ([[glossary/incident]]). Incidents have their own lifecycle separate from tickets and issues.

## Key attributes
- [gap] What are the stock fields on an incident object?
- Severity levels: [gap] How many levels? What are the labels?
- Stages: [gap] What stages does an incident move through?
- [gap] What is the DON prefix for incidents?

## Stages
[gap] Full stage list and transitions.

## Severity levels
[gap] Severity enum and SLA implications per level.

## On-call scheduling
[gap] How are on-call schedules configured? Rotation rules? Escalation policies?

## Broadcast / alerts
[gap] How are stakeholders notified? Broadcast channels? Alert templates?

## Analytics
[gap] What incident-specific dashboards or metrics exist? MTTR? Incident frequency?

## Relationships
- Linked to [[entities/ticket]] — [gap] How? One-to-many? Automatic or manual linking?
- [gap] Can incidents be linked to issues?
- [gap] Can incidents be linked to parts?

## Creation
[gap] How are incidents created? UI entry points? API? Automation triggers?

## Open questions
- [gap] Is there an incident commander role?
- [gap] Are post-mortems a built-in feature or handled externally?
- [gap] How does incident status appear in the left nav or Inbox?
