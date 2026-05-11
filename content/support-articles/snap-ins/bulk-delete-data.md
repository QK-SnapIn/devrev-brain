---
title: Bulk delete data
devrev_id: ART-21928
parent_directory: Automate
translation_group: rPFz5oz2
modified_date: "2026-03-24T12:03:18.764Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/rPFz5oz2"
tags: []
top_category: Snap-ins
wiki_match: features/slack-integration
match_score: 0.424
last_updated: 2026-05-11
---

# Bulk delete data

The bulk delete data snap-in allows users to quickly delete multiple tickets, issues, accounts, or contacts in DevRev. By using a command-based approach and tag-based filtering, it ensures efficient data cleanup while maintaining reliability. Furthermore, access control options are included to prevent the feature from being misused.

The following fields are mandatory:

* **Tags**
* **Object Type**

Deleted data cannot be recovered.

If items were imported via an active AirSync, the deletion will cause the sync to fail.

## Features

* **Command-based workflow:** Initiate deletions by using the `/bulk_delete` command in the timeline.
* **Tag-based filtering**: Only items matching the selected tags are deleted, providing precise control over the process.
* **Access Control**: Ensures only authorized users can perform deletions, this can be defined in the configuration.
* **Confirmation prompts**: Ensures users explicitly confirm whether they want to proceed with deletions, minimizing accidental actions.
* **Parallel execution**: Deletions are performed concurrently, ensuring fast and efficient data processing.
* **Error handling**: Failed deletions are logged, and feedback is provided directly in the timeline for review.
* **User feedback**: Detailed summaries of the deletion process are displayed in the timeline, including successful and failed operations.

## How to use bulk delete data

Accounts cannot be deleted unless all linked tickets are unlinked first.

1. Add the **Bulk Delete Data** snap-in from the DevRev Marketplace to your environment.
2. Select the tags you want to use as filters for the data deletion. These tags will determine which items are eligible for deletion.
3. In the timeline of any object, type the following command:

```
/bulk_delete
```

Select the `<data_type>` among one of the following:

* `Tickets`
* `Issues`
* `Accounts`
* `Contacts`
* `Opportunities`
* `Articles`

4. After entering the command, select the object type you want to delete from the list. Tags linked to these objects will be displayed for confirmation.
5. The repurcussions of deletion will be informed to the user before they are allowed to confirm whether they wish to proceed with the deletion.
6. The user details along with the details of execution of the delete process will be displayed in the timeline.
7. The system will log the deletion status in the timeline, detailing:

* Items successfully deleted.
* Items that could not be deleted.

If you're changing the configuration after running the command, re-run the command and then execute the snap-in to avoid mishaps.

If some items, such as accounts linked to tickets, couldn't be deleted, resolve the dependencies and re-run the command.

## Source
- DevRev support article [Bulk delete data](https://support.devrev.ai/en-US/devrev/article/rPFz5oz2) (ART-21928)
