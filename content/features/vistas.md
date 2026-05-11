---
title: Vistas
type: feature
status: draft
sources: [raw/docs/devrev-docs-scraped.md, https://support.devrev.ai/en-US/devrev/directories]
related: ["glossary/vista", "features/analytics"]
last_updated: 2026-05-11
docs_url: https://docs.devrev.ai/product/vistas
support_articles: [ART-21835]
---

# Vistas

## What it does
Vistas are saved, configurable views of work objects, issues, tickets, accounts, parts, and more. Users can filter, sort, group, and arrange columns to create focused views of their data.

## Why it exists
Teams need customizable views of their work to support different workflows -- triage, standups, sprint planning, escalation tracking. Vistas let users create and share these purpose-built views without modifying underlying data.

## Sub-types

| View type | Description |
|-----------|-------------|
| **List view** | Tabular layout with column customization |
| **Board view** | Kanban-style with drag-and-drop; supports swimlane rows |
| **Sprint boards** | Active, past, and upcoming sprints; linked to parts |
| **Vista reports** | Charts and graphs built on vista data |

## Finding Views
Views are accessible via **Explore** in the left navigation:
- **Stock Views** — pre-built views provided by DevRev
- **My Views** — user-created private views
- **Shared** — views shared by other team members

Views can also be **pinned to the left navigation sidebar** for quick access (default pinned views include Issues, Tickets, Inbox, Parts).

## Creating Views

**From Left Navigation:**
1. Click the **+** icon next to any section
2. Select object type (Issue, Ticket, Account, Part)
3. Choose a section to pin the view
4. View opens and appears in selected section

**From Existing View:**
1. Open any view and make modifications
2. Click **Save as** button when changes are pending
3. Enter name, optional description, and section
4. View saves under selected section or in **My Views**

## View Toolbar Controls
Located in top-right, from left to right:
- **Search** -- inline search within current view
- **Sort** -- order results by any attribute
- **Filter** -- toggle filter bar visibility
- **View options** -- configure columns, view type, grouping
- **Actions (three-dot menu)** -- share, export, delete options
- **Save** -- appears only when pending changes exist

## Filtering

**Showing/Hiding:** Click filter icon (funnel) to toggle bar visibility, displaying active filter chips.

**Adding Filters:**
1. Click filter icon
2. Click **+** in filter bar
3. Select attribute, set condition and value
4. View updates immediately

**Editing:** Click existing filter chip, adjust settings, confirm changes.

**Removing:** Click filter chip, select delete option. Use **Clear** button to remove all filters at once.

## Sorting
1. Click **Sort** icon
2. Select sorting attribute (Priority, Created date, Owner)
3. Choose **Ascending** or **Descending**
4. Multiple sort conditions supported

## View Options
Click **View options** icon to access three configuration areas:

**View Type:** Switch between **List**, **Board**, or **Gantt** layouts without losing filters.

**Group By:** Select attributes like Stage, Assignee, or Priority. Clear selection to remove grouping.

**Columns:** Toggle individual attributes on/off (Priority, Stage, Owner, Asset, Changes Needed). Visibility saves with the view.

## Search Within Views
1. Click **Search** icon
2. Type record name or description
3. Results filter as you type
4. No need to know record ID

## Sharing Views (RBAC)
Views are private by default. To share:
1. Click **Actions (three-dot menu)** and select **Share**
2. Search for individuals or groups
3. Assign roles: **Viewer** or **Editor**
4. Enable "Anyone in organization" toggle for **org-wide access**
5. Click **Share**

Shared views appear under "Shared with me" in left navigation.

**Access Control (RBAC):**
- Views can be shared **org-wide** or to **specific people**
- **Viewers** can see view and data but cannot save changes
- **Editors** can make and save modifications
- External/inactive users don't appear in search

## Export
1. Click **Actions (three-dot menu)**
2. Select **Export**
3. Choose format: **CSV** or **JSON**
4. Use **Export all columns** for every attribute

Exports reflect currently applied filters only.

## Deleting Views
1. Find view in left nav
2. Click edit icon next to view name
3. Click **Remove access**
4. Click **Delete** to confirm

Deletion affects only the view, not underlying records.

## Best Practices
- Define clear goals before creating views; focused views answer specific questions
- Keep views focused with minimal filters to ease maintenance
- Share views across teams for unified context during standups, triage, and reviews
- Use descriptive names like "Q2 Customer Escalations P1 & P2" with descriptions
- Regularly review and adjust views as workflows evolve

## Entry points
- Left navigation sidebar (pinned views)
- Explore section (all views)

## Related flows
- [gap] Vista creation and sharing flow

## Related scenarios
- [gap] Scenarios to be defined

## Open questions
- [gap] What is the maximum number of views a user can create?
- [gap] What are all the available grouping attributes?
- [gap] How do Vista reports differ from Dashboard widgets in [[features/analytics]]?

## Support documentation

Referenced DevRev support articles synchronized from [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories):

- [[support-articles/computer-by-devrev/vistas|Vistas]] (ART-21835) — [external](https://support.devrev.ai/en-US/devrev/article/SZYVVBEk)
