---
title: November 2025
devrev_id: ART-21884
parent_directory: Changelog
translation_group: pqon0Q2m
modified_date: "2026-04-24T15:27:42.962Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/pqon0Q2m"
tags: []
top_category: Changelog
wiki_match: features/commerce
match_score: 0.381
last_updated: 2026-05-11
---

# November 2025

![build-part.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108115&key=c9a66767d1039a97d202b9708746d6d887211db5fe45e8f244d723b7b7396dc7)

### Build App

* **Enhanced Sprint Board Navigation**

  Access sprint boards directly using the **Cmd + K** search, bypassing the need to select views. This update simplifies navigation and streamlines the workflow based on user feedback.
* The current sprint view now shows all assigned issues on initial load, so there's no need to navigate away and back.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4107994&key=ab7b128b7fe54c50f424c1fd262ac68c4f057106f227c84243bea1ae1710ead6) For more information about *Build App*, refer to the following articles: [Sprint mode](https://app.devrev.ai/devrev/settings/knowledge-base/articles/ART-21872)

![chat.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108196&key=bd83d7afde18015a08e1d5c8ce390c7d1fc3e5d923b17e68270ed9b794cd2d88)

### Channels

* **Telephony Support via Amazon Connect on DevRev**

  We're thrilled to introduce voice call support on DevRev through AWS Connect, allowing faster and more direct query resolution compared to text-based communication.

  **New features:**

  + **Inbound call support:** Receive incoming calls directly on DevRev powered by AWS Connect, offering a new voice channel for customer support.
  + **Outbound call support:** Agents can initiate outgoing calls to customers via DevRev.
  + **Identity mapping:** DevUser and RevUser identities are now mapped between AWS Connect and DevRev for smooth call routing and user identification.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108012&key=7f57d650058837e3dd7e01a2b6fab177e2f5b6bfa7f80484fc25ae3ebaca7d1e) For more information about *Channels*, refer to the following article: [[support-articles/snap-ins/exotel|Exotel]]

![cube.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108259&key=7fe69f908ee5de8ae2e80fa5382f148797b870a19374ab38445af3d80fe38645)

### Data-UI Platform

**Enhanced Bar Chart User Readability**

Bar charts now display user names as labels for quick identification of issue owners, improving data readability.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108028&key=b598030343abfa79eeca9bb7ecef5d2b2e7a8b388d6bded689e827328b5d18f2) For more information about *Vistas*, refer to the following articles: [[support-articles/computer-by-devrev/vistas|Vistas]]

![cube.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108350&key=35da23de2a9a21c3ea0b5fdaedc5f91bc3428e350f91ff7c5bcb884ea6ac218b)

### Sprint mode

**Improved Sprint Filter Experience**

We've enhanced the Sprint filter for easier selection. Now, when you choose a sprint, the **Selected** tab activates automatically, allowing immediate access to your chosen sprint board without extra clicks.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108039&key=ad0f3f82a8589474fb59b93a832628051160583c0a61e9f9431218fbd32a030f) For more information about *Sprint mode*, refer to the following articles: ‣ [Smart sprint | Automate | Snap-ins](https://devrev.ai/docs/automations/smart-sprint)

![support-part.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108437&key=668feb861c35d1a51d353a781f7fe46fbca1dd1bb077a8879971d3ebcc65f7b2)

### Support App

**Improvements to Owner and Group Assignment**

* Added a warning when selecting an owner not in the chosen group.
* Automatically sets the owner to **Unassigned** when switching to a group excluding the current owner.

**Description Enhancements**

* **Inline images:** Users can now add inline images directly within descriptions for clearer context.
* **Close button fix:** Resolved issue where images couldn't be closed due to editor mode switching.
* **Text cut-off issue:** Fixed text being cut off after images upon saving.
* **No more duplicates on clone:** Corrected duplicate copying of inline images when cloning.

**Internal Tickets via Workflows**

* Introduced visibility field in workflow nodes for managing a wide range of automations.

**Updates in Macros**

* All fields, irrespective of subtype, can now be selected and updated.
* Macros handle deprecated fields automatically without failures.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108052&key=3082d9db99201410434ad8175cf6638bec5d10edf15e5bd967c2235bc671a395) For more information about *Support App*, refer to the following article: [[support-articles/computer-plus-support/computer-support|Computer for Support Teams]]

![cube.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108508&key=61abad6b5a4105ad15e3072d7d9d155721def1464f82af903aa5abb090a16659)

### Vista

* **Link and ID Copying** Enhancements: Users can now copy links and IDs more easily with improved tooltips and reduced lag.
* **Ticket Number Copy Feature**: A new copy button next to the ticket number allows for quick URL copying.
* **Create List Views Instantly**

  Instantly create list views by clicking **+** in the left navigation. Select an object type, name your view, and optionally select a location to pin it.
* We've enhanced Vista view filtering with operator-based options, including **not-in** conditions for the Stage field, allowing precise exclusion of certain stages. The addition of **any of** and **none of** operators ensures consistent filtering across fields, streamlining workflows and boosting productivity.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/4108066&key=53c9a5ca5627abb0adaaafa9a1682015de8bafc16377b98a134cdfefd58b20a7) For more information about *Vistas*, refer to the following articles: ‣ [[support-articles/computer-by-devrev/vista-reports|Vista reports]] ‣ [[support-articles/computer-by-devrev/vistas|Vistas]]

## Source
- DevRev support article [November 2025](https://support.devrev.ai/en-US/devrev/article/pqon0Q2m) (ART-21884)
