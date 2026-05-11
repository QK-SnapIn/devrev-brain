---
title: OLA (Operational-Level Agreement)
type: feature
status: draft
sources: [https://support.devrev.ai/en-US/devrev/directories]
related: ["features/slas"]
last_updated: 2026-05-11
support_articles: [ART-21868]
---

# OLA (Operational-Level Agreement)

## What it does
Tracks internal team commitments ([[glossary/ola]]) and response/resolution targets, distinct from customer-facing SLAs.

## Why it exists
While SLAs define commitments to customers, OLAs define commitments between internal teams (e.g., engineering must respond to escalations within X hours). This ensures internal handoffs meet agreed timelines.

## Key behaviors
- Internal contract defining service level targets between teams (customer-agnostic, unlike SLAs).
- Applies to issues (not tickets).
- Built-in metric: "Issue Resolution Time".
- Timer controls: timers can be started, paused, or stopped based on issue stages.
- Breach notifications are delivered via the **OLA Breach Notifier** snap-in.

## Relationship to SLA
- OLAs are internal (team-to-team); SLAs are external (org-to-customer).
- OLAs apply to issues; SLAs apply to tickets.
- [gap] Can an OLA and SLA both apply to the same work item indirectly (e.g., linked ticket + issue)?
- [gap] Do OLA breaches affect SLA metrics?

## Entry points
- Settings → Support → OLAs
- Docs: https://docs.devrev.ai/product/ola
- [gap] How is OLA status visible on individual issues?

## Related flows
(none yet)

## Related scenarios
(none yet)

## Open questions
- [gap] Is OLA available in all org tiers?
- [gap] Can OLA policies be assigned to specific groups or teams?
- [gap] Workflow triggers for OLA breach events?
- [gap] Are there additional built-in metrics beyond "Issue Resolution Time"?

## Support documentation

Referenced DevRev support articles synchronized from [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories):

- [[support-articles/computer-plus-support/operational-level-agreements|Operational-level agreements]] (ART-21868) — [external](https://support.devrev.ai/en-US/devrev/article/ztv-zLpw)
