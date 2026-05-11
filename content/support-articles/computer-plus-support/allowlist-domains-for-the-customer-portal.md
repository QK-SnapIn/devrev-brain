---
title: Allowlist domains for the customer portal
devrev_id: ART-23634
parent_directory: Customer portal
translation_group: 6_lYKw2d
modified_date: "2026-04-09T12:45:25.136Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/6_lYKw2d"
tags: []
top_category: Computer+ Support
wiki_match: features/customer-portal
match_score: 0.85
last_updated: 2026-05-11
related: ['features/customer-portal']
---

# Allowlist domains for the customer portal

The DevRev customer portal requires specific domains to be reachable from end-user networks. If users access the portal from behind a VPN, firewall, proxy, or other network security layer, share the domain list below with your IT or network team so they can add the entries to the organization's allowlist.

## Prerequisites

Before deploying the customer portal to end users, confirm the following with your IT or network team:

1. Determine whether the organization uses a VPN (such as Zscaler, Cisco AnyConnect, Palo Alto GlobalProtect, or another solution) and whether it restricts outbound traffic by domain.
2. Check whether corporate firewalls or web proxies filter outbound HTTPS traffic.
3. Verify whether network access is restricted by default (deny-all policies), which requires explicit domain allowlisting.

If any of these conditions apply, the domains listed below must be added to the allowlist before users can access the portal.

## Required domain allowlist

Add the following domains to your network security configuration to ensure full functionality of the customer portal.

### Authentication

* `rev.auth.devrev.ai`

### Core portal services

* `support.devrev.ai`
* `api.devrev.ai`
* `default-portal-template.devrev.ai`
* `plug-platform.devrev.ai`
* `portal-library.devrev.ai`
* `exp.devrev.ai`
* `app.devrev.ai`

### Infrastructure services

* `ingestion-useast1.devrev.ai`
* `dvrv-us-1-wss.devrev.ai`
* `dvrv-in-1-wss.devrev.ai`
* `dvrv-sg-1-wss.devrev.ai`
* `dvrv-au-1-wss.devrev.ai`
* `dvrv-eu-1-wss.devrev.ai`
* `dvrv-jp-1-wss.devrev.ai`
* `default-portal-template.devrev.com`
* `portal-library.devrev.com`

DevRev documents domain-based allowlisting only. Static IP addresses and specific port numbers are not published because the underlying infrastructure may change. All traffic uses HTTPS (port 443). If your organization requires IP-level firewall rules, contact DevRev Support to discuss your requirements.

## Plug widget embedding

The domain list above covers the customer portal hosted by DevRev. If you embed the Plug chat widget on your own website, your site's Content Security Policy (CSP) headers must also permit connections to the domains listed above—particularly `plug-platform.devrev.ai`, `api.devrev.ai`, and the relevant regional WebSocket endpoint (`dvrv-*-wss.devrev.ai`). Add these origins to the `connect-src` and `frame-src` directives in your CSP.

## Email OTP delivery

If the portal uses email-based one-time passwords (OTP) for authentication, ensure that your email servers do not block messages from DevRev. Microsoft Exchange and Microsoft 365 servers in particular may quarantine OTP emails when the code appears in the subject line. Configure your mail server or spam filter to allow emails from DevRev's sending domain.

## Troubleshooting

* **Issue**: Users cannot access the portal or see a blank page after the domains have been allowlisted.

  **Solution**: Verify that all domains in the list above—including both `.devrev.ai` and `.devrev.com` entries—are allowlisted. Some proxies and VPNs cache DNS or maintain separate allowlists per policy group. Clear the DNS cache, confirm the rules apply to the affected user group, and retry. If the issue persists, contact DevRev Support with the list of domains you have allowlisted and any error messages or network traces.
* **Issue**: The Plug support chat widget does not load on your website.

  **Solution**: Ensure your site's CSP headers include the DevRev domains in `connect-src` and `frame-src` as described in the Plug widget embedding section above. Use your browser's developer console to check for blocked requests.
* **Issue**: Users do not receive OTP emails required to log in to the portal.

  **Solution**: Check your email server's quarantine and spam filters for blocked messages from DevRev.
* **Issue**: The organization blocks all `.ai` domains and cannot create exceptions.

  **Solution**: Configure a custom portal domain using a permitted TLD. The backend `.devrev.ai` API and WebSocket domains still require individual exceptions.

## Next steps

Provide the full domain list to your IT or network team and verify portal access from a representative end-user network segment before rolling out to all users. For an overview of portal capabilities, see the [[support-articles/computer-plus-support/customer-portal-setup-and-administration|customer portal overview]].

## Related wiki nodes
- [[features/customer-portal]]

## Source
- DevRev support article [Allowlist domains for the customer portal](https://support.devrev.ai/en-US/devrev/article/6_lYKw2d) (ART-23634)
