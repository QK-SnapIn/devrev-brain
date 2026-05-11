---
title: Board view
devrev_id: ART-21900
parent_directory: Vistas
translation_group: KcmqnIJG
modified_date: "2025-12-10T06:56:51.101Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/KcmqnIJG"
tags: []
top_category: Computer by DevRev
wiki_match: entities/article
match_score: 0.471
last_updated: 2026-05-11
summary: "The board view transforms your work items into visual cards organized in columns and rows, replacing the need to scroll through long lists or switch between multiple tabs."
---

# Board view

The board view transforms your work items into visual cards organized in columns and rows, replacing the need to scroll through long lists or switch between multiple tabs. It helps teams visualize their workflow, limit work in progress, and manage work items through different stages of completion. It's particularly valuable for process-oriented [[features/workflows|workflows]], such as moving [[features/tickets|tickets]] through support stages, tracking [[features/issues|issues]] from development to deployment, or managing sales [[entities/opportunity|opportunities]] through pipeline stages.

## How to use it

### Set up your board

1. **Access the view**: Go to any work item list, such as Issues or Tickets, and select **Board View** from the view type selector
2. **Configure columns**: Click the **Column** option and select your primary attribute, such as Stage, Status, or Priority.
3. **Add swimlanes**: Optionally, select a secondary grouping attribute from the **Rows** drop-down to create horizontal partitions within each column.
4. **Customize cards**: Click **Customize** and select up to five fields to display on each card for readability.

![](don:core:dvrv-us-1:devo/0:artifact/4100409)

### Work with Cards

1. **View details**: By default, each card displays the work item ID, title, priority/severity, and owner.
2. **Move items**:2a. **Between columns**: Drag cards horizontally to update their primary attribute. For example, moving from *In Progress* to *Review* when grouped by stage as column.2b. **With swimlanes active**: When grouped by both column (Stage) and row (Owner), dragging works in the following ways:

   * Drag horizontally across columns within the same row to change Stage while keeping the same Owner.
   * Drag vertically between rows within the same column to reassign Owner while keeping the same Stage.
   * Drag diagonally to change both Stage and Owner simultaneously. For example, moving a card from *In Progress/John* to *Review/Sarah*.
3. **Edit inline**: Click directly on editable fields within cards to make quick updates.
4. **Bulk edit**: Select multiple cards using hover or Shift + click and apply bulk actions in one go.

![](don:core:dvrv-us-1:devo/0:artifact/4100412)

### Customize your view

1. **Create new items**: Click the **+** icon in any column or swimlane intersection to add work items with pre-filled attributes.
2. **Apply filters**: Use the filter bar above the board to show only relevant items.
3. **Sorting**: Cards maintain your selected sort order selected via the **Order by** drop-down.
4. **Cell load limit**: Set the number of cards you want to load and view in one go per column or per cell when swimlanes are set.
5. **Handle restrictions**: Cards in columns representing non-editable fields show a lock icon and prevent dragging.
6. **Hide columns**: Click on 3 dots next to a column to hide it from the view to reduce clutter
7. **Save preferences**: For any change in view preference settings like filter, sort, column, row selection click Save on top to save it as a new view or update the existing view

## Best practices

* **Optimal Setup**: Use Stage or Status as your primary column grouping since these represent natural workflow progression. Reserve swimlanes for secondary attributes like Owner, Priority, or [[entities/part|Part]] when you need to see distribution across multiple dimensions.
* **Card Management**: Keep card fields to essential information only—too many fields make cards cluttered and hard to scan. Include ID, Title, Owner, and one status indicator as your baseline.
* **Performance Considerations**: For large datasets with 500+ items, apply filters before switching to board view to maintain responsiveness.
* **Column management:** Hide empty columns to reduce visual clutter when working with sparse data distributions.

## Source
- DevRev support [[entities/article|article]] [Board view](https://support.devrev.ai/en-US/devrev/article/KcmqnIJG) (ART-21900)
