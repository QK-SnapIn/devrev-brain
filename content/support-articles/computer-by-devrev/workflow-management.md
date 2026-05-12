---
title: Workflow management
devrev_id: ART-21904
parent_directory: Workflow engine
translation_group: sgdTQ9C3
modified_date: "2026-05-06T18:50:49.074Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/sgdTQ9C3"
tags: []
top_category: Computer by DevRev
wiki_match: features/incidents
match_score: 0.579
last_updated: 2026-05-11
summary: "DevRev provides robust version management capabilities that allow you to track changes, maintain version history, and manage workflow iterations."
---

# Workflow management

DevRev provides robust version management capabilities that allow you to track changes, maintain version history, and manage workflow iterations.

* **Version persistence**: All versions are maintained in history for reference.
* **Continuous operation**: Existing versions continue running while drafts are being edited. Workflow runs which are in running/waiting state continue to use the version with which they had started.
* **Explicit publishing**: Changes only affect future runs after explicit publishing.
* **Single draft**: Only one draft version can exist at any time.

## Version states

**Published**

* The currently active version running in production
* Marked with a `Published` tag in the version history
* Remains active until explicitly replaced by a new published version
* Multiple published versions can exist in history, but only one can be actively running

**Draft**

* An unpublished working copy of a workflow
* Only one draft version can exist at a time
* Indicated by a purple banner with the message: "This is an unpublished version of the workflow"

## Version management

Located on the right side of the interface, the version history panel provides the following:

* Chronological list of all versions
* Timestamp for each version creation
* Author information for each version change
* Clear indication of published vs. draft status
* Ability to click through and view different versions

## Publish a workflow

Any changes remain in draft mode until published, and the existing version continues running during editing.

1. Draft versions can be published using the "Publish" button
2. Publishing applies changes to all future workflow runs
3. The current version remains active until the draft is published
4. Once published, the draft becomes the new active version

## Access control

* By default, only admins can edit or deploy [[features/workflows|workflows]], while all users have the ability to view them.
* There is a default [[entities/group|group]] called **Agent and Automations Admin**. Members of this group have full access to manage workflows, including creating, updating, deploying, and deleting them. You can add people to this group to grant them these permissions.
* To create custom [[entities/group|groups]] for workflow managers, go to [**Settings** > **User Management** > **Roles**](https://app.devrev.ai/?setting=user-roles). Create a new role with the necessary workflow privileges and assign this role to a group.
* If you grant Create, Read, Update, and Delete permissions, the role gains full access to perform all operations on the workflows.
* If you provide only Create and Read permissions, the role can create new workflows and view existing ones, but can only update those in draft status.

## Error handling

You can enhance your workflows with robust error handling:

* **Add an error path**: Click the three-dot menu on any step in your workflow.
* **Define error actions**: Set a specific sequence of steps to execute if an error occurs during that action.
* **Ensure graceful management**: Manage errors by enabling appropriate fallback actions, such as sending a notification or logging the error. When a step fails, any subsequent steps in the path do not execute.

## Source
- DevRev support [[entities/article|article]] [Workflow management](https://support.devrev.ai/en-US/devrev/article/sgdTQ9C3) (ART-21904)
