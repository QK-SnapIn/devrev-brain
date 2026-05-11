---
title: GitHub
devrev_id: ART-21980
parent_directory: Integrate
translation_group: z0oDB6a6
modified_date: "2025-12-10T06:57:40.678Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/z0oDB6a6"
tags: []
top_category: Snap-ins
wiki_match: features/github-integration
match_score: 0.85
last_updated: 2026-05-11
related: ['features/github-integration']
---

# GitHub

Bring your code to the center of your decision-making with GitHub and DevRev. The GitHub integration allows GitHub users to onboard to DevRev and automate day-to-day activities, removing the need for tedious manual tasks.

* Work automation: Connect GitHub events to your DevRev issues.
* Magic Commands: Update DevRev issues without leaving your IDE.
* Autotrack work: Automatically track your work in DevRev even without creating an issue ahead of time.
* PR Task Creation: Create DevRev tasks for PR reviewers.
* PR Reminders: Automatically remind PR reviewers when a PR goes stale.

## Work automation

You can enable GitHub work automation through the [GitHub for DevRev snap-in](https://devrev.ai/marketplace/github) by establishing a GitHub connection and setting up a webhook.

To set up the GitHub for DevRev snap-in, go to [Marketplace](https://devrev.ai/marketplace) and install the [GitHub for DevRev snap-in](https://devrev.ai/marketplace/github).

## Webhook registration

You can register the webhook for an entire GitHub organization. The GitHub snap-in automatically completes the webhook registration and updates the timeline with a confirmation message stating, *The webhook registration on GitHub was successful*.

If the webhook registration fails, the snap-in will update the timeline with the message: *The webhook registration on GitHub was unsuccessful*. Refer to the instructions in the **Instructions** tab to manually complete the registration.

For manual webhook registration, follow the instructions below:

1. Go to **Settings > Webhooks** in your GitHub organization or repository and select **Add webhook**.
2. Add the following in the **Payload URL** field:

   ```
   https://api.dev.devrev-eng.ai/hidden/dev-orgs/DEV-787/event-source-webhooks/github/2ce09ba6-1d08-4cb6-ac0b-e0b2169aa18c
   ```
3. Set **Content type** to `application/json`.
4. Add the unique secret for each organization, like `dsnYinUbUK2U7ea3Ym1PlVxywHZ28B`.
5. In **Events**, select **Let me select individual events**. Select the following events:

   a. **Branch or tag creation**

   b. **Pushes**

   c. **Pull requests**

   d. **Pull request review comments**

   e. **Pull request review threads**

   f. **Pull request reviews**
6. Finalize the creation by clicking **Add webhook** in GitHub and closing this window.

### GitHub events

**Associate GitHub events with DevRev work**

You can associate GitHub commits, branches, and pull requests with the issues they correspond to. Doing so allows you to see GitHub activity in the corresponding DevRev issue and to act on those events, allowing you to automate your manual tasks.

**Commits**

You can associate commits with their corresponding issue by either of these methods:

1. Including one or more issue IDs anywhere in the commit message.

   * Example: `Fix: paging issue (issue:123)`
   * Example: `Disable routing table ISS-123 and default to zero ISS-231`
2. Include it in a branch name, PR title, or PR description that is associated with an issue.

**Branches**

You can associate a branch with its corresponding issues by including one or more issue IDs in the branch name. For example, branch `mavis/iss-123/teaches-typing`. All commits in this branch are automatically associated with issue `iss-123`, without you having to explicitly include it in the commit message.

**Pull Requests**

You can track your PRs with the corresponding issues by including one or more issue IDs in the PR title or description. For example, the PR title `iss-123 Fixes paging issue` links the PR to `ISS-123`.

# Work formats

You can explicitly link an issue ID to a commit, branch, or PR by using the following formats:

1. Using a display ID: `ISS-123`
2. Using an issue ID: `issue:123`

The display ID and issue ID are case-insensitive, the following are all acceptable and refer to the same issue:

* `ISSUE:123`
* `Issue:123`
* `issue:123`
* `ISS-123`
* `Iss-123`
* `iss-123`

### Automation

After a GitHub event is associated with an issue, the status of that issue is automatically updated according to the following rules:

|  |  |
| --- | --- |
| GitHub Event | Default Stage |
| New branch | *In Development* |
| Draft PR opened | *In Development* |
| PR opened | *In Review* |
| PR merged | *In Development* |
| PR closed | *In Development* |

For any specific GitHub event, organizations can configure which stage the issues should move to using the GitHub snap-in configuration. An organization can also select *None* if they do not want stage updates on issues for any specific GitHub event.

## Magic commands

With magic commands, you can perform various actions on your DevRev issues without leaving your IDE.

Supported magic commands:

### Toward

**/toward** can be used in a PR body to associate a PR with multiple DevRev issues without having to include them in the PR title. This associates the PR with the issues and the automations for stage changes apply just as if the issue IDs had been included in the title.

Example:

```
Fixes various formatting issues.
/towards ISS-31 ISS-232 ISS-421
```

### Close

**/close** can be used in a PR body to both associate a PR with multiple DevRev issues and close them when the PR is merged. This associates the PR with the issues and the automations for stage changes apply as soon as the PR is pushed to GitHub. Once the PR is merged, the issues are closed. If the command is not included, the issue stage will move from *In Review* to *In Development*, instead of transitioning to the closed state.

Example:

This associates and closes all 3 issues.

```
Fixes various formatting issues.
/close ISS-31 ISS-232 ISS-421
```

The special keyword #work can be used to close any issues already associated with a PR without having to specify them, such as when the issue IDs are already in the title. By running the command below, the specified issue stages will be moved to *Completed* by default.

```
Fixes various formatting issues.
/close #work
```

## Automatic work detection

DevRev can automatically track your coding activity, even if you don't explicitly associate it with an issue. When you create a new branch or PR, and the branch or PR isn't explicitly associated with an issue, DevRev creates an issue for you. We call this an autonomous issue or autonomous work item. DevRev fills in the details for you but you can rename the issue in DevRev, or mark it as belonging to a different, existing issue.

The automation configured to update the stages of issues based on GitHub events also applies to autonomous issues.

To make use of this feature, go to **My settings** and toggle **Enable for me**.

1. You can enable the "Create DevRev issue when a new branch is created" or the **Create DevRev issue when a new PR is opened** feature in the [GitHub for DevRev snap-in](https://devrev.ai/marketplace/github).
2. The "Default part to assign autonomous issues to" has been set to a valid part ID.

Each developer who wants to use the automatic work detection feature must link their GitHub account by going to **Settings** > **Account** > **External Identities** and **Link GitHub Account**.

You can configure these automations from [GitHub for DevRev snap-in](https://devrev.ai/marketplace/github).

## Task creation

DevRev can help you keep track of your issues while they're in the PR process. With PR Task Creation, a task is created for each PR reviewer in the DevRev issue associated with the PR. These tasks are automatically marked as completed when the reviewer approves or denies the PR or when the PR is closed for any reason.

To make use of this feature, the following conditions must be met:

1. The DevRev organization has enabled the **Create task for PR reviewers** feature in the [GitHub for DevRev snap-in](https://devrev.ai/marketplace/github).
2. Each developer that wants to use this feature has to link their GitHub account by going to **Settings** > **Account** > **External Identities** and **Link GitHub Account**.

## PR reminders

PRs can often go stale and delay the development process. With PR reminders, developers can be automatically notified when a PR has been inactive for a period of time.

To make use of this feature, the following conditions must be met:

1. The DevRev organization has enabled the "Send reminders for inactive PRs" feature in the [GitHub for DevRev snap-in](https://devrev.ai/marketplace/github).
2. (Optionally) Set the "Number of days to wait before sending PR inactivity reminders".

## Related wiki nodes
- [[features/github-integration]]

## Source
- DevRev support article [GitHub](https://support.devrev.ai/en-US/devrev/article/z0oDB6a6) (ART-21980)
