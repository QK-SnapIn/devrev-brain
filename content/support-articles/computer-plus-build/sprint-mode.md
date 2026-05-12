---
title: Sprint mode
devrev_id: ART-21872
parent_directory: Computer+ Build
translation_group: nPb7lTWZ
modified_date: "2025-12-10T06:56:34.01Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/nPb7lTWZ"
tags: []
top_category: Computer+ Build
wiki_match: support-app
match_score: 0.455
last_updated: 2026-05-11
summary: "Sprints involve the following for engineering work management:"
---

# Sprint mode

## Sprint activities

Sprints involve the following for engineering work management:

1. Creation
2. Planning
3. Retrospection
4. Backlog grooming

For a guided tour of sprints, check out the interactive [walkthrough](https://walkthrough.devrev.ai/app/sprint).

### Creation

To enable teams to deliver great products, attaching work items to [[features/parts|parts]] is no longer a requirement. You can define sprint boards the way you want because every organization has its team structure and way of distributing work among these teams. Creating sprint boards to start building is as easy as creating [[features/issues|issues]]. Refer to Create a sprint for detailed instructions.

Once the sprint board is created, you can find it under **Sprint Boards** in the left navigation bar of the DevRev app.

The issues visible in the sprint board's backlog are the ones that meet specific filters. These identified issues undergo grooming and are scheduled for upcoming active sprints.

### Planning

Planning a sprint starts with the **Backlog** tab on a sprint board, which shows issues logged but not assigned to any sprint. The sprint planning exercise involves the team members coming together to discuss the issues shown here and to decide which ones should be taken up as [[entities/part|part]] of the current sprint.

You can view the current sprint, the next sprint, and the backlog on the sprint board at any time.

As you plan on the issues, you may move them into a sprint by selecting the relevant ones, selecting the **Add to sprint** icon on top, and choosing the sprint number from the menu.

During sprint planning, it's also good practice to look at the [[entities/issue|issue]] coverage done in previous sprints. To access previous sprints select the **Previous** switch at the top of the sprint board.

![Previous sprints](don:core:dvrv-us-1:devo/0:artifact/4100187)

Team members can look into the issues and change stages as they progress on the planning and work done on the issue.

You can export views to CSV or JSON by selecting **Actions** in the upper-right corner and choosing the format.

### Retrospection

After completing a sprint, visit the sprint from the **Previous** tab and review the items which are *Completed* or still *In progress* by using the **Stage** filter on top. Alternatively, you can use a block-wise view by applying **[[entities/group|Group]]** on the **Stage** attribute. Toggle the switch in the **Group By** multi-select pane to view a metric summarization.

![Previous sprint by stage](don:core:dvrv-us-1:devo/0:artifact/4100191)

You may move incomplete items either into the next sprint or the backlog by multi-selecting the issues and using the **Add to sprint** icon from the tray on top.

### Backlog grooming

PMs, engineers, and designers should visit the backlog regularly to plan, brainstorm, and prepare the work item and its dependencies to have it ready for a future sprint. Activity here is mostly done at the level of individual items and their dependents.

## Create a sprint

1. You can create a sprint in either of the following ways:- ![sprint board in left nav](don:core:dvrv-us-1:devo/0:artifact/4100195)Go to **Work** > **Sprint Boards** on the left nav to view and create the sprint boards by clicking **+ Sprint board**.
     
   - Create sprint boards using Parts/[[glossary/trails|Trails]]:- Go to **[Product](https://app.devrev.ai/?vista=vista-def-my-parts)**[ > ](https://app.devrev.ai/?vista=vista-def-my-parts)**[Parts](https://app.devrev.ai/?vista=vista-def-my-parts)**[ > ](https://app.devrev.ai/?vista=vista-def-my-parts)**[Capability/Feature](https://app.devrev.ai/?vista=vista-def-my-parts)**. Select the part you want to create a sprint for.
     - Go to **Product** > **Trails** > **Capability/Feature**. Hover over the part you want to create a sprint and click **View**.
     - Go to **Related** > **Sprint boards**. If there are no sprint boards for the part, click **New sprint board** and specify the name, duration of sprints, and the start date. The start time allows you to select the date and time when the sprint begins. The sprint will conclude at the same time after the specified number of days, including weekends.![New sprint board](don:core:dvrv-us-1:devo/0:artifact/4100199)
2. Go to the new sprint board and click **Backlog**. Any issues assigned to the part but not to a sprint are listed here.
   If there are no issues shown, you can go to the sprint board and click **+Issue**.
   Create a new issue, assign it to the part, sprint and add the owner.Sprints are not coordinated with stages.
3. Select issues that you would like to assign to **Sprint 1** or **Sprint 2** then click **Move** in the toolbar at the top of the screen and select the sprint.![Add issues to sprint](don:core:dvrv-us-1:devo/0:artifact/4100203)
4. Go to **Sprint 1** or **Sprint 2** to see that issues are displayed.![View sprint](don:core:dvrv-us-1:devo/0:artifact/4100209)The sprint is also displayed in (and can be changed from) the issue.![View sprint in issue](don:core:dvrv-us-1:devo/0:artifact/4100212)

Parts are not linked to the sprint board. A sprint board will show up on a part if issues of that part are assigned to an active sprint.

You can [[features/search|search]] for sprint boards directly by adding the **Sprint** filter inside **Issues**. Go to **Sprint** > **Add** on top and search for the sprint by name. Use this to navigate to a sprint board that has not been shared with you explicitly.

![Search sprints in issues](don:core:dvrv-us-1:devo/0:artifact/4100217)

### Share and customize sprint boards

- As with other [[features/vistas|vistas]], everyone in the workspace can view the sprint board in **Sprint Boards** even if it's not exclusively shared with you. You can pin the sprint board for easy access and share the URL too which is under **Share** > **Copy Link**. To grant write permission, click **Share** and enter the email or name of the person.

![Share sprint board](don:core:dvrv-us-1:devo/0:artifact/4100221)

- You can go to **Settings** on the left of the **Insights** button on top to change **Duration** of the sprint and **Define backlog** by adding issue filters like **Part, Owner, Tags, Priority, Created by, SubType** that were used while creating the sprint board by clicking **+ Attributes**. This is especially useful for scenarios where the new team member’s work has to be tracked in the backlog or a new product part is added to the team’s focus area of work whose issues are to be tracked, etc.

![settings](don:core:dvrv-us-1:devo/0:artifact/4100229)

## Create child/parent/dependent issues

1. Select the issue for which you want to create a child/parent/dependent issue.
2. Click **+Link issues** and select the required issue state.
3. You can now search for an existing issue to add or create a new issue by clicking **+New Issue**.
4. Add title, description, and owner. Click **Create**.

## Sprint insights

Sprint insights help you understand and visualize more about your issues and provide you with data. To view your sprint insights, select the required sprint and click **Insights**.

- **Burn-down chart**: To help visualize sprint progress by viewing scope change over time and changes in work remaining over time. A line represents total incomplete issues over time as well as a specific line to represent how much work is left on issues directly linked to customer asks.
- **Filters for focused analysis and retrospection**: Ability to apply filters at the top of the page for **Part**, **Owner**, and **Priority**. This enhanced feature provides you with greater control and flexibility when analyzing the performance of various team members, different parts, and different priority work within your sprints.
- **High-level breakdown by origin and nature of work**: Data-driven insights to help answer how much development work is focused on new features vs. maintenance and how much of it is customer-initiated vs. internally initiated. This enables you to gain deeper insights into the origin and nature of the issues within your sprints.
- **Issue distribution**: Insights to understand the distribution of work across stages, owners, priority, and Part of your product
- **Sprint Health**: Provides a snapshot of the sprint health by capturing key metrics like % of work, time remaining in the sprint, and overall scope change since the start of the sprint
- **Time spent per stage**: One can view and analyze the average time spent on issues in each stage since the beginning of the sprint. This helps developers to reflect on which stages of their work are taking up most of their time.

## Source
- DevRev support [[entities/article|article]] [Sprint mode](https://support.devrev.ai/en-US/devrev/article/nPb7lTWZ) (ART-21872)
