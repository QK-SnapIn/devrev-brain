---
title: Twilio
devrev_id: ART-21987
parent_directory: Integrate
translation_group: GHRmPPZJ
modified_date: "2026-02-10T09:58:08.38Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/GHRmPPZJ"
tags: []
top_category: Snap-ins
wiki_match: glossary/trails
match_score: 0.5
last_updated: 2026-05-11
summary: "With the aim of having a single source of truth for all customer problems, DevRev has integrated with Twilio so as to record the customer support requests raised via phone."
---

# Twilio

With the aim of having a single source of truth for all customer problems, DevRev has integrated with Twilio so as to record the customer support requests raised via phone. Customers can now raise their concerns by calling the provided support number on Twilio. Each call creates a support [[entities/ticket|ticket]] with the call recording, caller [[features/identity|identity]], and call transcript, enabling the support team to maintain a complete context of the customer's problem.

## Prerequisites

* Ensure you have a Twilio [[entities/account|account]].

  If you would like to provide live call support, you need a Twilio Flex account. If voice notes are adequate for your business requirements, a Twilio account suffices.
* Configure the required [IVR](https://www.twilio.com/docs/flex/admin-guide/tutorials/ivr) on Twilio.
* Obtain [Twilio account SID](https://help.twilio.com/articles/14726256820123-What-is-a-Twilio-Account-SID-and-where-can-I-find-it-) and the authentication token. These details can be found on the **Twilio Console dashboard** under **Account Info**.

## Installing the Twilio snap-in

1. Install the [Twilio](https://marketplace.devrev.ai/twilio) snap-in from the DevRev marketplace.
2. Select the workspace to install the snap-in, confirm installation, and click **Deploy snap-in**.

## Set up the Twilio snap-in

Follow these steps to ensure that the customer calls received via Twilio are synced with DevRev [[features/tickets|tickets]].

1. On the **Snap-ins** > **Connections** tab, either add an existing connection or create a new connection by clicking **+ Connection** and providing a name.
2. Provide the **Twilio account SID** and the **authentication token**.
3. In the **Configurations** tab, fill in the following details:

* Phone number to sync the records of the calls received with DevRev tickets.
* Select the default [[entities/part|part]] that will be assigned to the tickets that are created by calls received on the configured phone number. You can also select the stages of the created tickets for different use cases.

## Source
- DevRev support [[entities/article|article]] [Twilio](https://support.devrev.ai/en-US/devrev/article/GHRmPPZJ) (ART-21987)
