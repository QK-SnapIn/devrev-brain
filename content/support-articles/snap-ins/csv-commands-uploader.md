---
title: CSV commands uploader
devrev_id: ART-21937
parent_directory: Automate
translation_group: GkwezNs3
modified_date: "2026-01-05T14:39:38.343Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/GkwezNs3"
tags: []
top_category: Snap-ins
wiki_match: features/commands
match_score: 0.85
last_updated: 2026-05-11
related: ['features/commands']
summary: "The CSV commands uploader is a snap-in designed to streamline the process of creating commands for work items in bulk through a CSV file."
---

# CSV commands uploader

The CSV [[features/commands|commands]] uploader is a snap-in designed to streamline the process of creating commands for work items in bulk through a CSV file. It efficiently handles commands while providing dynamic error handling and detailed tracking. With comprehensive status reporting, users receive a clear breakdown of successful and failed operations, including row numbers, error reasons, and the display name of command.

## Feature

* **Access Control**: Ensures only authorized users from the [[entities/group|group]] selected in the snap-in configuration can run the snap-in.

## CSV requirements

* The **Display\_name** of the command is the only mandatory column.
* For the **Owned\_by**, **Reported\_by,** and **Contact** columns, provide the email of the person to be assigned as the owner or reporter of the work item. If the CSV lists multiple owners, only the first will be set as the owner.
* For the **Applies to [[entities/part|Part]]**, **Stage**, **[[entities/account|Account]]**, **Developed with [[features/parts|Parts]]**, and **Tags** columns, provide the part name, stage name, account name, part name, and tag name respectively as it is present in the UI, ensuring case sensitivity.
* For **Date** and **Timestamp** related fields, provide the date and timestamp in the format *YYYY/MM/DD*.
* The `tnt__` prefix in some columns indicates custom fields from the tenant fragment.
* The `ctype__` prefix in some columns represents custom type fields from the custom type fragment. Users can fill these fields when selecting a subtype for a work item. If certain ctype\_\_ fields are mandatory for a specific subtype, they must be filled.
* For the `Update` operation, provide the display ID of the work item that needs to be updated.

The maximum row limit for the input CSV is 5,000.

## Validations for uploading CSV

The following validations are done while updating or creating a work item in DevRev:

1. Mandatory fields must be filled in accordance with the sample CSV file.
2. In a single run of the snap-in, users can perform either a create or an update operation, not both.
3. Do not re-run the command until a timeline is initiated for re-execution, and click the submit button only once.

## Upload commands from CSV

1. Add the **CSV Work Commands Uploader** snap-in from the DevRev Marketplace to your environment.
2. In the snap-in configuration, select the appropriate group you want to give access to run the snap-in.
3. In the **Discussion** tab of the snap-in, enter `/upload_commands`.
4. A snapkit with a drop-down appears in the **Discussion** tab of the snap-in. In the drop-down, select the type of work item you want to perform the operation on.
5. A sample CSV file is generated, with some mandatory fields specified.
6. Click **Upload**, browse and select the file, and then click **Submit**.
7. If all required headers exist in the CSV and the correct fields are provided as headers, a timeline comment is generated in the **Discussion** tab of the snap-in with the validation result of headers passed . Otherwise, it displays the invalid headers and any missing required headers.
8. After the operation is completed, a sample CSV is generated in the **Discussion** tab of the snap-in with the status of the operation, including each line number, any error messages for failed rows, and the display ID of the created commands for successful rows.
9. In case of a retry, a command timeline entry is created, and the user needs to re-enter the command `/upload_commands` .

## Related wiki nodes
- [[features/commands]]

## Source
- DevRev support [[entities/article|article]] [CSV commands uploader](https://support.devrev.ai/en-US/devrev/article/GkwezNs3) (ART-21937)
