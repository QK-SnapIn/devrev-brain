---
title: External identity provider setup
devrev_id: ART-21858
parent_directory: Access control
translation_group: zEOt0tAE
modified_date: "2026-02-18T22:27:18.188Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/zEOt0tAE"
tags: []
top_category: Computer by DevRev
wiki_match: features/identity
match_score: 0.85
last_updated: 2026-05-11
related: ['features/identity']
summary: "DevRev can be configured to use external identity providers for SSO."
---

# External identity provider setup

DevRev can be configured to use external [[features/identity|identity]] providers for SSO.

If you want DevRev to use an external identity provider, follow the instructions for your organization’s provider.

## Before you begin

To register DevRev as a SAML 2.0 application, you need the slug for your dev org.

To get the `dev_oid` and `slug`, run the following command:

```
curl --location --request GET 'https://api.devrev.ai/internal/dev-orgs.self.get' \
--header 'Authorization: <your PAT>'
```

In the response, the `dev_oid` is returned as the `display_id`.

Ensure the `connection_name` combines the `dev_oid` prefix with a custom string and matches the regex pattern:

```
^`[a-zA-Z0-9]`(-`[a-zA-Z0-9]`|`[a-zA-Z0-9]`)*$
```

This means it must:

* Start with an alphanumeric character.
* Contain alphanumeric characters or hyphens, without consecutive or trailing hyphens.
* Be unique within your organization.
* Follow the pattern of: `<dev_oid>-<CUSTOM-STRING>`.

The API call to create the connection fails if this pattern is not followed.

## Setup DevRev as service provider on identity provider

You can register DevRev as a service provider in any identity provider that supports SAML 2.0 or OpenID Connect (OIDC). The following are some common examples:

## Azure AD

1. Log in to Azure Active Directory and select **Enterprise applications > + New application**.
2. [[features/search|Search]] for "Azure AD SAML Toolkit" in the **Browse Azure AD Gallery** and select it.
3. Enter `DevRev` as the name and click **Create**.
4. Select **Single sign-on > SAML**.
5. Edit the **Basic SAML Configuration** and enter the following parameters.

   * **Identifier** (Entity ID): `urn:auth0:tf-devrev-prod:<connection_name>`
   * **Reply URL** (Assertion Consumer Service URL): `https://auth.devrev.ai/login/callback?connection=<connection_name>`
   * **Sign on URL**: `https://app.devrev.ai/<DEV_ORG_SLUG>`

   The `<connection_name>` must be the same in both parameters and follow the naming pattern described earlier.
6. Go to **Copy > SAML Certificates** and save the **App Federation Metadata URL**.
7. In the Azure portal, go to the application named "DevRev" that you created earlier under Enterprise applications. Within the application, go to **Users and [[entities/group|Groups]]** and assign the users who can access the app.

## Google Workspace

1. Log in to Google Workspace as an admin.
2. Select **Apps > Web and mobile apps > Add app > Add custom SAML app**.
3. Enter `DevRev` as the name of the app.
4. On the next screen, select **Download IdP metadata** then **Continue**.
5. Enter the following parameters.

   * **ACS URL**: `https://auth.devrev.ai/login/callback?connection=<connection_name>`
   * **Entity ID**: `urn:auth0:tf-devrev-prod:<connection_name>`
   * **Name ID format**: *Email*
   * **Name ID**: *Basic Information > Primary Email*

   The `<connection_name>` must be the same in both parameters and follow the naming pattern described earlier.

## Jump Cloud

1. Log in to the JumpCloud Administrator Console and go to **User Authentication > SSO > + Add New Application**.
2. Search for "Auth0" then click **Configure**.
3. Enter `DevRev` in **General Info > Display Label**.
4. Enter the following parameters.

   * **YOURTENANTDOMAIN**: `https://auth.devrev.ai/login/callback?connection=<connection_name>`
   * **TEAMNAME**: `<DEV_ORG_SLUG>`
5. Click **Activate** and then **Continue** in the confirmation window.
6. Click **Download Certificate** in the top left of the window.
7. Find **Auth0** in the application list on the SSO page and click anywhere in the row to reopen the application configuration panel.
8. Select the **SSO** tab and copy the **IdP URL**.

Leave the Admin Portal open.

## Okta

1. Log in to Okta as an admin and go to **Applications** > **Applications > Create App Integration** > **SAML 2.0**.
2. Complete the **General Settings**.
3. Enter the following parameters.

   * **Single sign-on URL**: `https://auth.devrev.ai/login/callback?connection=<connection_name>`
   * **Audience URI** (SP Entity ID): `urn:auth0:tf-devrev-prod:<connection_name>`
   * **Name ID format**: *EmailAddress*
   * **Application Username**: *Email*
   * **Feedback**: *I'm an Okta customer adding an internal app*
   * **App Type**: *This is an internal app that we have created*

   The `<connection_name>` must be the same in both parameters and follow the naming pattern described earlier.
4. Copy the metadata URL under **Sign On** > **Settings**> **SAML 2.0** and share with the DevRev customer success team.

## Configure DevRev to use your identity provider

After registering DevRev as an application in your identity provider, you need to create an authentication connection in DevRev that links to your identity provider. This connection enables DevRev to authenticate users through your external identity provider.

Before proceeding, ensure you have the following:

* A Personal Access Token (PAT) with admin permissions.
* Connection details from your identity provider setup.
* Your `dev_oid` and organization slug from the previous steps.

### Step 1: Create the authentication connection

An authentication connection is a configuration object that tells DevRev how to communicate with your identity provider. Use the [auth connections create API](https://developer.devrev.ai/public/api-reference/auth-connections/dev-org-auth-connections-create) to create this connection.

Choose the appropriate protocol based on your identity provider:

## SAML 2.0

**For SAML-based identity providers (Azure AD, Okta, etc.):**

```
curl --location --request POST 'https://api.devrev.ai/dev-orgs.auth-connections.create' \
--header 'Authorization: Bearer <your PAT>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "type": "samlp",
  "sign_in_endpoint": "<sign_in_endpoint>",
  "signing_cert": "<signing_cert>",
  "connection_name": "<connection_name>",
  "display_name": "<display_name>"
}'
```

**Expected successful response:**

```
{
  "auth_connection": {
    "id": "con_12345678",
    "display_name": "<display_name>",
    "enabled": false,
    "type": "samlp",
    "sign_in_endpoint": "<sign_in_endpoint>",
    "connection_name": "<connection_name>",
  }
}
```

## OpenID Connect

**For OIDC-based identity providers:**

```
curl --location --request POST 'https://api.devrev.ai/dev-orgs.auth-connections.create' \
--header 'Authorization: Bearer <your PAT>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "display_name": "<display_name>",
    "type": "oidc",
    "client_id": "<client_id>",
    "client_secret": "<client_secret>",
    "issuer": "<issuer>"
}'
```

**Expected successful response:**

```
{
  "auth_connection": {
    "id": "con_12345678",
    "display_name": "<display_name>",
    "enabled": false,
    "type": "oidc",
    "client_id": "<client_id>",
    "issuer": "<issuer>"
  }
}
```

Important

* The `connection_name` must follow the naming pattern described earlier.
* Save the `id` field from the response—you need it for the next step.
* The connection is created with `enabled: false` by default for security.

### Step 2: Enable the authentication connection

After successfully creating the connection, enable it using the connection ID from the previous response:

```
curl --location --request POST 'https://api.devrev.ai/dev-orgs.auth-connections.toggle' \
--header 'Authorization: Bearer <your PAT>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "id": "<CONNECTION_ID>",
  "toggle": "enable"
}'
```

**Expected successful response:**

```
{}
```

### Step 3: Test and verify the setup

Follow these steps to ensure your SSO integration is working correctly:

1. **Check the login page:**

   * Go to: `https://app.devrev.ai/<DEV_ORG_SLUG>`
   * You should see a new SSO login option with your identity provider's name
2. **Test user authentication:**

   * Use a test user [[entities/account|account]] that's assigned to the DevRev application in your identity provider
   * Click the SSO login option and complete the authentication flow
   * Verify the user is successfully logged into DevRev
3. **Test edge cases:**

   * Try logging in with a user not assigned to the DevRev application (should fail)
   * Test logout functionality
   * Verify session timeout behavior

* Start with a test user account before rolling out to all users.
* Test both successful and failed authentication scenarios.

### Step 4: Manage authentication methods (Optional)

After successfully enabling SSO, you can disable other authentication methods to enforce SSO-only login. This is commonly done to ensure all users authenticate through your organization's identity provider.

**Common scenario**: If users were previously logging in with Google OAuth and you've now enabled SSO, you can disable Google authentication to force all users to use SSO.

First, get the Google OAuth connection ID:

```
curl --location --request GET 'https://api.devrev.ai/dev-orgs.auth-connections.list' \
--header 'Authorization: Bearer <your PAT>'
```

Look for the Google OAuth connection in the response and note its `id` field.

Disable Google authentication:

```
curl --location --request POST 'https://api.devrev.ai/dev-orgs.auth-connections.toggle' \
--header 'Authorization: Bearer <your PAT>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "id": "<GOOGLE_OAUTH_CONNECTION_ID>",
  "toggle": "disable"
}'
```

Important considerations: When disabling other authentication methods:

* **Test SSO first**: Ensure SSO is working correctly before disabling alternatives.
* **Admin access**: Make sure at least one admin can access the system via SSO.

## IDP initiated SSO (Optional)

DevRev supports SP-initiated SSO, which means users always start the authentication process from DevRev. IDP initiated SSO means users start the authentication process from your identity provider's portal. The latter is not supported on DevRev.

A workaround for supporting IDP-initiated SSO is to bookmark your DevRev workspace URL (that is `https://app.devrev.ai/<DEV_ORG_SLUG>`) in your IDP. With only SSO Auth connection enabled, the experience would be as seamless as SP-initiated SSO.

### Parameter reference

* `<your PAT>`: Your Personal Access Token with admin permissions
* `<dev_oid>`: Your DevRev organization ID (from the initial API call)
* `<CUSTOM-STRING>`: A custom identifier you choose (must be consistent across all configurations)
* `<connection_name>`: A unique identifier for your connection (must follow the naming pattern)
* `<display_name>`: A human-readable name for your connection
* `<DEV_ORG_SLUG>`: Your DevRev organization slug
* `<CONNECTION_ID>`: The ID returned from the connection creation API call

## Troubleshooting

If you encounter [[features/issues|issues]]:

1. **Authentication endpoint errors**: Verify the `sign_in_endpoint` (SAML) or `issuer` (OIDC) is accessible and returns valid responses.
2. **Login failures**: Check that users are assigned to the application in your identity provider.

For additional support, contact the DevRev customer success team with your connection details and error messages.

## Related wiki nodes
- [[features/identity]]

## Source
- DevRev support [[entities/article|article]] [External identity provider setup](https://support.devrev.ai/en-US/devrev/article/zEOt0tAE) (ART-21858)
