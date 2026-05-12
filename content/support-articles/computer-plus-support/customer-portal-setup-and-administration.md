---
title: Customer portal setup and administration
devrev_id: ART-21864
parent_directory: Customer portal
translation_group: mCD8f9oD
modified_date: "2026-04-16T08:08:03.668Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/mCD8f9oD"
tags: []
top_category: Computer+ Support
wiki_match: features/customer-portal
match_score: 0.85
last_updated: 2026-05-11
related: ['features/customer-portal']
summary: "The customer portal is an online platform that enables your customers to interact with your support team, create support tickets, track the progress of their requests, and engage in conversations related to their issues."
---

# Customer portal setup and administration

The [[features/customer-portal|customer portal]] is an online platform that enables your customers to interact with your support team, create support [[features/tickets|tickets]], track the progress of their requests, and engage in [[features/conversations-feature|conversations]] related to their [[features/issues|issues]]. It serves as a centralized hub for managing customer support inquiries.

The customer portal is available in both web and mobile formats (Android and iOS). It enables end users to access support [[entities/article|articles]], manage tickets, and interact with the support team.

## Benefits

**Enhanced customer experience**

Customers can access self-service options, track their tickets, and receive timely updates, leading to improved satisfaction.

**Efficient [[entities/ticket|ticket]] management**

The portal streamlines ticket creation, assignment, and tracking, ensuring faster resolution times.

**Seamless, timely, and transparent communication**

Customers and support teams can engage in threaded conversations within the portal, eliminating the need for scattered email chains.

**Improved collaboration**

Customer admins can access and manage tickets from their team, enabling seamless collaboration and knowledge sharing.

## Features

**Ticket creation, tracking, and team collaboration**

Customers create tickets with relevant details such as [[entities/issue|issue]] description, priority, and category. To create a ticket, go to **+ Ticket**, enter a title and description, and click **Submit**. The ticket creation form supports custom fields and dependent fields, allowing admins to collect structured information tailored to your support [[features/workflows|workflows]]. Ticket tracking allows customers to monitor the progress of their requests and view updates in real time. Customer admins can access all tickets created by their team members, facilitating collaboration and knowledge sharing.

**Conversations and messaging**

Customers engage in threaded conversations with support representatives, providing additional information or seeking clarification regarding their tickets. Support teams respond to customer inquiries within the same thread, ensuring effective communication.

**[[entities/article|Article]] [[features/search|search]]**

Customers can search across your published articles and self-serve on their queries, finding answers on their own instead of waiting for your support team. The customer portal supports both syntactic search (finds results based on keywords) and semantic search (finds results based on the meaning or context of the query).

**Workspace switching**

Customers who belong to multiple workspaces can switch between them using the profile picker in the portal. This allows users to view tickets and articles scoped to each workspace without logging out and back in.

**Multi-language support**

The customer portal supports localization so you can serve customers in their preferred language. For details on configuring multi-language support, refer to [[support-articles/computer-plus-support/multilanguage-support-for-the-customer-portal-and-plug|Portal localization]].

**SEO compatibility**

The customer portal is SEO-compatible, enhancing discoverability so customers can find answers directly through search engines, even before contacting support. Public articles are discoverable by search engines such as Google. The article title is used as the title tag, and the article description serves as the meta description.

Enabling SEO requires the DevRev API. Contact DevRev Support to enable SEO for your portal and ensure the following steps are completed:

1. Set your custom portal URL in [Settings > Plug & Portal > Portal Settings](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration) before requesting SEO activation.
2. Enable SEO through DevRev Support.
3. Set up Google Search Console. Your marketing team with access to Google Search Console can complete this step:

   a. If the domain has not been registered in Google Search Console, register it by following the [Google domain verification guide](https://support.google.com/webmasters/answer/34592?hl=en).

   b. Add the sitemap to Google Search Console. A sitemap communicates the hierarchy and content of your portal to search engine crawlers, assisting in the efficient discovery and indexing of pages. The sitemap URL follows this format:

   ```
   https://<domain>/en-US/<workspace-slug>/sitemap.xml
   ```

   For example, if your portal is configured at `help.abc.com` and your workspace slug is `abc`, the sitemap is at:

   ```
   https://help.abc.com/en-US/abc/sitemap.xml
   ```

   In Google Search Console, click the **Sitemap** tab in the side panel, enter the sitemap link, and click **Submit**.

   1. Request indexing of the portal home page. The home page URL follows this format:

      ```
      https://<domain>/<locale>/<workspace-slug>/directories
      ```

      For example, if your portal is configured at `help.abc.com` and your workspace slug is `abc`, the home page is at:

      ```
      https://help.abc.com/en-US/abc/directories
      ```

      In Google Search Console, click the **URL inspection** tool at the top of the page, enter the home page URL, and click **Request Indexing**.

## Get started

Your customer portal is hosted by default at `support.devrev.ai/<yourcompany>`, where `<yourcompany>` is your workspace slug. To find your workspace slug, go to [Settings > General](https://app.devrev.ai/?setting=general) and locate the slug under your workspace details.

To set up a custom portal URL, configure the domain in [Settings > Plug & Portal > Portal Settings](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration). You must populate the custom portal URL in portal preferences before requesting a custom domain from DevRev Support; omitting this step causes portal access failures.

If your organization enforces strict firewall or Content Security Policy rules, allowlist the required DevRev domains so the portal loads correctly. For details, refer to [Allowlist domains for the portal](https://support.devrev.ai/devrev/article/ART-26498).

Follow these steps to configure the portal for the first time:

1. Create an [[entities/account|account]] in [Accounts](https://app.devrev.ai/?vista=vista-def-accounts) to represent each customer organization.
2. Create contacts in [Contacts](https://app.devrev.ai/?vista=vista-def-contacts) and link each contact to the appropriate account.
3. Configure portal settings in [Settings > Plug & Portal > Portal Settings](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration), including the custom portal URL and branding.
4. Optionally designate customer admins in [Settings > User management > Groups > Customer Admins](https://app.devrev.ai/?setting=groups%2Fgroup-default3).
5. Publish [[features/knowledge-base|knowledge base]] articles and configure their visibility settings so customers can self-serve.
6. Test the portal by logging in as a verified customer to confirm ticket creation, article search, and [[entities/conversation|conversation]] workflows function as expected.

Customers log in on the portal by entering their registered email address and the OTP sent to that address.

![Support portal login](don:core:dvrv-us-1:devo/0:artifact/12734531)

### Public portal access

You can configure the knowledge base to allow public access, which lets visitors browse published articles without logging in. This is useful for organizations that want to provide open self-service documentation. When public access is enabled, visitors can search and read articles but must still log in to create tickets or view existing ones.

### Customer roles and permissions

The customer portal has two levels of customer roles and permissions:

* **Verified customers**: Customers who can log in on the portal and see the tickets that they have created.
* **Customer admins**: Customers who can log in on the portal and see not only their own tickets but also all tickets raised by other users from their organization. You can add multiple customer admins from the same customer organization.

Only verified users can log in to the portal.

> 📝 **Note**: For a ticket to appear in a customer's portal view, the customer must be listed in the **Reported by** field on the ticket. Tickets without the customer in this field are not visible to them, even if they originally submitted the request through another channel.

To create a verified user:

1. Go to [Accounts](https://app.devrev.ai/?vista=vista-def-accounts) and create an account.
2. Go to [Contacts](https://app.devrev.ai/?vista=vista-def-contacts), create a contact, and link it to the account.

To set up customer admins:

1. Go to [Settings > User management > Groups > Customer Admins](https://app.devrev.ai/?setting=groups%2Fgroup-default3).
2. Select **Add User** in the top-right corner and search for the customer you want to designate as a customer admin.

### Customer portal login methods

The customer portal supports three login methods:

1. **Email OTP (one-time password)**: Users enter their email, receive a one-time code, and enter it to log in.
2. [[support-articles/computer-plus-support/federated-identity-provider-setup-for-the-customer-portal|**Federated identity**]]: Users log in through an external [[features/identity|identity]] provider such as Okta, Azure AD, or Google Workspace using the SAML protocol.
3. [[support-articles/computer-plus-support/jwt-based-sso-for-the-customer-portal|**JWT-based authentication**]]: Users log in through a custom integration where your application generates a signed JWT token. This method requires SSO activation by contacting DevRev Support and obtaining an Application Access Token (AAT). Use it when your organization needs programmatic authentication but does not use a centralized identity provider that supports SAML.

For detailed instructions on configuring identity providers, refer to [[support-articles/computer-plus-support/federated-identity-provider-setup-for-the-customer-portal|Identity provider setup]].

### Integrate your knowledge base articles

You can upload articles or provide links to articles hosted on your website or any other publicly accessible platform.

1. Go to [Settings > Support > Knowledge base > Articles](https://app.devrev.ai/?setting=knowledge-base%2Farticles) and click **+ Article**.
2. Add a link to your article or upload articles directly from your device, then set the status to *Draft* or *Published*.

Each article has a **Visible to** field that controls which audience can view it: all customers, verified customers only, or customer admins only. Configure this field to match your intended audience for each article.

Once articles are published, customers can search for them on the customer portal by entering queries in the search bar.

For more information, refer to [[support-articles/computer-plus-support/articles|Articles]].

## Customize the customer portal

You can customize the look of your customer portal to match your branding under [Settings > Plug & Portal > Portal Settings](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration). The portal settings include a **Live Preview** panel that shows changes in real time before you publish.

### General self-serve settings

Go to [Settings > Plug & Portal > Portal Settings > General](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration).

Feature enablement:

* Knowledge base (on/off, private or public access)
* Ticket management (on/off, private or public access)
* Communication banner on ticket list page
* AI search on portal
* PDF article export
* Subscribe to article updates
* [[glossary/plug|Plug]] on portal: Enables the [[features/plug-widget|Plug widget]] directly on the customer portal, giving users access to in-portal chat and AI-assisted support without leaving the page.

### Appearance self-serve settings

Go to [Settings > Plug & Portal > Portal Settings > Appearance](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration).

* Portal Theme: Dark or light mode
* Company Assets: Company name, company logo, favicon
* Color Tokens: Accent color
* Header: Header tabs
* Hero Section: Web and mobile banner images, welcome text, search placeholder
* Footer: Social media and company links

### Non-self-serve settings

The following customizations require assistance from DevRev. To request any of these changes, create a ticket at [DevRev Support](https://support.devrev.ai).

* **URL [[features/customization|customization]]**: You can host the portal on a custom domain (for example, `support.yourcompany.com`) instead of the default DevRev-provided URL. Create a ticket specifying the desired custom URL. Ensure the domain is included in your allowlisted domains.
* **CSS customization**: You can apply custom CSS to adjust portal styling beyond the built-in theme options, such as fonts, spacing, and component-level overrides. Create a ticket describing your requirements. The DevRev team works with you to scope what is achievable within the portal's CSS framework.

## Incident management tab

The customer portal includes a tab that redirects users to the [[glossary/incident|incident]].io page for [[features/incidents|incident management]]. This tab provides direct access to incident management tools and resources, allowing users to view and track active [[features/incidents|incidents]] without leaving the portal experience.

## Conversations and messaging

When a user opens a ticket in the customer portal, comments display with the newest comments appearing first. The comment input box is positioned directly below the latest comment, enabling quicker replies.

The portal automatically scrolls to the latest message when a user opens a ticket, providing a familiar messaging experience similar to popular chat applications.

## Just-in-time access to the customer portal

The portal offers just-in-time (JIT) provisioning to streamline login processes by automatically handling user account management.

When a user logs in, the system verifies whether the user exists as a contact within an account. If no such contact is found, JIT provisioning automatically creates a user account and grants immediate access to the portal. Users can sign up and log in without manual contact creation in the app.

If a user is already a contact in the app but does not have a mapped account, they can still log in and create a ticket. In this scenario, the login is performed under the default workspace assigned to the contact.

Users can also be linked to an existing account to ensure they receive the appropriate permissions upon login.

## Subscribe to articles for updates

You can let users subscribe to knowledge base articles and receive email notifications when updates are published.

A **Subscribe** icon appears below the article title in the customer portal. When users select the icon, they are added as subscribers to that article.

Users must be signed in to subscribe. If a user selects **Subscribe** while signed out, they are redirected to the sign-in page. After signing in, they are automatically added as a subscriber.

When the article is updated, knowledge base owners can choose to notify all subscribers by email.

The **Article Follow** snap-in must be installed before subscriptions work. If the snap-in is not installed, the subscribe toggle in portal settings has no effect.

Only native articles created in DevRev are supported.

To enable article subscriptions:

1. Go to [Settings > Integrations > Snap-ins > All Snap-ins](https://app.devrev.ai/?setting=snap-ins?view=all), search for **Article Follow**, and install the snap-in.
2. Go to [Settings > Plug & Portal > Portal Settings](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration) and turn on the **Subscribe to article updates** toggle.

To notify subscribers about article updates:

1. Open the article and select **Actions**.
2. Select **Publish & Notify** to send an email notification to all subscribers.
3. Optionally add a comment in the dialog box to include in the email, then select **Publish & Notify**.

Email notifications are sent within 5–7 minutes.

You can view all subscribers in the **Subscribers** field after you enable article subscriptions.

### Email notification details

* **Sender**: Article Subscriber bot
* **Subject**: `[Company Name] Update on Article – [Article Title]`
* **Message**: Notifies users that the article has been updated. Includes any additional comment added during publishing and a **View** button that opens the article.

The email template cannot be customized.

## Export articles as PDF

You can let users download knowledge base articles as PDF files directly from the customer portal. A **Download as PDF** option appears on each article, allowing users to save it in PDF format.

To enable PDF downloads, go to [Settings > Plug & Portal > Portal Settings](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration) and turn on the **Download as PDF** toggle.

After you enable this setting, a **Download as PDF** icon appears on all articles.

The PDF download feature is available only for native articles created in DevRev.

## Troubleshooting

* **Issue**: Customer cannot log in to the customer portal.

  **Solution**: Verify the email address is registered as a customer in DevRev. Log in to your DevRev account and search for a customer with that email. If the contact does not exist, create it or enable JIT provisioning. Also confirm the customer has completed the login flow at least once.
* **Issue**: Customer cannot view the tickets they created.

  **Solution**: Log in to DevRev and go to the tickets section. Filter by **Reported by** to confirm tickets exist for that customer. Also verify the customer is logged in to the correct portal URL and not the portal of a different workspace.
* **Issue**: Customer admin cannot see all tickets for the organization.

  **Solution**: Confirm the customer admin is logged in to the correct portal URL. Verify that other customers in the organization have reported tickets. In DevRev, check that the user is assigned the customer admin role.
* **Issue**: You cannot add a customer admin.

  **Solution**: The option to assign a customer admin requires admin access to the DevRev app. If you do not see this option, contact your workspace admin for assistance.
* **Issue**: Customer cannot create a ticket (the "+" button is missing).

  **Solution**: Verify that ticket management is enabled in [Settings > Plug & Portal > Portal Settings](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration) and that access is set to the appropriate visibility (private or public). If ticket management is enabled but the button still does not appear, confirm the customer is signed in and has the required permissions.
* **Issue**: Customer does not receive the OTP email during login.

  **Solution**: Ask the customer to check their spam or junk folder. Some email providers, particularly Microsoft Exchange, may block or delay OTP emails. If the issue persists, verify that the DevRev email sending domain is allowlisted in the customer's email security settings.

## Related wiki nodes
- [[features/customer-portal]]

## Source
- DevRev support article [Customer portal setup and administration](https://support.devrev.ai/en-US/devrev/article/mCD8f9oD) (ART-21864)
