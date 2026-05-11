---
title: Issues
devrev_id: ART-21870
parent_directory: Computer+ Build
translation_group: o81mkSOB
modified_date: "2026-01-05T16:12:59.798Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/o81mkSOB"
tags: []
top_category: Computer+ Build
wiki_match: features/issues
match_score: 1.0
last_updated: 2026-05-11
related: ['features/issues']
---

# Issues

Views of issues can be found under **Build** in the DevRev app and in sprint boards.

You can export views to CSV (max 5,000 entries) or JSON by selecting **Actions** in the upper-right corner and choosing the format.

## Attributes

Issues have attributes that can be used to filter and group issues in various views. Certain fields will be highlighted as mandatory during creation. For example, **Priority** is a required field.
You can find all the stock attributes listed under [**Settings** > **Object customization** > **Issue**](https://app.devrev.ai/?setting=object-customization?type=issue), go to **Stock fields**.
These are the stock attributes that come with DevRev:

* **Owner**: The person responsible for the issue. Issues are assigned to an engineer, PM, designer, or any other team member through the **Owner** attribute.
* **Priority**: The importance of the issue. Priorities can be set to P0, P1, P2, and P3. P0 is the highest priority and P3 is the lowest.
* **Stage**: The current state of the issue. The stage attribute is used to track the progress of the issue through its lifecycle. For more information on stages, see stages.
* **Part**: The part of the company or product that the issue is related to. For more information on parts, see [[support-articles/computer-by-devrev/parts-trails|parts]].
* **Created by**: The person who created the issue.
* **Created date**: The date the issue was created.
* **Modified date**: The date the issue was last modified.
* **Tags**: Tags are used to categorize issues.
* **Target close date**: The date by which the issue is expected to be resolved.
* **Modified by**: The person who last modified the issue.
* **Reported by**: The person who reported the issue.
* **Close date**: The date the issue was closed.

These attributes can be effectively used in filters and **Group** conditions across various vistas in DevRev to track specific work, capacity, and more.

You can add custom attributes to issues to track additional information. For more information on custom attributes, see [[support-articles/computer-by-devrev/object-customization|object customization]].

Issues are attached to parts in order to align efforts with product priorities.

As to the size of an issue and the flexibility it offers to manage changes in size, issues offer hierarchy in the form of parent-child relationships and granularity.

From an issue, you can create a parent issue or a child issue. In an issue, select **Link Issues** in the **Issues** pane and select the type to add.

![Link issue](don:core:dvrv-us-1:devo/0:artifact/4100143)

While a parent issue can and usually does have multiple children, an issue can have only one parent. If you try to add a parent to an issue that already has one, it fails.

[[support-articles/computer-by-devrev/tasks|Tasks]] can be used to break an issue down into smaller pieces. Issues may involve a checklist of items to be handled that can be represented as tasks.

## Discussion and events

The **Discussion** tab of issues is to facilitate communication and collaboration on a given work item across engineers, PMs, designers, and any other stakeholder within an organization.

![discussions](don:core:dvrv-us-1:devo/0:artifact/4100147)

The **Events** tab provides a log of key events such as owner assignments/changes, stage changes, and dependency updates.

## Create an issue

1. Go to [**Work > Issues**](https://app.devrev.ai/?vista=vista-def-issues) from the sidebar on the left.
2. Click \*\* + Issue\*\* on the top right corner of your screen.
3. Add a title and description for your new issue. You can also attach files related to the issue in the description.
4. Select which part of the company/product this issue is related to.

   ![New issue panel](don:core:dvrv-us-1:devo/0:artifact/4100151)
5. Enter other attributes for the issue: change the assignee or accept the default; enter the severity; add any relevant tags to help employees identify any relevant traits of the issue; select the workspace that the issue pertains to.
6. If there are other [[support-articles/computer-plus-support/tickets|tickets]] or issues that relate to this issue, click **Link Records** and select the relevant items.
7. If you would like to immediately create another issue, select **Create multiple**.
8. Click **Create**.

## Tags

* Stalled
* Priority/Escalated
* Fast/Slow Moving
* Blocked
* Resolution: [*values*]
* Impact: [*values*]
* Reason: [*values*]

An *autonomous issue* is an issue created automatically from an external event, such as a new VCS branch or pull request. These issues have the tag `autonomous`.

## Stages

This diagram represents the **Issue Transitions** workflow in DevRev, organized into three main groups:

* **📂 Open**: Initial stages for new and pending issues (Triage, Backlog, Prioritized)
* **⚡ In Progress**: Active development stages (In Development, In Review, In Testing, In Deployment)
* **🔒 Closed**: Final states for resolved issues (Completed, Won't Fix, Duplicate)

Issues can transition flexibly between most states, and closed issues can be reopened by returning to Triage.

![Issue Transitions Diagram](don:core:dvrv-us-1:devo/0:artifact/4100154)

**Open**

* *Triage*

  Issues that are newly created. From here either a user or automation takes a look at the issue and makes a determination of where it should go. In certain cases it may be immediately closed as a *duplicate* if the reported concern already exists in another issue. In other cases, the owner may determine that the issue is invalid or can't be fixed for other reasons and close the issue as *won't fix*.

  If the issue isn't duplicate and is something that should be accepted, the owner determines how soon it should be addressed by moving into the *backlog* or *prioritized* stage.
* *Backlog* (later)

  Issues that have been accepted but aren't planned for the next few development cycles (next and now). Issues in the *backlog* stage may be groomed at regular intervals to move to *Prioritized* or *In Development* depending on the current priority and bandwidth.
* *Prioritized*

  Issues that are planned to be completed in the current or subsequent development cycle but which have not yet been started. Issues in the *prioritized* stage should have clear requirements. Issues in the *Prioritized* stage may be taken up for execution (promoted to *In development*) or deprioritized (demoted to *Backlog*).

**In-progress**

* *In development*

  The issue owner is actively working on the issue. When the owner has their resolution in a good state they request review which puts the issue in the *In review* stage.
* *In review*

  The issue and resolution are currently being reviewed. In certain scenarios, the reviewer may request changes to the proposed solution. In this scenario, the stage would transition back to *In development*. If the reviewers approve the fixes, the issue progresses into the *In testing* stage for validation.
* *In testing*

  The fixes have been approved and are currently undergoing validation. If the tests fail or bugs are made apparent, the issue transitions back to the *In development* stage as changes are required. If the tests pass and the fix is acceptable, the issue starts the deployment (CD) lifecycle and transitions into the *In deployment* stage.
* *In Deployment*

  The fixes are currently being deployed. When the deployment is complete, the issue transitions to the *Resolved* stage. Traditional CD processes may move changes through various environments. These transitions should be tracked with stage notes.

**Closed**

* *Won't Fix*

  It can't be addressed with a change to the product.
* *Duplicate*

  Redundant with some other issue.
* *Completed*

  Deployment is complete.

## Subtypes

You can create subtypes of issues to categorize them further. For example, you can create subtypes for bugs, features, and tasks. Subtypes can be used to filter issues in various views.
A subtype inherits all the attributes of its parent issue type. You can add custom attributes to a subtype.
To know how to create subtypes and add custom attributes to them, see [[support-articles/computer-by-devrev/object-customization|object customization]].

## Related wiki nodes
- [[features/issues]]

## Source
- DevRev support article [Issues](https://support.devrev.ai/en-US/devrev/article/o81mkSOB) (ART-21870)
