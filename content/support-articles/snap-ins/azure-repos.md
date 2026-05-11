---
title: Azure Repos
devrev_id: ART-22935
parent_directory: Integrate
translation_group: H3nQTPYl
modified_date: "2026-02-16T11:36:55.39Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/H3nQTPYl"
tags: []
top_category: Snap-ins
wiki_match: features/airdrop
match_score: 0.444
last_updated: 2026-05-11
summary: "Bring your code to the center of your decision-making with Azure Repos and DevRev."
---

# Azure Repos

Bring your code to the center of your decision-making with Azure Repos and DevRev.

The Azure Repos integration enables teams to streamline their development [[features/workflows|workflows]] by connecting DevRev with Azure Repos. With this snap-in, you can automatically track and manage work items directly from your Git activity, keeping your [[features/issues|issues]] and statuses always in sync and up to date.

> ⚠️ This integration supports only organization [[features/accounts|accounts]] in Azure DevOps. Personal accounts are not supported.

## Key features

* **Work automation**: Connect Azure Repos activity to your DevRev issues.
* **Autotrack work**: Automatically track your work in DevRev even without creating an [[entities/issue|issue]] ahead of time.
* **PR [[entities/task|Task]] Creation**: Create DevRev [[entities/task|tasks]] for PR reviewers.
* **PR Reminders**: Automatically remind PR reviewers when a PR goes stale.
* **Magic [[features/commands|Commands]]**: Update DevRev issues without leaving your IDE.
* **Azure Boards Support**: Use Azure Boards work item ID prefixes instead of ISS.

## Work Automation

You can enable Azure Repos automation through the Azure Repos for DevRev snap-in by establishing a connection and setting up the integration via the DevRev Marketplace.

### Install the Snap-in

1. Go to **Settings**.
2. Under the **Integration** section, select **Snap-Ins**.
3. Click on **All Snap-Ins** to view the available options.
4. Use the [[features/search|search]] bar to find **Azure Repos**.
5. Select **Azure Repos** from the search results.
6. Click the **Add** button located in the top-right corner to install the snap-in.

### Connecting Your Azure Account

Once the snap-in is installed, a configuration modal will appear. Follow these steps to connect your Azure [[entities/account|account]]:

**Add a Connection**

1. Click **Search for Connection**.
2. Click **Add Connection**.
3. From the dropdown, select **Azure Repos**.
4. You will see two connection options. To proceed using a **Personal Access Token (PAT)**, follow the steps below.

**Generate a Personal Access Token (PAT)**

1. Go to your **Azure DevOps** portal.
2. Click on your profile icon in the top-right corner and select **User Settings**.
3. Choose **Personal Access Tokens**.
4. Click the **New Token** button.
5. In the form:

   * Enter a **Name** for your token.
   * Under **Scopes**, choose **Custom Defined**.
   * Select the following scope:

     + **Code → Read**

Once generated, copy the PAT and use it in the connection modal to complete the setup.

## Azure Repos Events

Associate Azure Repos commits, branches, and pull requests with the corresponding DevRev issues to automate status updates and eliminate manual work.

### Commits

Mention issue IDs in commit messages using either format:

* Display ID: `ISS-123`
* Object ID: `issue:123`
* Azure Boards format (e.g., `AB#123`, `Task 456`)

### Branches

Include issue IDs in branch names to associate all commits under that branch with a DevRev issue. Example: `feature/iss-123-fix-ui` or `feature/AB#123-add-logging`.

### Pull Requests

Mention issue IDs in PR titles or descriptions. Example: `Fix login flow ISS-321` or `Fix pipeline error AB#876`.

## Work Formats

Supported DevRev issue references include:

* `ISSUE:123`
* `issue:123`
* `ISS-123`
* Azure Boards formats like `AB#123`, `Task 456`
* Case-insensitive format accepted.

## Automation

Based on Azure Repos activity, DevRev updates issue stages automatically:

| Azure Event | Default Stage |
| --- | --- |
| New branch | In Development |
| PR created (draft or open) | In Review |
| PR merged | In Development |
| PR closed | In Development |

[[features/customization|Customization]] is possible to map each event to specific stages or opt out of automation.

## Magic Commands

With magic commands, you can perform actions on your DevRev issues directly within your PR body in Azure Repos, just like in GitHub.

### /toward

Use `/toward` in a PR body to associate multiple DevRev issues with the PR, without needing to include issue IDs in the PR title.

**Example:**

```
Fixes form validation errors.

/toward ISS-31 ISS-232 ISS-421
```

This will associate the PR with the listed issues, and automation rules for status updates will apply.

### /close

Use `/close` to both associate and close DevRev issues when the PR is merged.

**Example:**

```
Refactors caching mechanism.

/close ISS-31 ISS-232 ISS-421
```

## Automatic Work Detection (Autonomous Issues)

If your work isn't linked to an issue, DevRev automatically creates one:

* Tracks associated branches, commits, and PRs.
* Enriched with PR titles and descriptions.
* Tagged as **autonomous**.

These issues progress through:

* **In Development** (on branch/commit)
* **In Review** (on PR creation)
* **Closed** (on PR merge or inactivity timeout)

You can configure the default [[entities/part|part]] for autonomous work.

### Enrich Autonomous Work Descriptions

Autonomous issues pull in data from related PRs. Titles and descriptions auto-update unless the user modifies them manually.

### Link Autonomous Work with Related Issues

When DevRev detects references to other issues within PR bodies, it links those as parents of the autonomous issues created.

### Automatically Close Autonomous Work

Autonomous issues are closed when:

* Related PR is merged.
* No PR is linked and timeout expires (configurable).

## PR Task Creation

Tasks are created for each PR reviewer under the associated DevRev issue. They are auto-completed when the reviewer acts or PR is closed.

**Conditions:**

* PR reviewer tasks must be enabled in Azure Repos for DevRev.
* Each developer must link their Azure DevOps account in DevRev.

## PR Reminders

To reduce PR stagnation, reminders are posted when a PR remains inactive for a configured number of days.

**Conditions:**

* Enable "Send reminders for inactive PRs" in the snap-in.
* Configure `max_inactive_days` to control reminder timing.
* Mention DevRev issues in branch names, commits, PR titles, or PR bodies to trigger reminders.

---

Start using the Azure Repos snap-in to make your software development more accountable, automated, and free of tedious status updates.

## Source
- DevRev support [[entities/article|article]] [Azure Repos](https://support.devrev.ai/en-US/devrev/article/H3nQTPYl) (ART-22935)
