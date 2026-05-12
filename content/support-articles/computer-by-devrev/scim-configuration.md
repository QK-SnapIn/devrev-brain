---
title: SCIM configuration
devrev_id: ART-22503
parent_directory: Access control
translation_group: sPx7s2Wz
modified_date: "2026-04-14T01:52:30.918Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/sPx7s2Wz"
tags: []
top_category: Computer by DevRev
wiki_match: features/side-conversations
match_score: 0.667
last_updated: 2026-05-11
summary: "Provisioning users and groups from Okta to DevRev minimizes the need for manual addition of each employee or group in DevRev, reducing administrative errors, saving time, and ultimately lowering costs."
---

# SCIM configuration

Provisioning users and [[entities/group|groups]] from Okta to DevRev minimizes the need for manual addition of each employee or [[entities/group|group]] in DevRev, reducing administrative errors, saving time, and ultimately lowering costs.

# Features

* **Push new users**: Automatically adds newly created users in Okta to DevRev.
* **Push profile updates**: Seamlessly syncs profile changes from Okta to DevRev.
* **Push user deactivation**: Deactivation or removal of users in Okta disables them in DevRev.
* **Push groups**: Automatically reflects groups created or updated in Okta to DevRev.

# Set up provisioning in Okta

## Prerequisites

* Obtain admin access to the Okta dashboard.
* Obtain admin access to the respective organization in DevRev.
* Ensure SSO is enabled for the organization. For details, see [SSO-SAML documentation](https://devrev.ai/docs/product/sso-saml).

## Configure DevRev SCIM app

1. Log in to Okta as an admin and go to **Applications > Applications**.
2. Select **DevRev SSO/SCIM App** or **SCIM 2.0 Test App** from the catalog.
3. Enter a valid app name, for example, DevRev, and the connection name configured while setting up SSO. Click **Done**.
4. Add the integration and configure the basic details. Click **Done**.
5. Set the application username format as **Email**. This is treated as the `userName` in DevRev.
6. Under the **Provisioning** tab, click on **Configure API Integration** and enable it.
7. Click on **Configure API Integration**.
8. To fetch the API Token, go to **Settings > Security** in your DevRev organization and enable SCIM. Copy the API token value.
9. Paste the copied API token into Okta, test the API credentials, and click **Save** on success.
10. Enable the following options for syncing to the application in Okta:

    * Create Users
    * Update User Attributes
    * Deactivate Users
11. The following fields are supported for the Okta to DevRev sync. Remove others by clicking the cross button.

    ![supported-fields.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/5469666&key=91a8a449850fe1f6befd2a0124d31b7324bcbd426ba7c870809b9aec415f9608)

## Provision users from Okta to DevRev

1. Select the **Assignments** tab.
2. Choose the **Assign** drop-down menu and select **Assign to People**.
3. Enter the name of the user you want to send to DevRev in the **[[features/search|Search]]…** box.
4. Select **Assign**.
5. Enter additional user details if needed. Select **Save and Go Back**.

Provisioned users in Okta will be created in a 'Shadow' state in DevRev. To locate them, go to **Settings > Users**. They become active upon login.

* DevRev uses `userName` as the source of truth, which is a unique identifier within DevRev. An email update in DevRev will reflect as a `userName` change in Okta. Update both email and `userName` simultaneously.
* DevRev treats the display name as a user preference. While it is synced upon initial user creation, subsequent updates from Okta will not modify it, allowing users to retain their preferred display names.

## Provision groups from Okta to DevRev

1. Navigate to the top and click the tab for **Push Groups > Push Groups**.
2. Enter the group name in the **Enter a group to push…** box and select it.
3. Select **Save**.

The provisioned group in Okta will be created in DevRev with associated members. To locate it, go to **Settings > Groups**.

* Import functionality for groups is not currently supported.
* DevRev has a unique constraint on group names, so more than one group cannot have the same name. Click on **Refresh App Groups** before pushing a new group to prevent errors if the group already exists in DevRev.

## Source
- DevRev support [[entities/article|article]] [SCIM configuration](https://support.devrev.ai/en-US/devrev/article/sPx7s2Wz) (ART-22503)
