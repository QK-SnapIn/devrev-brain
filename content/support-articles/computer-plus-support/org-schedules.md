---
title: Org Schedules
devrev_id: ART-25289
parent_directory: Computer+ Support
translation_group: N2JScs7f
modified_date: "2026-03-09T07:17:33.131Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/N2JScs7f"
tags: []
top_category: Computer+ Support
wiki_match: features/issues
match_score: 0.421
last_updated: 2026-05-11
---

# Org Schedules

Organization Schedules establish the operating hours and availability rules applied across your organization. They serve as the foundation for determining when your organization is open, reachable for support, and functioning within defined service boundaries.

These schedules have a direct effect on how tickets are processed, how SLAs are tracked, how automations behave, and how customers are informed about availability.

## Organization Schedules Controls

**Business hours**

Business hours define your organization's official hours of operation, for example, Monday through Friday from 9:00 AM to 6:00 PM, with weekends excluded. This configuration governs whether an incoming ticket falls within or outside of active business hours.

**SLA calculations**

Organization Schedules determine how SLA timers are measured and applied. Specifically, they control when response time tracking begins, when timers are paused due to off-hours periods, and when a ticket is flagged as overdue.

For example, if a ticket arrives at 7:00 PM and business hours close at 6:00 PM, the SLA timer will not begin until the following business day at 9:00 AM. This approach ensures that SLA measurements accurately reflect active working time rather than elapsed calendar time.

**Holiday rules**

Organizations can define exceptions to their standard schedule to account for public holidays, company wide closures, or periods of reduced operation. These holiday rules take precedence over the default schedule and automatically adjust SLA calculations and availability indicators accordingly.

**Routing and automation**

Organization Schedules can also drive automated workflows that respond to off-hours activity. This includes sending after hours reply messages, triggering escalation procedures, routing requests to on-call teams etc.. Together, these rules help ensure that any requests received outside of business hours are managed in a consistent and appropriate manner.

## Create a Org Schedule

1. Go to **Settings** > **Support**> **Org Schedule** > **+New Organization Schedule**

![Screenshot 2026-02-25 at 9.24.19 AM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11804485&key=36d3211f59b530dc366ea23da68ae6f92eb569842834dfbebf0b711787816b5b)

2. Choose the org schedule name, timezone, validity, business hours & holidays.

![Screenshot 2026-02-25 at 9.26.27 AM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11804486&key=29d96bb332502ca2180d135deff7ec9e1c8b7e2f52ccaba1cda0c132916934d3)3. Choose to save the schedule as draft or publish

![Screenshot 2026-02-25 at 9.28.49 AM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11804487&key=992ffa133512302eef83714baa255539ebc7962eba0ddd75253fe046a9978078)

## Edit an Org Schedule

Administrators can update an organisation schedule at any time, either before or after its expiry date.

### Expiry Notifications

To ensure continuity, automated notifications are sent to administrators at the following intervals prior to schedule expiry:

* 1 month before expiry
* 2 weeks before expiry
* 1 week before expiry
* 1 day before expiry

These reminders help administrators take timely action to extend or modify the schedule as needed.

### Impact on Linked SLAs

All SLAs mapped to the organisation schedule will continue to function as expected after updates are made. No additional configuration changes are required for linked SLAs.

### Edit an Org Schedule

1. Open the Edit Modal. Go to the **Organization Schedule** and click **Edit**.

![Screenshot 2026-02-24 at 3.35.52 PM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11804513&key=6c72a1ad94ff7b73e762bd96a49cb8c0d4892ea4e332980b568eb1070d820c99)2. Update Schedule Configuration

In the **Edit Organization Schedule** modal:

* Modify the validity period (start and end dates)
* Update operating days and timings
* Make any other required configuration changes  
  ![Screenshot 2026-02-24 at 3.36.11 PM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11804524&key=09e5413f49b1865cea1935b5e1dcdfdbd326c5c52750e952996e1979da3237e6)

Once updates are complete, save the changes to apply them.

### Note:

1. Publishing creates a new version of the organization schedule. Existing items will continue using the previous version of the schedule, while the new version will apply to items created after publishing.
2. For SLAs, when a ticket’s policy is updated, the latest version of the organization schedule associated with that policy will be applied.

## Source
- DevRev support article [Org Schedules](https://support.devrev.ai/en-US/devrev/article/N2JScs7f) (ART-25289)
