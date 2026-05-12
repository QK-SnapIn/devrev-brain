---
title: Tracxn sync
devrev_id: ART-21961
parent_directory: Automate
translation_group: _FQ-4JGU
modified_date: "2025-12-10T06:57:29.218Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/_FQ-4JGU"
tags: []
top_category: Snap-ins
wiki_match: glossary/airsync
match_score: 0.556
last_updated: 2026-05-11
summary: "The Tracxn Sync snap-in automates the discovery and syncing of recently funded startups from Tracxn into DevRev."
---

# Tracxn sync

The Tracxn Sync snap-in automates the discovery and syncing of recently funded startups from Tracxn into DevRev. It helps you capture emerging [[entities/opportunity|opportunities]] and enrich *[[entities/account|Account]]* and *Contact* onjects.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **Explore Marketplace** in the top-right corner.
2. In the DevRev marketplace, find **`Tracxn Sync`** and click **Install**.

## Configuration

In **Settings** > **Menu**, the following configuration options are available:

* **Enable Sandbox Environment:**Use Tracxn’s sandbox environment for testing.
* **Enable *Account* Custom Field Mapping For Tracxn:**Use the Tracxn-based *Account* custom field mappings.
* **Enable *Account* Custom Field Mapping For DevRev:**Use static *Account* custom field values.
* **Enable *Contact* Custom Field Mapping For Tracxn:**Use the Tracxn-based *Contact* custom field mappings.
* **Enable *Contact* Custom Field Mapping for DevRev:**Use static *Contact* custom field values.
* **Enable Tags For *[[features/accounts|Accounts]]*:**Apply tags to created *Accounts*.
* **Enable Tags For *Contacts*:**Apply tags to created *Contacts*.
* ***Account* Field Mapping:**Map fields from Tracxn company objects to DevRev *Account* fields.

  **Format:**

  ```
  { "<Tracxn Field>": "<Account Field API Name>" }
  ```

  **Explanation:**
  Tracxn Field: Tracxn key exactly how it appears in the payload.
  *Account* Field API Name: Field API name in the *Account* object

  **Example:**

  ```
  { "name": "display_name", "website": "domains" }
  ```
* ***Contact* Custom Field Mapping From Tracxn:**Map Tracxn fields to custom fields in DevRev’s *Account* object.Enable ***Account* Custom Field Mapping For Tracxn** to use this.

  **Format:**

  ```
  { "<Tracxn Field>": "<Contact Custom Field API Name>" }
  ```

  **Explanation:**
  Tracxn Field: Tracxn key exactly how it appears in the payload.
  *Account* Custom Field API Name: Custom field API name in the *Account* object

  **Example:**

  ```
  { "companySize": "tnt__company_size", "industry": "tnt__industry" }
  ```
* ***Account* Custom Field Mapping Within DevRev:**Define static custom field values for *Accounts*.Enable ***Account* Custom Field Mapping For DevRev** to use this.

  **Format:**

  ```
  { "<Account Custom Field API Name>": "<Data to be inserted>" }
  ```

  **Explanation:**
  *Account* Custom Field API Name: Custom field API name in the *Account* object
  Data to be inserted: Exact data to be inserted. It can be of any type like string, boolean, or numbers

  **Example:**

  ```
  { "tnt__source": "Tracxn", "tnt__synced": "true" }
  ```
* ***Account* Tags:**Comma-separated list of tags to apply to newly created *Accounts*.

  **Example:**

  ```
  startup, funded, prospect
  ```
* ***Account* Owner:**Email of the DevRev user who should own the *Account*.

  **Example:**

  ```
  devrev.user@devrev.ai
  ```
* ***Contact* Field Mapping:**Map fields from Tracxn employee objects to DevRev *Contact* fields.

  **Format:**

  ```
  { "<Tracxn Field>": "<Contact Field API Name>" }
  ```

  **Explanation:**Tracxn Field: Tracxn key exactly how it appears in the payload.*Contact* Field API Name: Field API name in the *Contact* object

  **Example:**

  ```
  { "name": "display_name", "linkedin": "linkedin_profile" }
  ```
* ***Contact* Custom Field Mapping From Tracxn:**Map Tracxn fields to custom fields in DevRev’s *Contact* object.Enable ***Contact* Custom Field Mapping For Tracxn** to use this.

  **Format:**

  ```
  { "<Tracxn Field>": "<Contact Custom Field API Name>" }
  ```

  **Explanation:**Tracxn Field: Tracxn key exactly how it appears in the payload.*Contact* Custom Field API Name: Custom field API name in the *Contact* object

  **Example:**

  ```
  { "title": "tnt__job_title", "seniority": "tnt__seniority_level" }
  ```
* ***Contact* Custom Field Mapping Within DevRev:**Define static custom field values for *Contacts*.Enable ***Contact* Custom Field Mapping For DevRev** to use this.

  **Format:**

  ```
  { "<Contact Custom Field API Name>": "<Data to be inserted>" }
  ```

  **Explanation:***Contact* Custom Field API Name: Custom field API name in the *Contact* objectData to be inserted: Exact data to be inserted. It can be of any type like string, boolean, or numbers

  **Example:**

  ```
  { "tnt__source": "Tracxn", "tnt__verified": "true" }
  ```
* ***Contact* Tags:**Comma-separated list of tags to apply to newly created *Contacts*.

  **Example:**

  ```
  founder, outreach-target
  ```
* ***Contact* Owner Mapping:**Dynamically assign ownership of *Contacts* based on email.

  **Format:**

  ```
  { "<Owner Email>": "<Custom Field API Name>" }
  ```

  **Example:**

  ```
  { "devrev.user@devrev.ai": "tnt__contact_owner" }
  ```

## Source
- DevRev support [[entities/article|article]] [Tracxn sync](https://support.devrev.ai/en-US/devrev/article/_FQ-4JGU) (ART-21961)
