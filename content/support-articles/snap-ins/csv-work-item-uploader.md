---
title: CSV Work Item Uploader
devrev_id: ART-21935
parent_directory: Automate
translation_group: SkecO3wG
modified_date: "2026-01-09T13:36:29.203Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/SkecO3wG"
tags: []
top_category: Snap-ins
wiki_match: features/workflows
match_score: 0.474
last_updated: 2026-05-11
---

# CSV Work Item Uploader

The CSV Work Item Uploader is a snap-in designed to streamline the process of creating and updating work items in bulk through a CSV file. It efficiently handles any number of work items while providing dynamic error handling and detailed tracking. With comprehensive status reporting, users receive a clear breakdown of successful and failed operations, including row numbers, error reasons, and the display IDs of the created/updated work items.

## Feature

* **Access Control**: Ensures only authorized users from the group selected in the snap-in configuration can run the snap-in

## Commands

* `/upload_workitems`: Initiates the CSV upload process for creating or updating work items.
* `/reset_snap_in`: Resets the snap-in state and terminates any current execution, allowing you to restart the upload process. Use this command if you encounter issues during the upload process and want to terminate the current process or need to start over with a different CSV file.

## CSV requirements

1. For `Owned_by`, `Reported_by`, and `Contact` columns,provide the email of the person who should be assigned as the owner or reporter of the work item. If the CSV lists multiple owners, only the first is set as the owner.
2. For `Owned_by` column , to assign `Unassigned` as the owner of a work item, enter `unassigned` in the `Owned_by` column. This will set the owner of the work item to `Unassigned`.
3. For `Applies to Part`, `Stage`, `Account`, `RevOrg`, `Developed with Parts`, and `Tags` columns, provide the part name, stage name, account name, workspace, part name, and tag name respectively as it appears in the UI (case-sensitive).
4. For `Date` and `Timestamp` related fields, provide the date and timestamp in the format `YYYY/MM/DD`.
5. The `tnt__` prefix in some columns indicates custom fields from the tenant fragment.
6. The `ctype__` prefix in some columns represents custom type fields from the custom type fragment. Users can fill these fields when selecting a subtype for a work item. If certain ctype\_\_ fields are mandatory for a specific subtype, they must be filled.
7. For `Update` operation, provide the display ID of the work item that needs to be updated.
8. For custom fields of type ID, the user needs to input the don-id of the object.
9. For the linking of objects to work-Item, we need to enter the display ID of the object in the `links` column to link the work item to that object.

## Validations for uploading CSV

The following validations are done while updating or creating a work item in DevRev:

1. Mandatory fields need to be filled in accordance with the sample CSV file.
2. In single run of the snap-in, users can either perform create or update operation.
3. Do not re-run the command until a timeline is initiated for re-execution, and click the submit button only once.

## Upload work items from CSV

1. Add the **CSV Work Item Uploader** snap-in from the DevRev Marketplace to your environment.
2. In the snap-in configuration, select the appropriate group you want to give access to run the snap-in
3. In the **Discussion** tab of the snap-in, enter `/upload_workitems`.
4. A snapkit with two dropdowns appears in the discussion tab of the snap-in. In the first dropdown, select the type of operation you want to perform, and in the second dropdown, select the type of work item you want to perform the operation on.
5. A sample CSV file is generated, with some mandatory fields specified.
6. Click **Upload**, browse and select the file, and then click **Submit**.
7. If all required headers exist in the CSV and the correct fields are provided as headers, a timeline comment is generated in the discussion tab of the snap-in with the validation result of headers passed . Otherwise, it displays the invalid headers and any missing required headers.
8. After the operation is completed, a sample CSV is generated in the discussion tab of the snap-in with the status of the operation, including each line number, any error messages for failed rows, and the display ID of the created or updated work items for successful rows.
9. In case of a retry, a command timeline entry is created, and the user needs to re-enter the command `/upload_workitems` .

## Resetting the snap-in

If you need to restart the upload process, in the **Discussion** tab of the snap-in, enter `/reset_snap_in`. This will reset the snap-in state and terminate any current execution.

After the reset, you can run `/upload_workitems` again to restart the upload process.

## Source
- DevRev support article [CSV Work Item Uploader](https://support.devrev.ai/en-US/devrev/article/SkecO3wG) (ART-21935)
