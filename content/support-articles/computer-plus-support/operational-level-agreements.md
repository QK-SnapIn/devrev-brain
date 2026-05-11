---
title: Operational-level agreements
devrev_id: ART-21868
parent_directory: Computer+ Support
translation_group: ztv-zLpw
modified_date: "2026-05-06T17:37:52.748Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/ztv-zLpw"
tags: []
top_category: Computer+ Support
wiki_match: features/ola
match_score: 0.912
last_updated: 2026-05-11
related: ['features/ola']
summary: "An operational-level agreement (OLA) is an internal contract that defines the service-level targets expected from different teams within your organization."
---

# Operational-level agreements

An operational-level agreement ([[glossary/ola|OLA]]) is an internal contract that defines the service-level targets expected from different teams within your organization. OLAs are customer-account-agnostic and are usually created to ensure that internal stakeholders have their own targets, which in turn helps meet the customer [[support-articles/computer-plus-support/service-level-agreements|SLAs]].

## OLA targets

### Filter issues by next OLA target

To filter [[features/issues|issues]] based on OLA compliance, use the **Next OLA Target** filter:

* **All**: Filters all issues that have an OLA applied. It does not include issues that had an OLA metric applied in the past and have since completed.
* **Breached Since**:

  + **Any**: Issues that have breached the OLA, regardless of when the breach occurred.
  + **Over an Hour**: Issues that have been in breach for more than one hour.
  + **Over a Day**: Issues that have been in breach for more than one day.
  + **Custom**: Issues that have been in breach since a specified date.
* **Will Breach In**:

  + **Any**: All issues that are not in breach.
  + **Over an Hour**: Issues with less than one hour left before breaching.
  + **Over a Day**: Issues with less than one day left before breaching.
  + **Custom**: Issues that will breach by a selected date.

### Track OLAs on issues

In the issues view, the **Next OLA Target** column displays the OLA targets for each [[entities/issue|issue]]. If there are two active metrics, the one closest to breaching is shown as the **Next OLA Target**. Negative values (for example, `-10m`) indicate how much time has passed since a metric was breached.

OLA metrics can be in the following stages:

* **Active**: The metric is currently being tracked.
* **Close to Breach**: The time spent meets or exceeds the close-to-breach target set in the policy.
* **Breached**: The time spent meets or exceeds the breach target set in the policy.
* **Paused**: The metric is paused based on stage conditions in the snap-in.
* **Completed**: The *stop* condition has been met.

Metrics in the *Active*, *Close to Breach*, or *Breached* stages may follow business hours, moving in and out of schedule without including out-of-schedule time in calculations.

In the **Detailed** view, all applied metrics and their stages can be reviewed for an issue.

## OLA policy management

### Install snap-ins

Before creating OLA policies that use metrics such as Issue Resolution Time or Acknowledgment Time, install the required snap-ins from the DevRev marketplace:

* [OLA metrics for issues](https://marketplace.devrev.ai/ola-metric-on-issues) provides the **Issue Resolution Time** metric.
* [Acknowledgment Metric on Issues](https://marketplace.devrev.ai/acknowledgement-metric-on-issues) provides the **Acknowledgment/First Response Time** metric.

Install and configure these snap-ins before publishing an OLA so that the metrics are available when you define policies.

### Create an OLA

Admins and users with OLA policy permissions can create, publish, or manage OLAs.

1. Under [**Settings** > **Support** > **OLAs**](https://app.devrev.ai/?setting=olas), click **+ Create**.
2. In the **Create OLA** window, enter a name and description for the OLA. The OLA is created in the *Draft* state, and you can assign policies to it as needed.

### Create policies within an OLA

1. Click **+ Issue Policy**.
2. In the **New Issue Policy** pane, select the appropriate **Conditions** and **Metrics**.

   Available conditions include:

   * **Subtype**: filter by issue subtype (e.g., bug, feature request).
   * **Severity**: filter by severity level.
   * **[[entities/part|Part]]**: filter by the associated part.
   * **Tags**: filter by one or more tags applied to the issue.

   Available metrics depend on which snap-ins are installed. **Issue Resolution Time** is provided by the [OLA metrics for issues](https://marketplace.devrev.ai/ola-metric-on-issues) snap-in, and **Acknowledgment/First Response Time** is provided by the [Acknowledgment Metric on Issues](https://marketplace.devrev.ai/acknowledgement-metric-on-issues) snap-in. If a snap-in is not yet installed, DevRev prompts you to install it.
3. Click **Continue**.

You can set breach and warning targets for each metric by selecting between calendar or business hours for calculation. Multiple policies can be created within an OLA, and they are applied based on priority if an issue meets conditions in more than one policy.

### Publish an OLA

After creating the necessary policies, click **Publish** to activate the OLA.

> ⚠️ **Warning**: Once an OLA is published, it cannot be edited, nor can you modify the policies or their priority order.

Only one OLA can be in the *Published* state at any time. If there is an existing published OLA, it is archived when you publish a new one. Any new issues follow the guidelines of the newly published OLA, while issues previously managed by the old OLA remain unaffected.

### Clone an OLA

If you need to modify an existing OLA, you can clone it. Cloning duplicates all the policies from the original OLA and generates a new OLA in the *Draft* state.

To clone an OLA, go to the desired OLA, click the three-dot menu (⋮) in the top-right corner, and select **Clone OLA**.

### Define OLA metrics

You can specify which issue stages trigger the OLA metric timer to *start*, *pause*, and *stop*. This configuration is available through the snap-in for each metric, which can be found at [**Settings** > **Integrations** > **Snap-ins**](https://app.devrev.ai/?setting=snap-ins).

## Troubleshooting

* **Issue**: OLA metric is not running after publishing the OLA.

  **Solution**: Verify that the required metric snap-in (OLA metrics for issues or Acknowledgment Metric on Issues) is installed and configured at [**Settings** > **Integrations** > **Snap-ins**](https://app.devrev.ai/?setting=snap-ins). Ensure the snap-in has valid stage values assigned for start and stop conditions, and confirm that the OLA is in the *Published* state.
* **Issue**: Metric snap-in was accidentally uninstalled and OLA data is missing from issues.

  **Solution**: Reinstall the snap-in from the DevRev marketplace and reconfigure the stage values. The metric resumes tracking for newly created issues once the snap-in is active and the OLA is published. Previously tracked metrics that were removed cannot be recovered automatically; contact DevRev support for assistance with historical data.
* **Issue**: Configuration changes to the snap-in do not apply to existing issues.

  **Solution**: This is expected behavior. Configuration changes apply only to issues created after the changes are saved. Issues already in flight continue under the configuration that was active at their creation. To apply new timing rules to existing issues, clone the OLA, update the policies as needed, and publish the new OLA; however, note that previously started timers on in-flight issues are not recalculated.

## Related wiki nodes
- [[features/ola]]

## Source
- DevRev support [[entities/article|article]] [Operational-level agreements](https://support.devrev.ai/en-US/devrev/article/ztv-zLpw) (ART-21868)
