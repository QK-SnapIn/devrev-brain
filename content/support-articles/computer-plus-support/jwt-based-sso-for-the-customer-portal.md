---
title: JWT-based SSO for the customer portal
devrev_id: ART-27338
parent_directory: Customer portal
translation_group: N3bhguFi
modified_date: "2026-03-27T01:26:19.082Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/N3bhguFi"
tags: []
top_category: Computer+ Support
wiki_match: features/customer-portal
match_score: 0.85
last_updated: 2026-05-11
related: ['features/customer-portal']
summary: "The customer portal supports three login methods: email OTP, JWT-based SSO, and federated SSO (SAML/OIDC via providers such as Okta or Azure AD)."
---

# JWT-based SSO for the customer portal

The [[features/customer-portal|customer portal]] supports three login methods: email OTP, JWT-based SSO, and federated SSO (SAML/OIDC via providers such as Okta or Azure AD). This [[entities/article|article]] covers the **JWT-based SSO** implementation flow. For an overview of all login methods, see the [[support-articles/computer-plus-support/customer-portal-setup-and-administration|Customer Portal Overview]].

## Prerequisites

Before implementing JWT-based SSO, ensure the following are in place:

1. **SSO activation**: Contact DevRev Support to enable JWT-based SSO for your customer portal. You must provide a valid redirect URL where customers are directed when they initiate login.
2. **Application Access Token (AAT)**: Obtain an AAT for your workspace. The AAT authenticates your server's calls to the DevRev Auth Service.
3. **[[features/identity|Identity]] provider (IdP)**: Have an identity provider configured to authenticate your customers and return user traits (such as email and display name).

## Authentication flow

1. A customer clicks **Log in** on your customer portal. The portal redirects the customer to your SSO redirect URL (configured during activation).
2. On the redirected page, authenticate the customer with your identity provider (IdP) and retrieve their user traits.
3. From your server, call the DevRev `auth-tokens.create` endpoint to exchange the user traits for a one-time token.
4. Redirect the customer to the portal callback URL, including the one-time token as a query parameter. The portal exchanges this one-time token for a session token and logs the customer in.

   Use the following callback URL format:

   ```
   https://support.devrev.ai/<your-org-slug>/callback/sso?jwt=<onetime-token>
   ```

   If your portal uses a custom domain, replace `support.devrev.ai/<your-org-slug>` with your custom domain:

   ```
   https://<your-custom-domain>/callback/sso?jwt=<onetime-token>
   ```
5. To redirect the customer to a specific page after login instead of the default landing page, append the `redirect_to` parameter with a relative path:

   ```
   https://support.devrev.ai/<your-org-slug>/callback/sso?jwt=<onetime-token>&redirect_to=/article/ART-1
   ```

   This logs the customer in and redirects them to `https://support.devrev.ai/<your-org-slug>/article/ART-1`.

## Issue a one-time token

Call the [`auth-tokens.create`](https://developer.devrev.ai/api-reference/auth-tokens/create) endpoint from your server to obtain a one-time token. Authenticate the request with your AAT.

**Required fields:**

* `email`: The customer's email address.

**Optional fields:**

* `display_name`: The customer's display name.
* `external_ref`: An external identifier for the customer in your system.

**Example request:**

```
curl -X POST https://api.devrev.ai/auth-tokens.create \
  -H "Authorization: Bearer <your-AAT>" \
  -H "Content-Type: application/json" \
  -d '{
    "email": "customer@example.com",
    "display_name": "Jane Doe",
    "external_ref": "ext-12345"
  }'
```

The response contains a `token` field with the one-time token to use in the callback URL.

## Automatic user provisioning

When you exchange user traits for a one-time token, DevRev automatically provisions the customer if they do not already exist. A new customer record is created with the traits you provided, and the one-time token is generated for the new [[entities/account|account]]. This just-in-time (JIT) provisioning eliminates the need to pre-create customer [[features/accounts|accounts]].

## One-time token security

The one-time token mitigates security risks associated with JWT-based authentication tokens exposed in URLs, including [token impersonation](https://medium.com/@talsec/protecting-your-api-from-app-impersonation-token-hijacking-guide-and-mitigation-of-jwt-theft-48e744b76327) and [replay attacks](https://auth0.com/docs/secure/security-guidance/prevent-threats).

**Short-lived session**

The token expires 5 minutes after issuance. You must redirect the customer to the portal callback URL within this window. If the token expires, request a new one.

**Guaranteed one-time exchange**

The portal accepts the one-time token exactly once and exchanges it for an authenticated session token. Any attempt to reuse the token results in a denied request, and any previously authenticated session associated with that token may be revoked.

## Troubleshooting

* **[[entities/issue|Issue]]**: The customer sees a 403 error after being redirected to the portal.

  **Solution**: Verify that your AAT is valid and has the correct scopes. Confirm the email address in the token request matches an allowed domain for your portal. If the token has already been exchanged, request a new one.
* **Issue**: The one-time token is expired or invalid (`invalid_token` or `token_expired` error).

  **Solution**: One-time tokens expire after 5 minutes. Ensure the redirect happens promptly after token issuance. Request a new token and retry the redirect.
* **Issue**: The customer is redirected but the login does not complete (invalid state error).

  **Solution**: Confirm the callback URL matches the format `https://support.devrev.ai/<your-org-slug>/callback/sso?jwt=<token>` exactly. If you use a custom domain, ensure the domain is registered with DevRev Support. Do not alter the query parameter name or URL path.
* **Issue**: A previously authenticated session is unexpectedly revoked.

  **Solution**: This occurs when a one-time token is reused. Each token is valid for a single exchange. Ensure your application does not cache or retry the callback URL with the same token.

## Related wiki nodes
- [[features/customer-portal]]

## Source
- DevRev support article [JWT-based SSO for the customer portal](https://support.devrev.ai/en-US/devrev/article/N3bhguFi) (ART-27338)
