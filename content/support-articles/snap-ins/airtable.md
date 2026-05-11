---
title: Airtable
devrev_id: ART-21922
parent_directory: Automate
translation_group: t_d0xCEa
modified_date: "2025-12-10T06:57:04.021Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/t_d0xCEa"
tags: []
top_category: Snap-ins
wiki_match: entities/article
match_score: 0.667
last_updated: 2026-05-11
---

# Airtable

The **Airtable** snap-in automates lead intake from Airtable form submissions by mapping responses to DevRev contacts, accounts, and custom objects. It supports field mapping, duplicate detection, tagging, and ownership assignment using custom configurations. Submissions are processed in real time, enabling seamless CRM integration and streamlined data management.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **Explore Marketplace** in the top-right corner.
2. In the DevRev marketplace, find **`Airtable Integration`** and click **Install**.

## Configuration

In **Settings** > **Menu**, the following configuration options are available:

* **Create Custom Object:**
  Create a custom object.
* **Create Account and Contact:**
  Enable this option to create accounts and contacts.
* **Link Account and Contact:**
  Enable this option to link the account and contact to the custom object.
* **Account Description Fields:**
  Enable this option to generate a rich description for accounts using values from multiple Airtable columns.
* **Contact Description Fields:**
  Enable this option to generate a rich description for contacts using values from multiple Airtable columns.
* **Airtable Email Columns:**
  Comma-separated list of names of the columns in Airtable that contain email addresses. These are used to link or create contacts.
* **Airtable Phone Number Column:**
  Provide the column name from Airtable that contains the contact's phone number.
* **Airtable to Custom Object Mapping:**
  Map fields from Airtable to your DevRev custom object fields.
  **Format:**

  ```
  { "<Airtable Column Name>": "<Custom Object Field API Name>" }
  ```

  **Explanation:**
  Airtable Column Name: Column name exactly as it appears in Airtable.
  Custom Object Field API Name: Field API name in the custom object schema.
  **Example:**

  ```
  { "Use Case": "tnt__use_case" }
  ```
* **Airtable to Account Mapping:**
  Map Airtable fields to DevRev Account object fields.
  **Format:**

  ```
  { "<Airtable Column Name>": "<Account Field API Name>" }
  ```

  **Explanation:**
  Airtable Column Name: Column name exactly as it appears in Airtable.
  Account Field API Name: Field API name in the account object
  **Example:**

  ```
  { "Company Name": "display_name" }
  ```
* **Account Owner:**
  Provide the email address of the DevRev user who should be the owner of the account created.
  **Example:**

  ```
  devrev.user@devrev.ai
  ```

  This field is used to assign the account to a DevRev user.
* **Account Description Fields:**
  Provide a comma-separated list of Airtable columns you want included in the generated account description.
  **Example:**

  ```
  Name, DOB, Address
  ```
* **Account Tags:**
  Provide a comma-separated list of tags to apply to newly created accounts.
  **Example:**

  ```
  is_followup, immutable
  ```
* **Airtable to Contact Mapping:**
  Map Airtable fields to DevRev *Contact* object fields.Do not include email or phone here—they're handled.
  **Format:**

  ```
  { "<Airtable Column Name>": "<Contact Field API Name>" }
  ```

  **Explanation:**
  Airtable Column Name: Column name exactly as it appears in Airtable.
  Contact Field API Name: Field API name in the account object
  **Example:**

  ```
  { "Founder First Name": "display_name", "Founder Last Name": "display_name" }
  ```
* **Contact Owner:**
  Define who should own the created contact using a dynamic mapping.
  **Format:**

  ```
  { "<Owner Email>": "<Contact Owner Field API Name>" }
  ```

  **Explanation:**
  Owner Email: Email address of the DevRev user.
  Contact Owner Field API Name: The custom field in your schema where this user ID should be stored.
  **Example:**

  ```
  { "devrev.user@devrev.ai": "tnt__owner" }
  ```
* **Contact Description Fields:**
  Comma-separated list of Airtable columns to include in the **description** field of the created contact.
  **Example:**

  ```
  Name, DOB, Address
  ```
* **Contact Tags:**
  Comma-separated list of **tags** to be applied to newly created contacts.
  **Example:**

  ```
  is_followup, immutable
  ```
* **Leaf Type:**
  The type of custom object to create.
* **Submission Date Mapping:**
  The name of the custom object API field where you want to store the Airtable submission timestamp.
* **Custom Object Mapping for Account and Contact:**
  Map the Custom Object fields to which the account and contact are linked. Use tnt values only.
  **Format:**

  ```
  { "Account": "tnt__customer", "Contact": "tnt__contact" }
  ```

  **Example:**

  ```
  { "Account": "tnt__customer", "Contact": "tnt__user" }
  ```
* **Other Information Mapping:**
  Define the field name where unmapped Airtable fields should be collected into a single field.

## Source
- DevRev support article [Airtable](https://support.devrev.ai/en-US/devrev/article/t_d0xCEa) (ART-21922)
