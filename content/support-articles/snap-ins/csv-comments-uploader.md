---
title: CSV comments uploader
devrev_id: ART-21936
parent_directory: Automate
translation_group: o0SkItaZ
modified_date: "2026-01-05T14:39:51.383Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/o0SkItaZ"
tags: []
top_category: Snap-ins
wiki_match: features/commerce
match_score: 0.414
last_updated: 2026-05-11
summary: "The CSV comments uploader is a snap-in designed to streamline the process of creating timeline entries on work items in bulk through a CSV file."
---

# CSV comments uploader

The CSV comments uploader is a snap-in designed to streamline the process of creating timeline entries on work items in bulk through a CSV file. It efficiently handles timeline entries while providing dynamic error handling and detailed tracking. With comprehensive status reporting, users receive a clear breakdown of successful and failed operations, including row numbers, error reasons, and the link of the created timeline entries.

## Feature

* **Access Control**: Ensures only authorized users from the [[entities/group|group]] selected in the snap-in configuration can run the snap-in

## CSV requirements

1. The `display_id` field is mandatory and must contain a valid work item display ID.
2. For tagging users in the timeline entries, use the format `<user@email.com>`.
3. Timeline entries can be added to both internal discussions and customer messages.
4. The CSV should contain at least one of `internal_discussion` or `external_discussion` columns.

The maximum row limit for the input CSV is 5,000.

## Validations for uploading CSV

The following validations are done while creating timeline entries on work items in DevRev:

1. **Display ID** is a mandatory field and must be filled according to the sample CSV file.
2. Do not re-run the command until a timeline is initiated for re-execution, and click the **Submit** button only once.

## Upload comments from CSV on work-items

1. Add the **CSV Comments Uploader** snap-in from the DevRev Marketplace to your environment.
2. In the snap-in configuration, select the appropriate group you want to give access to run the snap-in
3. In the **Discussion** tab of the snap-in, enter `/upload_timelines`.
4. A sample CSV file is generated, with display\_id as a mandatory field.
5. Click **Upload**, browse and select the file, and then click **Submit**.
6. If all required headers exist in the CSV and the correct fields are provided as headers, a timeline comment is generated in the **Discussion** tab of the snap-in with the validation result of headers passed. Otherwise, it displays the invalid headers and any missing required headers.
7. After the operation is completed, a sample CSV is generated in the **Discussion** tab of the snap-in with the status of the operation, including each line number, any error messages for failed rows, and the link of the successfully created timeline entry for successful rows.
8. In case of a retry, a timeline entry is created, and the user needs to re-enter the command `/upload_timelines`.

## Source
- DevRev support [[entities/article|article]] [CSV comments uploader](https://support.devrev.ai/en-US/devrev/article/o0SkItaZ) (ART-21936)
