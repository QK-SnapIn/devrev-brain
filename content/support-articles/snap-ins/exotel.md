---
title: Exotel
devrev_id: ART-21977
parent_directory: Integrate
translation_group: e71SC9Cp
modified_date: "2025-12-10T06:57:38.944Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/e71SC9Cp"
tags: []
top_category: Snap-ins
wiki_match: glossary/ola
match_score: 0.444
last_updated: 2026-05-11
summary: "With the aim of having a single source of truth for all customer problems, DevRev has integrated with Exotel so as to record the customer support requests raised via phone."
---

# Exotel

With the aim of having a single source of truth for all customer problems, DevRev has integrated with Exotel so as to record the customer support requests raised via phone. Customers can now raise their concerns by calling the provided support number on Exotel. Each call creates a record associated with the caller contact, enabling the support team to maintain a complete context of the customer's problem.

For more information, refer to the [Exotel snap-in](https://marketplace.devrev.ai/exotel) on the DevRev marketplace.

## Prerequisites

1. Sign up for an Exotel [[entities/account|account]].
2. Verify your account through phone or email.
3. Get your account KYC verified.
4. Purchase ExoPhone.

## Installing the Exotel Integration snap-in

1. Install the Exotel Integration snap-in from the DevRev marketplace.
2. Select the workspace to install the snap-in, confirm installation, and click **Deploy**.

### Exotel setup guidelines:

1. [Invite co-workers](https://support.exotel.com/support/solutions/articles/144565-how-do-i-add-a-user-or-co-worker-or-employee-#:~:text=Exotel%20Support%20Center,-Welcome&text=Login%20to%20your%20Exotel%20account,access%20rights%20is%20provided%20here.) and add them to the [group](https://support.exotel.com/support/solutions/articles/35147-how-do-i-create-a-group-) responsible for call-based support.
2. Create the required [call flow](https://support.exotel.com/support/solutions/articles/35140-how-do-i-create-edit-save-a-flow-). Greetings, IVR, and routing can be set up here. Add the DevRev URL from the Exotel Integration snap-in in the passthru applet added in this flow.
3. [Associate the call flow](https://support.exotel.com/support/solutions/articles/3000019845-how-do-i-assign-an-existing-number-to-an-app-or-how-do-i-edit-the-number-associated-with-an-app-) to the required Exophone.

When merging duplicate contacts, set the Exotel-created contact as
primary to retain call records

## Source
- DevRev support [[entities/article|article]] [Exotel](https://support.devrev.ai/en-US/devrev/article/e71SC9Cp) (ART-21977)
