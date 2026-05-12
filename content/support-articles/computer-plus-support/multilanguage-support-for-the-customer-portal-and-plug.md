---
title: Multilanguage support for the customer portal and Plug
devrev_id: ART-24672
parent_directory: Customer portal
translation_group: UTCG6oLa
modified_date: "2026-04-03T16:59:01.087Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/UTCG6oLa"
tags: []
top_category: Computer+ Support
wiki_match: features/customer-portal
match_score: 0.85
last_updated: 2026-05-11
related: ['features/customer-portal']
summary: "The customer support portal and Plug can be configured to support multiple languages."
---

# Multilanguage support for the customer portal and Plug

The customer support portal and [[glossary/plug|Plug]] can be configured to support multiple languages. For DevRev app UI language settings, see [Multilanguage support in DevRev](https://support.devrev.ai/devrev/article/ART-17790). For general portal setup including custom domains, login methods, and roles, see [[support-articles/computer-plus-support/customer-portal-setup-and-administration|Customer portal setup]].

## Multilanguage portal user experience

**Language switching on the portal**

If a translation exists for the selected language, the customer sees the translated [[entities/article|article]] or collection. If a translation does not exist, the customer lands on an error page with a link back to the homepage. Customers who access your portal URL without a language code see the default language.

**[[features/search|Search]] behavior**

On the portal and Plug, search is language-scoped: a customer on the Spanish portal sees results only from published Spanish [[entities/article|articles]]. In [[features/conversations-feature|conversations]], articles from all languages are indexed regardless of the Plug language, and the AI responds in the language the customer writes in.

**[[entities/ticket|Ticket]] fields**

Stock ticket fields are auto-translated with no manual work needed. Custom ticket fields are not translated.

Configure Portal and Plug to serve content in multiple languages. This guide covers adding languages, configuring translations for Portal and Plug, and managing translated [[features/knowledge-base|knowledge base]] articles.

## Supported languages

The following locales are supported for the [[features/customer-portal|customer portal]] and Plug. Additional languages may be enabled on request by contacting [DevRev support](https://support.devrev.ai).

| **Language** | **Code** |
| --- | --- |
| Arabic (UAE) | ar-AE |
| German (Germany) | de-DE |
| English (UAE) | en-AE |
| English (Australia) | en-AU |
| English (UK) | en-GB |
| English (US) | en-US |
| Spanish (Argentina) | es-AR |
| Spanish (Spain) | es-ES |
| Spanish (Mexico) | es-MX |
| French (France) | fr-FR |
| Hebrew (Israel) | he-IL |
| Hindi (India) | hi-IN |
| Indonesian | id-ID |
| Italian (Italy) | it-IT |
| Japanese (Japan) | ja-JP |
| Korean (South Korea) | ko-KR |
| Malay (Malaysia) | ms-MY |
| Dutch (Netherlands) | nl-NL |
| Polish (Poland) | pl-PL |
| Portuguese (Brazil) | pt-BR |
| Portuguese (Portugal) | pt-PT |
| Russian (Russia) | ru-RU |
| Slovenian (Slovenia) | sl-SI |
| Thai (Thailand) | th-TH |
| Urdu (Pakistan) | ur-PK |
| Vietnamese (Vietnam) | vi-VN |
| Chinese (Simplified, China) | zh-CN |
| Chinese (Traditional, Taiwan) | zh-TW |
| Spanish (Peru) | es-PE |
| Spanish (Colombia) | es-CO |

## Before you begin

* Confirm you have admin access to DevRev settings.
* Set up your Portal or Plug in the default language (`en-US`) before adding translations.
* Prepare translated content for each language you plan to support.

Global settings (such as enabling knowledge base, conversations, and portal visibility) apply to all languages. Configure these settings from the default language (`en-US`).

## Portal configuration

### Enable languages

1. Go to [Settings > Language & Region > Plug & Portal language settings](https://app.devrev.ai/?setting=languages) and add languages for Portal in the **Customer Portal Language Settings** section.
2. Go to [Settings > Portal Settings](https://app.devrev.ai/?setting=customer-portal-settings%2Fgeneral?activeTab=appearance) and select the default language (`en-US`).
3. Configure global settings (knowledge base, ticketing, AI search). These settings apply to all languages.
4. Customize language-specific fields (brand text, design labels, custom labels) for the default language.
5. Click **Apply Changes**.
6. Select each additional language from the language switcher.
7. Customize language-specific fields for each language.
8. Click **Apply Changes** for each language.
9. Enable the **Publish toggle** for each language you want to make available. Each language must be published independently.

The system translates static components (such as "Search" and navigation labels) automatically. You must translate custom components (such as company name and custom labels) manually for each language.

### Configure knowledge base translations

Create your collection hierarchy in all languages before adding articles. The structure must be identical across languages.

1. Create collections in the default language (`en-US`).
2. Create translated versions in each additional language with the same hierarchy.
3. Create articles in the default language and assign them to collections.
4. Create a translation of each article for each additional language. The collection mapping applies automatically from the default language version.

> ⚠️ **Warning**: If a translated collection does not exist when you create an article translation, the system displays a warning and cannot map the article automatically.

Translated articles inherit the visibility settings of the default language version. If you change the collection assignment for one language version, verify the collection mappings for all language versions.

To verify, do the following:

* Open your portal URL without a language code and confirm the default language (`en-US`) appears.
* Open your portal URL with a language code appended (for example, `/fr-FR` or `/ja-JP`) and confirm the translated content appears.

### Manage article translations

To delete a single language version, select the three-dot menu in the article list and remove the translation. To delete all language versions, select the remove icon on the article page.

When importing articles through the API, pass the `language` parameter to assign the article to a specific language:

* Pass a supported language code to create the article in that language.
* Omit the language code to create the article in the default language (en-US).
* Avoid passing unsupported language codes. The API returns an error.

When importing articles through the [[glossary/airsync|AirSync]] connector for Zendesk, configure language mappings to assign translated articles to the correct locale in DevRev.

### Troubleshooting

* **[[entities/issue|Issue]]**: A translated article shows a collection warning and cannot be mapped to a collection.

  **Solution**: Create the translated collection structure before creating translated articles. The collection hierarchy must match across all languages. Once the translated collection exists, re-map the article to the correct collection.
* **Issue**: A language does not appear on the portal after configuration.

  **Solution**: Verify that the **Publish** toggle is enabled for that language in [**Settings** > **Plug & Portal** > **Portal Settings**](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration). Each language must be published individually. Also confirm that at least one piece of content (an article or collection) exists in that language.
* **Issue**: The API returns an error when creating an article with a language code.

  **Solution**: Verify the language code matches one of the supported codes exactly (for example, `es-ES`, not `es`). If the language is not in the supported list, contact [DevRev support](https://support.devrev.ai) to request it.
* **Issue**: You need the `translation_group` for an article but it is not returned by the API.

  **Solution**: Use the `/internal/articles.get` endpoint instead of `articles.get`. The `translation_group` field is not exposed in the public endpoint.

## Plug configuration

1. Go to [Settings > Language & Region > Plug & Portal language settings](https://app.devrev.ai/?setting=languages) and add languages for Plug in the **Plug Language Settings** section.
2. Go to [Settings > Plug Chat](https://app.devrev.ai/devrevdocs/settings/customer-portal-settings/general?activeTab=appearance).
3. Select the default language (`en-US`).
4. Configure [[entities/conversation|conversation]] toggle, button text, logo, accent color, tabs (Home, Conversations, [[features/tickets|Tickets]]), and welcome text.
5. Click **Save & Publish**.
6. Select each additional language from the language switcher.
7. Customize language-specific fields for each language.
8. Click **Save & Publish** for each language.

Each language must be saved and published independently. Changes to one language do not affect other languages.

To set the language programmatically, pass the `locale` parameter when initializing Plug on your website:

```
window.plugSDK.init({
  // ...existing options,
  locale: 'en-US' // Replace with the target language code
});
```

To verify, open the [[features/plug-widget|Plug widget]] on your website with the `locale` parameter set and confirm the translated interface loads.

### Troubleshooting

* **Issue**: Plug displays in the wrong language.

  **Solution**: Ensure the correct locale code is passed in the `plugSDK.init()` call. The locale value must match one of the supported language codes listed above.

## Related wiki nodes
- [[features/customer-portal]]

## Source
- DevRev support article [Multilanguage support for the customer portal and Plug](https://support.devrev.ai/en-US/devrev/article/UTCG6oLa) (ART-24672)
