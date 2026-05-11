---
title: Outlook Email
devrev_id: ART-30343
parent_directory: Integrate
translation_group: 724unkqM
modified_date: "2026-04-24T20:03:20.813Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/724unkqM"
tags: []
top_category: Snap-ins
wiki_match: glossary/trails
match_score: 0.421
last_updated: 2026-05-11
---

# Outlook Email

# Outlook Email Sender

## Overview

The **Outlook Email Sender** snap-in lets you send emails directly from DevRev workflows using your organization's Microsoft Outlook mailbox. It connects to Microsoft Graph — Microsoft's unified API for Office 365 — via an Azure AD app registration, so emails appear to come from a real mailbox in your tenant without requiring any user to be logged in.

Use this snap-in whenever a workflow needs to notify customers, teammates, or external stakeholders by email. You can personalize each email with a rich HTML body, include CC and BCC recipients, and attach files stored as DevRev artifacts.

---

## Prerequisites

Before you install the snap-in, set up the Azure AD app registration that it uses to send mail.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) with an account that has permission to register applications.
2. Go to **Identity → Applications → App registrations** and select **New registration**.
3. Give the app a descriptive name (for example, `DevRev Outlook Email Sender`) and register it.
4. After the app is created, copy and save the following values — you need them during snap-in configuration:

   * **Application (client) ID**
   * **Directory (tenant) ID**
5. Go to **Certificates & secrets → New client secret**, set an expiry, and copy the **secret value** immediately — it is shown only once.
6. Go to **API permissions → Add a permission → Microsoft Graph → Application permissions** and add:

   * `Mail.Send` — required for all emails.
   * `Mail.ReadWrite` — required when the total size of attached files is 3 MB or more.
7. Select **Grant admin consent** to activate the permissions for your tenant.

> **Note:** The sender mailbox must exist in the same Azure tenant as the app registration. It can be a regular user mailbox or a shared mailbox.

---

## Installation

1. In DevRev, open the **Snap-in marketplace** and search for **Outlook Email Sender**.
2. Select the snap-in and click **Install**.
3. When prompted, create a new **Outlook / Microsoft Graph** keyring and enter the three values you copied from Azure AD:

   * **Client ID** — the Application (client) ID.
   * **Client Secret** — the secret value from the client secret you created.
   * **Tenant ID** — the Directory (tenant) ID.
4. Save the keyring. DevRev stores these credentials securely and never exposes them in logs.
5. Complete the installation. The **Send Outlook email** action is now available in the workflow builder.

---

## Configuration

The snap-in is configured at the workflow step level. Each step that uses **Send Outlook email** has the following fields:

| Field | Required | Description |
| --- | --- | --- |
| **To** | Yes | One or more recipient addresses, comma-separated. Accepts `Name <email@domain.com>` or plain `email@domain.com` format. |
| **CC** | No | Carbon copy recipients, comma-separated. Same format as **To**. |
| **BCC** | No | Blind carbon copy recipients, comma-separated. Same format as **To**. |
| **Subject** | Yes | The email subject line. Supports workflow variables. |
| **Body** | Yes | The email body. Accepts rich text (HTML). Supports workflow variables for personalization. |
| **Sender mailbox** | Yes | The UPN or SMTP address of the mailbox that sends the email (for example, `noreply@yourdomain.com`). This mailbox must be in the same tenant as your Azure AD app. |
| **Attachments** | No | DevRev artifact IDs to attach. Maximum 10 files. Maximum 25 MB total. `.eml` files are not allowed. |

### Tips for configuration

* Use workflow variables in **Subject** and **Body** to personalize emails with customer names, ticket IDs, or other dynamic data from your workflow context.
* The **Sender mailbox** is typically a shared mailbox (for example, `support@yourdomain.com`) so the reply-to address is managed by your team rather than tied to an individual.
* If you use the **Attachments** field, make sure the artifacts are already created in DevRev before the **Send Outlook email** step runs.

---

## How the email is sent

When the workflow reaches the **Send Outlook email** step, the snap-in:

1. Retrieves a short-lived access token from Azure AD using the configured client credentials. No user interaction is needed.
2. Downloads any attached DevRev artifacts and validates their size and file type.
3. Chooses a sending method based on total attachment size:

   * **Under 3 MB total**: sends the email in a single API call with attachments included in the request body.
   * **3 MB or more total**: creates a draft message, uploads each attachment individually (using chunked uploads for large files), and then sends the draft. This path requires the `Mail.ReadWrite` permission in addition to `Mail.Send`.
4. Returns a result to the workflow — either **Success: true** or **Success: false** with an error message describing what went wrong.

---

## Result

After the step runs, the workflow receives two output values:

| Output | Type | Description |
| --- | --- | --- |
| **Success** | Boolean | `true` if the email was accepted by Microsoft Graph for delivery; `false` if an error occurred. |
| **Error message** | Text | Empty when **Success** is `true`. Contains a description of the failure when **Success** is `false`. |

Use the **Success** output in subsequent workflow steps to branch on success or failure — for example, to log a note on the ticket or trigger a fallback notification.

---

## Verifying the result

After a workflow run that includes **Send Outlook email**, verify the outcome using these steps:

1. **Check workflow run logs** — Open the workflow run in DevRev. The **Send Outlook email** step shows **Success: true** or **Success: false**. If it failed, the **Error message** output explains why (for example, invalid recipient address, missing permission, or attachment too large).
2. **Check the recipient's inbox** — The email arrives from the configured sender mailbox. If it does not appear in the inbox, check the recipient's spam or junk folder.
3. **Check the sender mailbox Sent Items** — In Outlook or OWA, open the sender mailbox (if you have access) and look in **Sent Items**. A successfully delivered email appears there.
4. **Check Azure AD audit logs** — In the Microsoft Entra admin center, go to **Monitoring → Audit logs** and filter by the app registration. Successful token requests confirm that the snap-in authenticated correctly.

---

## Limitations

| Constraint | Value |
| --- | --- |
| Maximum recipients (To + CC + BCC combined) | No hard limit enforced by the snap-in; Microsoft Graph enforces its own per-request limits |
| Maximum attachments per email | 10 files |
| Maximum total attachment size | 25 MB |
| Blocked file types | `.eml` (to prevent mail loops) |
| HTTP timeout per request | 180 seconds |
| Attachment upload chunk size | 4 MB per chunk |

> **Large attachment note:** When total attachment size is 3 MB or more, the snap-in uses the Microsoft Graph draft-and-upload flow. This requires the `Mail.ReadWrite` application permission in addition to `Mail.Send`. If that permission is missing, the step fails with a permission error.

---

## Troubleshooting

| Symptom | Likely cause | Resolution |
| --- | --- | --- |
| **Success: false** — `invalid_client` or `unauthorized_client` | Incorrect Client ID, Client Secret, or Tenant ID in the keyring. | Re-enter the keyring credentials from the Azure AD app registration. |
| **Success: false** — `Insufficient privileges` | `Mail.Send` or `Mail.ReadWrite` permission is missing or admin consent was not granted. | Add the required permissions and grant admin consent in the Entra admin center. |
| **Success: false** — `MailboxNotEnabledForRESTAPI` | The sender mailbox is a resource mailbox type not supported by Graph, or the mailbox does not exist in the tenant. | Use a user mailbox or a standard shared mailbox. Verify the UPN in Microsoft 365 admin. |
| **Success: false** — `.eml attachments are not allowed` | An `.eml` artifact was included in the **Attachments** field. | Remove the `.eml` artifact. Use a different file type for the attachment. |
| **Success: false** — attachment size limit exceeded | Total artifact size exceeds 25 MB. | Reduce the number or size of attached artifacts. Consider sharing files via a link instead. |
| Email arrives in spam | The sending domain lacks SPF/DKIM records, or the sender mailbox is new. | Work with your IT team to configure SPF and DKIM for the sending domain. |

---

## Best practices

* **Use a dedicated shared mailbox** for automated emails (for example, `notifications@yourdomain.com`). This keeps automated mail separate from personal inboxes and makes it easy to monitor.
* **Set Client Secret expiry reminders.** Azure AD client secrets expire. When a secret expires, the snap-in fails with an authentication error. Rotate secrets before they expire and update the DevRev keyring immediately.
* **Grant only the permissions you need.** If your workflows never send attachments larger than 3 MB, you only need `Mail.Send`. Add `Mail.ReadWrite` only when large attachments are required.
* **Use workflow variables for personalization.** Dynamic subjects and bodies improve recipient engagement and reduce the need for multiple similar workflow steps.
* **Handle the Success output.** Always connect the **Success** output to a downstream step so your workflow can react to failures gracefully — for example, by creating a follow-up task or sending an alert to your team.
* **Test in a non-production workflow first.** Before rolling out to customers, run the step with a test recipient to confirm credentials, formatting, and attachments all work as expected.

## Source
- DevRev support article [Outlook Email](https://support.devrev.ai/en-US/devrev/article/724unkqM) (ART-30343)
