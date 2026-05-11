---
title: Subtype Migration
devrev_id: ART-21954
parent_directory: Automate
translation_group: 5v0wASIB
modified_date: "2025-12-10T06:57:24.97Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/5v0wASIB"
tags: []
top_category: Snap-ins
wiki_match: features/github-integration
match_score: 0.629
last_updated: 2026-05-11
---

# Subtype Migration

The [Subtype Migration snap-in](https://marketplace.devrev.ai/marketplace/subtype-migration) is designed to facilitate the seamless transition of work items (tickets and issues) from one custom schema subtype to another. It efficiently handles large volumes of work items by processing them in batches, transferring custom field values between corresponding fields and maintaining proper workflow stages while preserving data integrity throughout the migration process.

## Installation

1. Open the DevRev marketplace and install the **Subtype Migration** snap-in.
2. Select the workspace where you want to install the snap-in, confirm your selection, and click **Deploy snap-in**.

## Configuration

1. Go to **Snap-ins** > **Subtype Migration** > **Configure**.
2. Fill in the configuration details:

   * **Work Item Type**: Select either "ticket" or "issue" based on the type of work items you want to migrate
   * **Source Subtype**: Enter the name of the current subtype from which you want to migrate work items
   * **Target Subtype**: Enter the name of the target subtype to which you want to migrate work items
   * **Field Mappings**: Enter each mapping as `source_field, target_field`, one mapping per line

   Field names and subtype names must exactly match how they appear in object customization.

   * Each `source_field` must exist in the source subtype and each `target_field` must exist in the target subtype.
   * Field types between source and target must be compatible for successful data transfer.
   * Duplicate field names should not be present in the same subtype.
3. Click **Save** and **Install**.
4. Enter `/migrate_subtype` in the Discussion section of the snap-in to start the migration process.
5. On successful validation, the snap-in presents you with a stage mapping interface. Select the **source stage** from your current subtype and the **target stage** from the destination subtype.

   * The *source* stage filters which items to migrate; the *target* stage sets their destination after migration.
   * If the stage diagram of both subtypes is the same, select the same stage as both *source* stage and *target* stage to maintain the current stage of work items during migration.

   If you need to stop a migration in progress, use the `/stop_migration`command.

   Once the migration starts, you receive a confirmation UI with details of the migration plan. After confirmation, the process begins, and progress updates are posted to the timeline. Large migrations may take time to complete, progress updates are provided throughout the process.

   The snap-in intelligently identifies fields present in the source subtype that may not be included in your field mappings, allowing you to make informed decisions about your migration plan.

   When the migration is completed, a summary is provided showing total items successfully migrated and any failed items with their display IDs. If any items fail, you can re-run the command `/migrate_subtype` to retry the migration for those specific items.

## Source
- DevRev support article [Subtype Migration](https://support.devrev.ai/en-US/devrev/article/5v0wASIB) (ART-21954)
