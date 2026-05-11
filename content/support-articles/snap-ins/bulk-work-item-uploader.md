---
title: Bulk work item uploader
devrev_id: ART-21929
parent_directory: Automate
translation_group: oE5z15dL
modified_date: "2025-12-23T16:13:43.676Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/oE5z15dL"
tags: []
top_category: Snap-ins
wiki_match: features/workflows
match_score: 0.462
last_updated: 2026-05-11
---

# Bulk work item uploader

The [bulk work item uploader](https://devrev.ai/marketplace/bulk-ticket-uploader) enables you to upload multiple tickets or issues from a CSV file to DevRev. It's useful when migrating work items from a third-party system to DevRev or creating tickets or issues in bulk from a CSV file. The CSV file supports the following columns:

```
Title,Description,Owners,Part,Tags,Subtype,WorkType
Front page not loading,"This is a sample ticket body with “” quotes",youremail@example.com,PROD-1,frontend,subtype1,Ticket
APIs returning errors,"The user.get API is returning 500",youremail@example.com,PROD-2,backend,subtype2,Issue
```

The `Title` column is required, while the others are optional. If the `WorkType` column is not specified or empty, the work item is created as a ticket.

If the CSV lists multiple owners, only the first is set as the owner in the DevRev ticket. Update the owner value to the email. In the Subtype column, write the name of the subtype instead of the display name. Default work item created is a ticket if not specified.

For detailed information about DevRev tickets, refer to [[support-articles/computer-plus-support/tickets|Tickets]].

For detailed information about DevRev issues, refer to [[support-articles/computer-plus-build/issues|Issues]].

## Validations while creating work items

The following validations are done while importing or creating a work item in DevRev:

* A maximum of 50 work items can be created at once. If more than 50 work items are listed in a CSV file, the system doesn't upload any work items.
* The title field is mandatory. Rows with blank titles are skipped.
* A work item isn't created if a part or user ID mentioned in a row doesn't exist. Other work items aren't impacted by this.
* The workspace ID is only used for associating tickets to the workspace and not issues.
* If the CSV lists multiple owners, only the first is set as the owner in the DevRev work item.

## How to use bulk ticket uploader

1. In the **Discussion** tab of an account, ticket, part, or issue, enter `/upload_workitems`.
   A **Bulk Uploader Bot** form appears.
2. From the **Select work items' owners (max 1)** drop-down menu, select the work item's owner name.
3. From the **Select a part to assign to work items** drop-down menu, select a part for the work items. If the bulk work item upload is done using a part, the part is automatically selected.
4. In the **Customer ID** drop-down menu, select from the available workspaces associated with this account. If the bulk ticket upload is done using an account, the relevant workspaces are shown in the **Customer ID** drop-down menu.
5. Click **Upload**, browse, and select the file. The CSV file is uploaded.
6. Click **Submit**.

   The **Bulk Uploader Bot** processes the CSV file and creates tickets or issues with the defined parameters. The newly created work items are listed displaying the work item number and title.

## Source
- DevRev support article [Bulk work item uploader](https://support.devrev.ai/en-US/devrev/article/oE5z15dL) (ART-21929)
