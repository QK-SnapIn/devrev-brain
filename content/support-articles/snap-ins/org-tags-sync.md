---
title: Org tags sync
devrev_id: ART-21942
parent_directory: Automate
translation_group: 1v0qi5L8
modified_date: "2025-12-10T06:57:17.255Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/1v0qi5L8"
tags: []
top_category: Snap-ins
wiki_match: glossary/airsync
match_score: 0.5
last_updated: 2026-05-11
summary: "The Org tags sync snap-in is an automation tool designed to synchronize tags across multiple organizations."
---

# Org tags sync

The **Org tags sync** snap-in is an automation tool designed to synchronize tags
across multiple organizations.

When a new tag is created in the main organization, the snap-in ensures the tag
is automatically propagated to all linked organizations. Updates to existing
tags in the main organization are reflected in other organizations. Copies all
existing tags from the main organization to all linked organizations via
command.

## Configuration

Follow these steps to set up the Org tags sync snap-in:

1. Go to **Snap-ins** > **Org Tags Sync** > **Configure**.
2. Fill in the configuration settings.

   * **Connect your snap-ins workspace**: Go to the **Connections** and locate
     the **Connect your Snap-ins workspace** section. Click **[[features/search|Search]] for
     Connections** and select **Org tags sync** from the list of available
     options.
   * Enter connection details:

     + **Connection Name**: Provide a name for this connection. This can be any
       meaningful label that helps you identify the connection later.
     + **Org # PAT**: Enter the Personal Access Token (PAT) for the target
       organizations you wish to synchronize tags with.
3. Click **Save**.
4. Click **Install** to activate the snap-in.

Once the snap-in is installed, it automatically starts checking newly created
and updated tags and creates or updates them on the linked organizations.

### Trigger tag sync for existing tags

To create and update tags that were created before the snap-in was installed:

1. Go to the **Events/Discussions** section in the snap-in.
2. Enter the command: `/org_tag_sync`.
3. Allow time for the process to complete—this may vary depending on the number
   of existing tags.

## Source
- DevRev support [[entities/article|article]] [Org tags sync](https://support.devrev.ai/en-US/devrev/article/1v0qi5L8) (ART-21942)
