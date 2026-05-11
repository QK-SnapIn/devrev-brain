---
title: Account and contact import
devrev_id: ART-21882
parent_directory: Customer records
translation_group: Ni6_K6iY
modified_date: "2025-12-10T06:56:40.102Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Ni6_K6iY"
tags: []
top_category: Computer+ Support
wiki_match: entities/account
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/account']
---

# Account and contact import

You can upload and manage accounts and contacts by importing data from CSV files.

![CSV upload](don:core:dvrv-us-1:devo/0:artifact/4100327)

## Import data

1. Go to the top-right corner of the **Accounts and Contacts** vista and click the ⚡ button.
2. Click **Download sample CSV**. The sample CSV file includes all the necessary headers and sample values supported by DevRev.
3. Open the downloaded sample CSV file. Fill in the required headers and values as specified in the sample CSV.

   Columns with headers that do not conform to the predefined schema will not be imported.
4. In the dialog box, upload the populated CSV file.
5. (Optional) Configure import settings.

   * **Add tags to identify new imports**: Attach any existing tags to new imports for easy identification post-import.
   * **Update existing accounts**: Select to update existing accounts by appending new values, rather than creating new objects.
6. Click **Import** to initiate the process. Notifications about successful imports and any errors will appear in the form of toasts at the bottom left.

## CSV file requirements

### Mandatory fields

To ensure a successful import, certain fields are required.

**Accounts**:

* `display_name`
* `external_refs` (a unique identifier for the account, such as the company's website domain.)

**Contacts:**

* `display_name`
* `external_ref` (a unique identifier for the contact, such as a database identifier or an email address.)
* `account_external_reference` (the external reference of the contact's parent account)

### Array fields

For fields that accept multiple values, such as **owners** and **industry**, values should be separated by commas (,). If a value contains a comma, enclose it in backticks. For example, enter "Rail, Bus & Taxi" as `` `Rail, Bus & Taxi` ``.

### Tags

Ensure all tags listed in the CSV file already exist within the application. Tags are not created automatically during the import process to prevent errors and maintain control. For example, if your CSV contains a tag in the `tags.name` column such as `Q3FY25_CSS_Forum_Bay_Area`, ensure to create the tag in the system first.

### Owner fields

For accounts, owner information must be provided in email format. Avoid using names or display names.

## Limitations

The CSV import feature currently supports a maximum of 500 rows per request. For larger datasets, split the CSV into smaller files containing up to 500 rows each.

## Troubleshooting

The following table describes the errors you may encounter during import and how to troubleshoot them:

|  |  |
| --- | --- |
| Error | Resolution |
| Invalid format for phone numbers | Validate the phone number is in E164 Format. For example, +12014631690. |
| Tags not found in organization | Pre-create the tag in the app before importing. |
| Account with external reference 'non-existing-account' not found | Ensure the parent account exists in the app before importing. |
| Mandatory field 'external\_refs' is empty | Fill all mandatory fields in the CSV. |
| Found non utf-8 character | Export the CSV with UTF-8 encoding. |
| Input CSV has no rows | Ensure the CSV contains data rows. |
| No user found with email | Ensure the email is correct and not a name. |
| Missing required headers | Include headers for the required fields in the CSV. |

## Related wiki nodes
- [[entities/account]]

## Source
- DevRev support article [Account and contact import](https://support.devrev.ai/en-US/devrev/article/Ni6_K6iY) (ART-21882)
