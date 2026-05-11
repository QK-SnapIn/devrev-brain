---
title: Qase
devrev_id: ART-21985
parent_directory: Integrate
translation_group: GhJNjSzF
modified_date: "2025-12-10T06:57:43.859Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/GhJNjSzF"
tags: []
top_category: Snap-ins
wiki_match: entities/task
match_score: 0.5
last_updated: 2026-05-11
---

# Qase

Qase integration helps foster collaboration between product development which uses DevRev Build and QA engineers on Qase who write tests and file defects for test case failures.

* PMs and engineers can understand feature testing and know if there are any missing pieces while developing the feature.
* Provides updates on test cases that failed and why they failed.
* QA engineers can log work items on DevRev when bugs are found in testing.

For more information, refer to the [Qase snap-in](https://marketplace.devrev.ai/qase) on the DevRev marketplace.

# Install

1. In DevRev, go to [**Settings** > **Integrations** > **Snap-ins**](https://app.devrev.ai/?setting=snap-ins) and click **Explore**.
2. In the marketplace, find Qase and click **Install**.

# Configure

## Create a connection

1. Create a connection by going to **Settings** > **Snap-ins** > **Connections** > **+ Connection**.
2. Choose **Snap-in Secret**, add a connection name, Qase API key, and click **Next**.

## Add the connection and part

Before you begin:

* Create a Qase API token in your account profile.
* Create a Qase project. Obtain the project code from the browser URL (e.g., `https://app.qase.io/project/DEMO`, where `DEMO` is the project code).

1. Use an existing active connection or create a new connection of snap-in-secret workspace. Add the Qase API token to the snap-in configuration under the connection settings.
2. Add the project code and the part to which the Qase defect is linked in **Configuration**.

## Configure Qase to connect to DevRev

1. Go to the **Webhooks** menu in the project settings and click on **Create new webhook**.
2. Fill in the webhook name, URL, and secret obtained from the Snap-in **Instructions** tab.
3. Select the **Created** event only in the events for defects.
4. Click **Create webhook**.

* To create a custom field: Navigate to Qase and click on **Workspace** in the left navigation. Select **Fields** and click on **Create custom field**. Inside the title and placeholder, add `DEVREV_ISSUE_ID`. In the **Entity**, select **Test case**, and in **Type**, select **Short text**, then click **Save**.
* Repeat this process for the **Entity Test run** and for the **Entity Defect** of type **Short text**, with the title and placeholder as `DEVREV_ISSUE_ID`.

## Usage

Once the configuration is complete, you can seamlessly link and manage Qase test cases, test runs, and defects within DevRev issues.

### Link DevRev issues with Qase test cases

Use the `/link_test_cases` command in the **Discussion** tab. You can either:

1. Directly search for specific test cases.

   ```
   /link_test_cases [search keyword]
   ```

   This will display test cases related to the keyword in a dropdown.
2. Run the command without a keyword.

   ```
   /link_test_cases
   ```

   This will display a random list of test cases in the dropdown.
3. Use the **search box** to find test cases by their **Qase title** or **keywords**, then click **Search** to list the related test cases.
4. Select the relevant test cases, then click **Submit** to link them to the DevRev issue.

If a test case is selected from the dropdown and another search is performed, the previously selected test case will not be linked, even after submission.

## View test cases linked to a DevRev issue

1. In Qase, add the DevRev issue ID in the custom field `DEVREV_ISSUE_ID` of the relevant test case.
2. In DevRev, open the issue and click the **Open Surface** icon in the top-right corner.
3. Select **Test Case Details** to view the linked test cases.

## View test runs linked to a DevRev issue

1. In Qase, add the DevRev issue ID in the custom field `DEVREV_ISSUE_ID` of the test run.
2. Select the desired test cases and **start the test run**.
3. In DevRev, open the issue and click the **Open Surface** icon in the top-right corner.
4. Select **Test Run Details** to view the linked test runs.

## Create defect issue creation from Qase

1. In Qase, add the DevRev issue ID in the custom field `DEVREV_ISSUE_ID` of the defect.
2. Verify that a new **defect issue** is automatically created in **DevRev** as a child of the mentioned issue.

## Source
- DevRev support article [Qase](https://support.devrev.ai/en-US/devrev/article/GhJNjSzF) (ART-21985)
