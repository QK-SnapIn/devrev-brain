---
title: Effort logger
devrev_id: ART-21939
parent_directory: Automate
translation_group: tRt27Qm8
modified_date: "2025-12-10T06:57:15.469Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/tRt27Qm8"
tags: []
top_category: Snap-ins
wiki_match: log
match_score: 0.85
last_updated: 2026-05-11
related: ['log']
summary: "The effort logger snap-in allows users to log effort against objects with comprehensive validation and custom schema management."
---

# Effort logger

The effort logger snap-in allows users to log effort against objects with comprehensive validation and custom schema management. It provides a seamless way for teams to track time spent on [[features/tickets|tickets]], [[features/conversations-feature|conversations]], and other objects within DevRev.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **Explore Marketplace** in the top-right corner.
2. In the DevRev marketplace, find **Effort Logger** and click **Install**.

## Configuration

In **Settings** > **Menu**, the following configuration option is available:

* **Date Threshold (days)**: The date threshold for the effort log (in days). If the date is older than the threshold, the effort log is not created. If not set, the default is 365 days.

Configure the appropriate roles and permissions to access and modify the custom effort log objects based on your organization's requirements.

## Features

* **Effort logging**: Log hours and minutes worked against objects
* **Date validation**: Automatic date format validation with MM/DD/YYYY support
* **Custom schema management**: Automatic creation and validation of custom schema fragments
* **Timeline integration**: Create timeline entries for effort logs and error messages
* **Data validation**: Comprehensive validation of required fields and data types
* **Error handling**: Robust error handling with detailed error messages
* **Zero effort prevention**: Prevents logging when both hours and minutes are zero
* **Date range validation**: Ensures dates are within acceptable range (last 10 days to next 10 days)
* **Automatic cleanup**: Removes timeline entries when logging effort
* **Custom object storage**: Stores effort logs as custom objects with structured data

## How to use

1. **Access the command**: In the timeline of any [[entities/ticket|ticket]] or [[entities/conversation|conversation]], type the following command:

```
/log_effort
```

2. **Enter effort details**: The snap-in prompts you to enter:

   * **Date**: The date when the effort was performed (MM/DD/YYYY format)
   * **Hours**: Number of hours worked (0 or positive number)
   * **Minutes**: Number of minutes worked (0-59)
3. **Validation**: The system automatically validates:

   * Date format and range (within last 10 days to next 10 days)
   * Hours and minutes values
   * Prevents logging when both hours and minutes are zero
4. **Confirmation**: After successful validation, the effort is logged and a confirmation message appears in the timeline.

## Supported object types

The Effort logger snap-in works with the following object types:

* **Tickets**: Log effort against support tickets, bug reports, and feature requests
* **Conversations**: Track time spent on customer conversations and discussions

## Related wiki nodes
- [[log]]

## Source
- DevRev support [[entities/article|article]] [Effort logger](https://support.devrev.ai/en-US/devrev/article/tRt27Qm8) (ART-21939)
