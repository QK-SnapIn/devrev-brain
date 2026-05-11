---
title: Vistas
devrev_id: ART-21835
parent_directory: Vistas
translation_group: SZYVVBEk
modified_date: "2026-05-07T02:47:56.532Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/SZYVVBEk"
tags: []
top_category: Computer by DevRev
wiki_match: features/vistas
match_score: 1.0
last_updated: 2026-05-11
related: ['features/vistas']
summary: "Vistas are saved, configurable views of your work objects, issues, tickets, accounts, parts, and more."
---

# Vistas

[[features/vistas|Vistas]] are saved, configurable views of your work objects, [[features/issues|issues]], [[features/tickets|tickets]], [[features/accounts|accounts]], [[features/parts|parts]], and more. You can filter, sort, [[entities/group|group]], and arrange columns to focus on exactly what you need, then save and share those configurations with your team.

> 📝 **Note**: By default, all users can create views. Admins can restrict view-creation permissions from workspace settings.

## Best practices

* **Define your goal before creating a view.** A focused view is more useful than a broad one. For example, create a view named "Open P0 issues assigned to me" with filters set to **Priority: P0**, **Owner: @me**, and **Stage: Open**. Know what question you are trying to answer before adding filters.
* **Keep views focused.** A view with many filters is harder to maintain. If you need to answer multiple questions, create separate views. For instance, separate "Q2 Customer Escalations" from "Unassigned Triage Items" rather than combining both into one overloaded view.
* **Share views to align your team.** When multiple people work from the same view, they share the same context. Use shared views for standups (e.g., "Sprint 12 Active Work" grouped by Owner), triage sessions, and sprint reviews.
* **Use descriptive names.** Names like "Q2 Customer Escalations P1 & P2" are easier to navigate than "My Filtered View 3". Add a description when you save so others understand the view's purpose, for example: "All P1/P2 tickets from enterprise accounts opened after April 1."
* **Revisit and update views regularly.** As your team's [[features/workflows|workflows]] evolve, review saved views periodically and adjust filters, columns, and grouping to reflect current needs. Remove views that no longer serve a purpose to keep the left nav uncluttered.

## Find views

* **Left navigation**: **Issues**, **Tickets**, **[[features/inbox|Inbox]]**, and **Parts** are pinned by default; views you create or that others share can pin under a section too. For pinning, unpinning, and organization, see [Left Navigation](https://support.devrev.ai/devrev/article/ART-233).
* **Recents**: The left nav lists up to five most recently opened unpinned views so you can reopen them without pinning.
* **Explore**: Open [**Explore**](https://app.devrev.ai/explore) to browse all views. It [[entities/group|groups]] **Stock Views** (defaults such as Issues, Tickets, Sprint Boards), **My Views** (yours), and **Shared** (from teammates). Filter the list by type, including Sprint Boards, to find a view quickly.

### View controls

Every view has a standardized toolbar in the top right. The controls appear in the following order, left to right:

* **[[features/search|Search]]**: Opens inline search within the current view.
* **Sort**: Opens sort options to order results by any attribute.
* **Filter**: Toggles the filter bar on or off.
* **View options**: Configures visible columns, view type, and group by.
* **⚡[[glossary/vista|Vista]] Reports**: Opens the reporting interface for the current view, allowing you to generate charts and summaries from the displayed data.
* **Actions (⋮)**: Share, export, and reporting.
* **Save**: Saves unsaved changes; only visible when changes are pending.

## Create a view

* **Create from the left nav**: Click **+** next to any section, pick an object type (**[[entities/issue|Issue]]**, **[[entities/ticket|Ticket]]**, **[[entities/account|Account]]**, **[[entities/part|Part]]**, etc.), and optionally choose a section to pin to. When you open the view, it is added under that section.
* **Save from within an existing view**: Change filters, sort, columns, or grouping. If the view already has a name and you own it or are an **Editor**, **Save** in the toolbar overwrites it. Otherwise use **Save as** (name, optional description, section). If you pick a section, the view appears there; otherwise find it under **Explore** > **My Views**.

> 📝 **Note**: **Save** and **Save as** are distinct actions. **Save** updates the current named view in place, while **Save as** always creates a new view. If you only see **Save as**, the view has not been saved before or you do not have editor access to it.

## Filters

Filters narrow your view to show only the records that match conditions you define. Views display up to 50 records per page.

* **Show or hide the filter bar**: Click **Filter** (funnel) in the toolbar to toggle the bar; when on, active chips show (for example **Created date: Last 90 days**, **Stage**).

![filters GIF.gif](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/13198704&key=b028a06328f30c775ea72b4571b37b7064583b2baa08a10f70ce25539fb2f006)

* **Add a filter**: With the bar visible, click **+**, choose an attribute, and set condition and value; the view updates and a new chip appears.
* **Edit a filter**: Click a chip, change condition or value, then confirm.
* **Remove a filter**: Click the chip and choose delete; the view updates immediately.
* **Clear all filters**: Click **Clear** in the filter bar.
* **Sort**: Click **Sort**, pick attributes such as **Priority**, **Created date**, or **Owner**, and **Ascending** or **Descending**; you can stack sorts — primary first, then tie-breakers.

![Sort.gif](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/13198750&key=66ab339a0218e330a5ef4966f9733e7b5d58c872f16a26e00dc1260666b23248)

* **View options**: Toolbar icon opens view type, **Group by**, and column visibility.

![view options.gif](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/13198764&key=2e322cc3580a4945ce0b3a1961cf5b8d29c7f9ac51c8e7ccbd21fa9ef85d64bc)

* **View type**: Under **View options** > **View type**, choose **List**, **Board**, or **Gantt**; it persists when you **Save**. List, board, and Gantt share the same filters and configuration. **Board** shows cards in columns (for example Stage or Priority); drag cards between columns to update values (Kanban-style triage or sprints). **Gantt** timelines records by target start and close date. Only object types with those fields (for example [[entities/enhancement|enhancements]]) support it; issues and tickets without target dates do not.
* **Group by**: Under **View options**, set **Group by** to an attribute such as **Stage**, **Owner**, or **Priority** to split the view into labeled sections; clear **Group by** there to remove grouping. When a group-by attribute is applied, each group displays up to 30 records.
* **Columns**: Under **View options**, toggle attributes such as **Priority**, **Stage**, **Owner**, **Asset**, or **Changes Needed**; visibility saves with **Save**.
* **Search**: Click **Search**, type part of a name or description; matches narrow as you type (record IDs are not required).

![search.gif](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/13198837&key=412c23c839220b98b6b1f6cf727bb30e7c02d0df0627eeae7a91b07212f5f02b)

## View management

* **Share a view**: Views are private by default. **Actions** > **Share** opens **Share View**; search people on **Owner** or groups on **Group**, assign **Viewer** or **Editor**, optionally enable **Anyone in organization**, then **Share**. External and inactive users do not appear in search — use **Copy link** instead. Recipients see shared views under **Shared with me**.
* **Access**: Users open or edit a view only if it is shared with them or a group they belong to — even a direct URL does not bypass that. **Viewers** see the view and data but cannot save; **Editors** can save changes.
* **Managing access**: Editors and the creator open **Actions** > **Share** to see everyone with access and their roles; click **Remove access** on an entry to revoke it.
* **Actions** > **Export**: Filtered views can be exported as **CSV** or **JSON**. **Export all columns** includes every attribute, not only visible columns. Since exports honor active filters, excluded records are omitted.

  > 📝 **Note**: Exports run asynchronously and make take some time depending on the size of the data set. A popup announces completion, and you can also see completed exports in **Updates > Others** or [**Settings > Jobs**](https://app.devrev.ai/?setting=jobs).
* **Actions** > **Reporting**: Refer to [[support-articles/computer-by-devrev/vista-reports|Vista Reports]].

![One-click export of all columns.gif](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/13198879&key=4059e288a2d8a9c910ba267add9d524f9ec3ff7d15b655c38b4f2ac7a6cb8ce9)

* **Delete a view**: **Actions** > **Delete**, then confirm in the dialog. Underlying records are not deleted.

## Related wiki nodes
- [[features/vistas]]

## Source
- DevRev support [[entities/article|article]] [Vistas](https://support.devrev.ai/en-US/devrev/article/SZYVVBEk) (ART-21835)
