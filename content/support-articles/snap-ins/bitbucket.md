---
title: Bitbucket
devrev_id: ART-21972
parent_directory: Integrate
translation_group: 86lhlMKY
modified_date: "2025-12-10T06:57:36.151Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/86lhlMKY"
tags: []
top_category: Snap-ins
wiki_match: entities/ticket
match_score: 0.667
last_updated: 2026-05-11
summary: "Bring your code to the center of your decision-making with Bitbucket and DevRev."
---

# Bitbucket

Bring your code to the center of your decision-making with Bitbucket and DevRev. The Bitbucket integration allows Bitbucket users to onboard to DevRev and automate day-to-day activities, removing the need for tedious manual [[entities/task|tasks]].

* **Work automation**: Connect Bitbucket events to your DevRev [[features/issues|issues]].
* **Magic [[features/commands|commands]]**: Update DevRev issues without leaving your IDE.
* **Autotrack work**: Automatically track your work in DevRev even without creating an [[entities/issue|issue]] ahead of time.
* **PR [[entities/task|task]] creation**: Create DevRev tasks for PR reviewers.
* **PR reminders**: Automatically remind PR reviewers when a PR goes stale.

For more information, refer to the [Bitbucket for DevRev snap-in](https://marketplace.devrev.ai/bitbucket) on the DevRev marketplace.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **Explore Marketplace** in the top-right corner.
2. In the DevRev marketplace, find **Bitbucket for DevRev** and click **Install**.
3. During the snap-in installation, follow the instructions for installing the webhook. The webhook can be installed for an entire Bitbucket org or specific repositories. If you install the webhook successfully, the message "Webhook installed successfully" is displayed in the **Discussions** tab. If it was not installed correctly, you could see "Webhook installation is unsuccessful". If the webhook is not successfully installed, you need to create the webhook manually by following the instructions below.

## Configuration

### Work automation

You can enable Bitbucket work automation through the Bitbucket for DevRev snap-in by establishing a Bitbucket connection and setting up a webhook.

### Bitbucket events

**Associate Bitbucket events with DevRev work**

You can associate Bitbucket commits, branches, and pull requests with the issues they correspond to. Doing so allows you to see Bitbucket activity in the corresponding DevRev issue and to act on those events, allowing you to automate your manual tasks.

**Commits**

You can associate commits with their corresponding issue by either of these methods:

* Including one or more [[support-articles/snap-ins/github#work-formats|issue IDs]] anywhere in the commit message.

  + Example: `Fix: paging issue (issue:123)`
  + Example: `Disable routing table ISS-123 and default to zero ISS-231`
* Including it in a branch that's associated with an issue.

**Branches**

You can associate a branch with its corresponding issues by including one or more issue IDs in the branch name. For example, `branch mavis/iss-123/teaches-typing`. All commits in this branch are automatically associated with the issue `iss-123`, without you having to explicitly include it in the commit message.

**Pull requests**

You can track your PRs with the corresponding issues by including one or more issue IDs in the PR title. For example, the PR title `iss-123 Fixes paging issue` links the PR to **ISS-123**.

### Work formats

You can explicitly link an issue ID to a commit, branch, or PR by using the following formats:

1. Using a display ID: `ISS-123`
2. Using an issue ID: `issue:123`

The display ID and issue ID are case-insensitive, the following are all acceptable and refer to the same issue:

* `ISSUE:123`
* `Issue:123`
* `issue:123`
* `ISS-123`
* `Iss-123`
* `iss-123`

### Automation

After a Bitbucket event is associated with an issue, the status of that issue is automatically updated according to the stages you have selected and configured in the snap-in configuration screen. An example configuration of Bitbucket event-to-stage mapping can be:

|  |  |
| --- | --- |
| Bitbucket Event | Stage to assign to |
| New commit | *In Development* |
| New branch | *In Development* |
| PR Opened | *In Review* |
| PR Closed | *In Development* |

## Magic commands

With magic commands, you can perform various actions on your DevRev issues without leaving your IDE.

Supported magic commands:

### Toward

`/toward` can be used in a PR body to associate a PR with multiple DevRev issues without having to include them in the PR title. This associates the PR with the issues and the automations for stage changes apply just as if the issue IDs had been included in the title.

Example:

```
Fixes various formatting issues.
/towards ISS-31 ISS-232 ISS-421
```

### Close

`/close` can be used in a PR body to both associate a PR with multiple DevRev issues and close them when the PR is merged. This associates the PR with the issues and the automations for stage changes apply as soon as the PR is pushed to Bitbucket. Once the PR is merged, the issues are closed.

Example:

This associates and closes all 3 issues.

```
Fixes various formatting issues.
/close ISS-31 ISS-232 ISS-421
```

The special keyword `#work` can be used to close any issues already associated with a PR without having to specify them, such as when the issue IDs are already in the title.

```
Fixes various formatting issues.
/close #work
```

## Automatic work detection

DevRev can automatically track your coding activity, even if you [[glossary/don|don]]'t explicitly associate it with an issue. When you create a new branch or PR, and the branch or PR isn't explicitly associated with an issue, DevRev creates an issue for you. We call this an autonomous issue or autonomous work item. DevRev tries to fill in the details for you but you can rename the issue in DevRev, or mark it as belonging to a different, existing issue.

To make use of this feature, go to **Configurations** > **Track Autonomous work**.

* You can keep it disabled if you choose to explicitly create issues and link your Bitbucket activity or you can enable it either for PR creation or branch creation event.
* Select the default [[entities/part|part]] under **Default part for autonomous issues** as a default Part ID if you enable **Track autonomous work**. Autonomous issues originating from BitBucket will be attributed to a default part. You can configure the default part while setting up your snap-in. Every issue in DevRev must have a part attribution.

### Autonomous work lifecycle

The lifecycle of autonomous work will also be automatically updated based on the stage of Bitbucket event mapping. Closing of autonomous work items based on PR close event is a user-level setting that each individual developer can opt-in for based on their preferences under **My Settings** and toggle on **Enable for Me**.

## Task creation

DevRev can help you keep track of your issues while they're in the PR process. With PR Task Creation, a task is created for each PR reviewer in the DevRev issue associated with the PR. These tasks are automatically marked as completed when the reviewer approves or denies the PR or when the PR is closed for any reason.

To make use of this feature, the following conditions must be met:

1. Create task for PR reviewers is enabled under **My Settings** and toggle on **Enable for me**.
2. Each developer that wants to use this feature has to link their Bitbucket [[entities/account|account]] by going to **Settings** > **Account** > **External Identities** and **Link Bitbucket Account**.

## PR reminders

PRs can often go stale and delay the development process. With PR reminders, developers can be automatically notified when a PR has been inactive for a period of time.

To make use of this feature, the following conditions must be met:

1. Enable the **Send reminders for inactive PRs** feature in the snap-in in your DevRev organization.
2. (Optional) Set the **Days before sending PR reminders**.

## Source
- DevRev support [[entities/article|article]] [Bitbucket](https://support.devrev.ai/en-US/devrev/article/86lhlMKY) (ART-21972)
