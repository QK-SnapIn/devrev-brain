---
title: Filtering Jira Issues with Custom Fields - UI Guide
devrev_id: ART-23026
parent_directory: AirSync
translation_group: dhtjswOf
modified_date: "2026-01-20T09:56:18.227Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/dhtjswOf"
tags: []
top_category: Computer by DevRev
wiki_match: entities/issue
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/issue']
---

# Filtering Jira Issues with Custom Fields - UI Guide

> **Note**: This guide describes the current filtering capabilities. Fine-grained filter configuration through the UI may change in future releases.

---

## Prerequisites

1. **Jira Custom Field**: Create a custom field in Jira with enum/select list values
2. **Field Applied to Issue Types**: Ensure the custom field is added to the Jira issue types to be synced

---

## Step-by-Step Configuration

### Step 1: Create a Custom Field in Jira

1. Go to **Jira Settings** → **Issues** → **Custom Fields**
2. Click **Create Custom Field**
3. Associate with relevant issue types (Task, Bug, Story, etc.)
4. Add the newly created field to all the screens where you want to see the field

### Step 2: Configure Filter in DevRev

1. Navigate to **Settings → AirSync → Add connection -> Jira Sync**
2. Select your Jira sync connection
3. Go to **Sync Configuration** or **Field Mappings**
4. For each issue type you want to filter:

   * Click on the issue type (e.g., "Task", "Bug", "Story")
   * Find the **Filter** section
   * Click **Add Filter** or **Edit Filter**
   * Select your custom field
   * Choose the operator: **Any of**
   * Select the value
   * Save the filter

### Step 3: Apply to Multiple Issue Types

Repeat Step 2 for all issue types that need filtering:

* Task
* Bug
* Story
* Sub-task
* etc.

---

## How It Works

### ✅ Jira to DevRev Sync - FILTERED

When syncing from Jira to DevRev, the filter is applied:

* **Issues with "Enable Sync = Yes"** → ✅ **Synced to DevRev**
* **Issues with "Enable Sync = No"** → ❌ **NOT synced to DevRev**
* **Issues without the field set** → ❌ **NOT synced to DevRev**

**Example**:

* JIRA-100 has "Enable Sync = Yes" → Appears in DevRev
* JIRA-101 has "Enable Sync = No" → Does NOT appear in DevRev

### ⚠️ DevRev to Jira Sync - NOT FILTERED

**IMPORTANT**: Filters do NOT apply when syncing from DevRev to Jira.

In the DevRev → Jira reverse sync, only issues associated with the subtypes defined in the sync unit are synced back to Jira, while other issues are excluded.

**Example**:

* Create issue in DevRev with "Enable Sync = No" → ✅ **Still syncs to Jira**
* Create issue in DevRev with "Enable Sync = Yes" → ✅ **Syncs to Jira**
* Create issue in DevRev (any field value) → ✅ **Always syncs to Jira**

---

## Summary

| Direction | Filtering | Behavior |
| --- | --- | --- |
| **Jira to DevRev** | ✅ Supported | Only issues matching filter sync to DevRev |
| **DevRev to Jira** | ❌ Not Supported | ALL issues sync to Jira without filtering |

**Key Takeaways**:

* ✅ Use Jira custom field values to control which issues flow into DevRev.
* ⚠️ Filters are not applied when syncing from DevRev to Jira - all issues are synced

**Limitations and Tips**:

* **Team-managed projects**: Custom fields may be project-scoped; ensure the field exists for each project in scope
* **Multiple projects**: Ensure the field context includes all projects involved in the sync

## Related wiki nodes
- [[entities/issue]]

## Source
- DevRev support article [Filtering Jira Issues with Custom Fields - UI Guide](https://support.devrev.ai/en-US/devrev/article/dhtjswOf) (ART-23026)
