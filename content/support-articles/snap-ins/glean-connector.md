---
title: Glean connector
devrev_id: ART-21988
parent_directory: Integrate
translation_group: _NpOkgmO
modified_date: "2025-12-10T06:57:46.017Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/_NpOkgmO"
tags: []
top_category: Snap-ins
wiki_match: entities/enhancement
match_score: 0.462
last_updated: 2026-05-11
---

# Glean connector

Index your DevRev objects into Glean. This snap-in functions as a connector with Glean, the enterprise search tool, making DevRev objects discoverable and enabling searches using a wide range of filters.

For more information, refer to the [Glean connector snap-in](https://devrev.ai/marketplace/glean-connector) on the DevRev marketplace.

## Installation

1. Create a Glean datasource by following the steps provided under "Option 1: Using the [Glean custom app setup page](https://developers.glean.com/docs/indexing_api/indexing_api_getting_started/#set-up-a-datasource).

   a. Choose a unique name for the datasource.

   b. Select "Published content" as the datasource category.

   c. Enter a display name.

   d. Skip the icon entry, as the snap-in will overwrite it with the DevRev logo for easy recognition.

   e. In the URL regex field, enter: ^<https://app.devrev.ai/>.\*

   f. Ensure the "Email is used to reference users [...]" box is unchecked.

   g. Click the "Publish" button to create the custom app.
2. To enable search results for this new datasource in Glean's UI, follow the steps provided in [Glean documentation](https://developers.glean.com/docs/indexing_api/indexing_api_getting_started/#enable-search-results-for-the-datasource).
3. Create a Glean API token by following the instructions provided in the [Glean documentation](https://developers.glean.com/docs/indexing_api/indexing_api_tokens/). Under **Scopes**, enter the unique name assigned to the datasource in the previous step.
4. In DevRev's marketplace, click **Install** to register the snap-in with your organization.
5. In the DevRev app, set up the connection by navigating to **Settings** > **Snap-ins** > **Connections** at the top.

   * Search and select an existing connection or create a new one by clicking **+ Connection**.
   * Select **Snap-in Secret** from the dowpdown list.
   * Provide a name and enter the API token on the "Secret" input box. Ensure to toggle on **Make public** to share the connection publicly with your organization.

## Configure the snap-in

1. In the **Configuration** tab, select the connection containing Glean's API token that was just created.
2. Enter the datasource unique name, display name, and your Glean's instance name. You can find the latter in the URL when accessing your organization's Glean platform. Enter the value before **-be.glean.com**. For example, if your url is "app.glean.com/some-name-be.glean.com", enter "some-name".
3. Decide which DevRev object types should be indexed and discorevable in Glean. Set the toggles based on your preferences.
4. Determine if there are any custom fields associated with specific object types that should be visible as filters in Glean's UI. While stock fields and object types are automatically enabled as filters, custom fields require their display names for indexing. Add a configuration input for each custom field that needs to be indexed.
5. Save your changes and proceed to install the snap-in. It will run on a schedule, indexing objects into Glean accordingly.

## Source
- DevRev support article [Glean connector](https://support.devrev.ai/en-US/devrev/article/_NpOkgmO) (ART-21988)
