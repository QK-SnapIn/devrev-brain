---
title: Federated identity provider setup for the customer portal
devrev_id: ART-23825
parent_directory: Customer portal
translation_group: Tkwo2Ncm
modified_date: "2026-03-27T18:07:54.792Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Tkwo2Ncm"
tags: []
top_category: Computer+ Support
wiki_match: features/identity
match_score: 0.85
last_updated: 2026-05-11
related: ['features/identity']
summary: "The DevRev customer portal supports three login methods: email OTP, JWT-based SSO, and federated identity provider SSO."
---

# Federated identity provider setup for the customer portal

The DevRev [[features/customer-portal|customer portal]] supports three login methods: email OTP, [[support-articles/computer-plus-support/jwt-based-sso-for-the-customer-portal|JWT-based SSO]], and federated [[features/identity|identity]] provider SSO. Federated SSO delegates authentication to your organization's SAML-based identity provider. If your organization uses a centralized identity provider, the federated model requires less setup than JWT-based SSO. For an overview of customer portal login methods, see [[support-articles/computer-plus-support/customer-portal-setup-and-administration|Customer portal overview]].

> 📝 **Note**: This [[entities/article|article]] covers federated SSO for the **customer portal** only. To configure an external identity provider for the DevRev app itself, see [[support-articles/computer-by-devrev/external-identity-provider-setup|External identity provider setup]].

## Before you begin

Before configuring federated login, ensure you have the following:

* **Admin access to your DevRev workspace.** You must be a workspace administrator to update portal authentication preferences.
* **A personal access token (PAT).** Generate a PAT from [Settings > Account > Personal Access Tokens](https://app.devrev.ai/?setting=account) in the DevRev app. Replace `DEV_ORG_SLUG` in the URL `https://app.devrev.ai/DEV_ORG_SLUG/settings/account` with your workspace slug.
* **Your workspace slug** `DEV_ORG_SLUG`)**.** This is the short identifier for your workspace, visible in the DevRev app URL (for example, `https://app.devrev.ai/example`).
* **Your workspace [[glossary/don|DON]]** (`DEV_ORG_DON`)**.** Obtain this value by calling the following endpoint, replacing `DEV_ORG_SLUG` with your workspace slug:

  ```
  https://api.devrev.ai/internal/dev-orgs.public-info.get?slug=DEV_ORG_SLUG
  ```

  The response is a JSON message containing the `DEV_ORG_DON` value in the `id` attribute:

  ```
  {
    "auth0_org_id": "XXXXXXX",
    "dev_slug": "example",
    "id": "don:identity:dvrv-us-1:devo/iP3bd1RS",
    "id_v1": "XXXXXXX"
  }
  ```
* Admin access to your identity provider (Azure AD, Google Workspace, JumpCloud, or Okta).

## Configure federated login

1. Create a SAML application in your identity provider representing the DevRev customer portal. See the identity provider-specific sections below for detailed steps.
2. File a support [[entities/ticket|ticket]] at [DevRev support](https://support.devrev.ai) with the SAML metadata, downloaded certificate, or IdP URL. Include your workspace slug and the identity provider you are using in the ticket body.
3. Once support has made the required configuration, run the following cURL command to enable federated login for your customer portal, replacing `$PAT`, `DEV_ORG_SLUG`, and `DEV_ORG_DON` with your values:

   ```
   curl -v --location --request POST 'https://api.devrev.ai/internal/preferences.update' \
      --header "Authorization: $PAT" \
      --header 'Content-Type: application/json' \
      --data-raw '{
        "auth": {
          "login_method": "federated",
          "connection_name": "saml|<DEV_ORG_SLUG>"
        },
        "type": "portal_preferences",
        "object": "<DEV_ORG_DON>"
      }'
   ```

   A successful response returns a JSON object confirming the updated preferences with `login_method` as `federated`.

## JIT provisioning

Just-in-time (JIT) provisioning automatically creates customer [[features/accounts|accounts]] in your DevRev workspace when a user logs in through the federated identity provider for the first time. The customer's workspace domain defaults to their email domain. This eliminates the need to pre-create customer accounts manually.

To enable JIT provisioning, run the following cURL command:

```
curl -v --location --request POST 'https://api.devrev.ai/internal/preferences.update' \
--header "Authorization: $PAT" \
--header 'Content-Type: application/json' \
--data-raw '{
  "auth": {
    "jit_rev_user_provisioning": "all"
  },
  "type": "portal_preferences",
  "object": "<DEV_ORG_DON>"
}'
```

A successful response returns a JSON object confirming that `jit_rev_user_provisioning` is set to `all`.

## Reset to default authentication

If you need to revert from federated login to the default email OTP authentication method – for example, if your identity provider is temporarily unavailable, or if you are switching to a different login method – run the following cURL command:

```
curl -v --location --request POST 'https://api.devrev.ai/internal/preferences.update' \
--header "Authorization: $PAT" \
--header 'Content-Type: application/json' \
--data-raw '{
  "auth": {
    "login_method": "default"
  },
  "type": "portal_preferences",
  "object": "DEV_ORG_DON"
}'
```

A successful response returns a JSON object confirming that `login_method` is set to `default`. After resetting, customers log in with email OTP.

## Azure AD

1. Log in to Azure Active Directory, select **Enterprise applications > + New application**, [[features/search|search]] for **Azure AD SAML Toolkit** in the gallery, and select it.
2. Enter **DevRev** as the name and click **Create**.
3. Select **Single sign-on > SAML** and edit the **Basic SAML Configuration** with the following parameters:

   * **Identifier (Entity ID)**: `urn:auth0:revportal-prod:DEV_ORG_SLUG`
   * **Reply URL (Assertion Consumer Service URL)**: `https://rev.auth.devrev.ai/login/callback?connection=DEV_ORG_SLUG`
   * **Sign on URL**: `https://support.devrev.ai/DEV_ORG_SLUG`
4. Under the **SAML Certificates** section, copy the **App Federation Metadata URL** and share it with the DevRev team by filing a support ticket at [DevRev support](https://support.devrev.ai). ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/12734202&key=e54f8559f998fcd2eae2f3c3ed6ef72d5b94cfc0d92632ed5c7eacaca9d9c177)
5. In the Azure portal, go to the **DevRev** application under **Enterprise applications**, select **Users and [[entities/group|Groups]]**, and assign the users who can access the customer portal.

## Google Workspace

1. Log in to Google Workspace as an admin, then select **Apps > Web and mobile apps > Add app > Add custom SAML app**.
2. Enter **DevRev** as the name of the app.
3. On the next screen, select **Download IdP metadata** and then click **Continue**.
4. Enter the following parameters:

   * **ACS URL**: `https://rev.auth.devrev.ai/login/callback?connection=DEV_ORG_SLUG`
   * **Entity ID**: `urn:auth0:revportal-prod:DEV_ORG_SLUG`
   * **Name ID format**: Email
   * **Name ID**: Basic Information > Primary Email
5. Click **Finish** to save and create the SAML app.
6. On the app details page, set **User access** to **ON for everyone** (or restrict to specific organizational units as needed) and click **Save**.
7. Share the downloaded IdP metadata file with the DevRev team by filing a support ticket at [DevRev support](https://support.devrev.ai).

## JumpCloud

1. Log in to the JumpCloud Administrator Console, go to **User Authentication > SSO > + Add New Application**, search for **Auth0**, and click **Configure**.
2. Enter **DevRev** in **General Info > Display Label**.
3. Enter the following parameters:

   * <YOURTENANTDOMAIN>: `https://rev.auth.devrev.ai/login/callback?connection=DEV_ORG_SLUG`
   * <TEAMNAME>: `DEV_ORG_SLUG`
4. Click **Activate** and then **Continue** in the confirmation window.
5. Click **Download Certificate** in the top left of the window.
6. Find **Auth0** in the application list on the SSO page and click anywhere in the row to reopen the application configuration panel.
7. Select the **SSO** tab and copy the **IdP URL**.
8. Share the downloaded certificate and the IdP URL with the DevRev team by filing a support ticket at [DevRev support](https://support.devrev.ai). Include your workspace slug in the ticket.

## Okta

1. Log in to Okta as an admin, go to **Applications > Applications > Create App Integration > SAML 2.0**, and complete the **General Settings**.
2. Enter the following parameters:

   * **Single sign-on URL**: `https://rev.auth.devrev.ai/login/callback?connection=DEV_ORG_SLUG`
   * **Audience URI (SP Entity ID)**: `urn:auth0:revportal-prod:DEV_ORG_SLUG`
   * **Name ID format**: EmailAddress
   * **Application Username**: Email
3. Under **Sign On > Settings > SAML 2.0**, copy the **metadata URL** and share it with the DevRev support team by filing a support ticket at [DevRev support](https://support.devrev.ai). ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/12734229&key=28a4f3d81ddd3bd49a275be2de4439ed4d1d6933064f77b99b9a166ce49782cd)

## Verify federated login

After the DevRev team confirms the connection is active and you have enabled federated login with the cURL command, verify the setup:

1. Open your customer portal URL (`https://support.devrev.ai/DEV_ORG_SLUG`) in an incognito or private browser window.
2. Click **Sign in**. The portal redirects you to your identity provider's login page instead of showing the email OTP screen.
3. Authenticate with a test user who is assigned to the SAML application in your identity provider. After successful authentication, the portal redirects you back and displays the customer portal home page.
4. If JIT provisioning is enabled, confirm that the test user's customer [[entities/account|account]] was automatically created in your DevRev workspace by checking **Customers** in the DevRev app.

If the login does not redirect to your identity provider, or if an error occurs, see the troubleshooting section below.

## Troubleshooting

* **[[entities/issue|Issue]]**: The customer portal shows the default email OTP login screen instead of redirecting to the identity provider.

  **Solution**: Verify that the cURL command to enable federated login returned a successful response with `"login_method": "federated"`. Ensure the `connection_name` matches the value provided by the DevRev team. Re-run the cURL command if necessary.
* **Issue**: The identity provider returns an error after the portal redirects (for example, "invalid ACS URL" or "unknown service provider").

  **Solution**: Confirm that the **ACS URL** and **Entity ID** configured in your identity provider exactly match the values expected by DevRev. Contact [DevRev support](https://support.devrev.ai) to verify the correct values for your workspace.
* **Issue**: Authentication succeeds at the identity provider, but the portal displays an error or does not load.

  **Solution**: Ensure the DevRev team has completed the connection setup on their end. File a support ticket at [DevRev support](https://support.devrev.ai) with the error details and your workspace slug.
* **Issue**: JIT provisioning is enabled but new users are not being created automatically.

  **Solution**: Verify that the JIT provisioning cURL command returned a successful response with `"jit_rev_user_provisioning": "all"`. Ensure the user's email domain is correct and that the SAML assertion includes the user's email address as the Name ID.
* **Issue**: Users who were previously able to log in with email OTP can no longer access the portal after enabling federated login.

  **Solution**: Once federated login is enabled, all portal users must authenticate through the identity provider. Ensure all portal users are assigned to the SAML application in your identity provider.

## Related wiki nodes
- [[features/identity]]

## Source
- DevRev support article [Federated identity provider setup for the customer portal](https://support.devrev.ai/en-US/devrev/article/Tkwo2Ncm) (ART-23825)
