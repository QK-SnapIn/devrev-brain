---
title: Coralogix security integration
devrev_id: ART-21974
parent_directory: Integrate
translation_group: trsnGQg_
modified_date: "2025-12-10T06:57:37.246Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/trsnGQg_"
tags: []
top_category: Snap-ins
wiki_match: log
match_score: 0.85
last_updated: 2026-05-11
related: ['log']
summary: "The Coralogix security integration snap-in enables automatic creation and management of DevRev issues based on security alerts from your Coralogix instance."
---

# Coralogix security integration

The Coralogix security integration snap-in enables automatic creation and management of DevRev [[features/issues|issues]] based on security alerts from your Coralogix instance. This integration helps streamline your security [[glossary/incident|incident]] response workflow by bringing Coralogix alerts directly into your DevRev workspace.

## Features

* Automatic creation of issues in DevRev when Coralogix security alerts are triggered
* Rich context integration with detailed alert information
* Smart priority mapping between Coralogix severity and DevRev priorities
* Structured custom fields for enhanced alert tracking

## Install

1. Go to [**Settings** > **Integrations** > **Snap-ins**](https://app.devrev.ai/?setting=snap-ins).
2. [[features/search|Search]] for **Coralogix Security Integration** and click **Install**.
3. Configure the snap-in settings:

   * Select the default **[[entities/part|Part]] ID** for [[entities/issue|issue]] creation
   * (Optional) Set a default owner for created issues
   * (Optional) Configure tags to be added to issues
   * Click **Save** > **Install**
4. After installation, you receive:

   * A webhook URL
   * A secret signature key

## Configure coralogix webhook

1. In your Coralogix console, go to **Data Flow** > **Outbound Webhooks** > **Generic Webhook**.
2. Click **Add new webhook destination**.
3. Configure the webhook:

   * Set the HTTP method to **POST**
   * Paste the copied webhook URL in the **URL** field
   * Add the following header for authentication:

     ```
     X-DevRev-Signature: <your-secret-signature-key>
     ```

     Replace `<your-secret-signature-key>` with the signature key provided during installation.
4. Configure the payload format according to your alert requirements.

The secret signature key is used to verify that webhook requests are genuinely from your Coralogix instance. Keep it confidential and never share it publicly.

## Custom fields

The integration creates and populates the following custom fields for each issue:

|  |  |
| --- | --- |
| Field Name | Description |
| Alert Name | Name of the triggered security alert |
| Alert Action | Action taken by Coralogix |
| Alert Event Timestamp | Time when the alert was triggered |
| Application Name | Affected application or service |
| Alert URL | Direct link to the alert in Coralogix |
| Alert Metadata | Structured alert details and context |

## Priority mapping

The integration automatically maps Coralogix severity levels to corresponding DevRev priorities:

|  |  |
| --- | --- |
| Coralogix Severity | DevRev Priority |
| critical | P0 |
| error | P1 |
| warning | P2 |
| info | P3 |

## Using the Integration

Once configured, the integration works automatically:

1. When a security alert is triggered in Coralogix, it sends the alert data to DevRev.
2. The snap-in validates the webhook signature.
3. Upon successful validation, it creates a new issue with:

   * Alert details in the description
   * Mapped priority level
   * Configured tags
   * Assigned owner (if specified)
   * Populated custom fields

## Troubleshooting

If you encounter issues with the integration:

1. Verify the webhook URL is correctly configured in Coralogix.
2. Ensure the signature header is set with the correct secret key.
3. Check that the snap-in configuration has the correct Part ID.
4. Review the webhook delivery logs in Coralogix for any authentication errors.
5. Verify that the secret signature key is correctly formatted in the header.

## Related wiki nodes
- [[log]]

## Source
- DevRev support [[entities/article|article]] [Coralogix security integration](https://support.devrev.ai/en-US/devrev/article/trsnGQg_) (ART-21974)
