---
title: Plug widget customization
devrev_id: ART-21877
parent_directory: Customer Support Agent
translation_group: H86AvWQa
modified_date: "2026-04-26T21:47:12.587Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/H86AvWQa"
tags: []
top_category: Customer Support Agent
wiki_match: features/plug-widget
match_score: 0.85
last_updated: 2026-05-11
related: ['features/plug-widget']
summary: "There are three ways to customize the PLuG widget."
---

# Plug widget customization

# PLuG widget customization [UPDATE]

> **[[entities/article|Article]] to update:** https://developer.devrev.ai/sdks/[[glossary/plug|plug]]/customize (article/21877)

---

# PLuG widget customization

There are three ways to customize the [[features/plug-widget|PLuG widget]]. They can be combined: SDK values take priority over dashboard settings, and CSS overrides both.

1. **Dashboard settings** — No-code configuration in DevRev Settings.
2. **SDK initialization** — Programmatic options passed to `plugSDK.init()`.
3. **CSS [[features/customization|customization]]** — Full brand styling via a custom stylesheet.

---

## 1. Dashboard settings

Go to **Settings > PLuG & Portal > PLuG Chat**.

### Configuration tab

| Setting | Description |
| --- | --- |
| Unique App ID | Widget identifier. Pass this as `app_id` in `init()`. |
| Enable PLuG widget | Master on/off toggle for all PLuG surfaces. |
| Widget alignment | Left or right relative to the launcher. |
| Enable default launcher | Show or hide the floating button. |
| Custom launcher selector | CSS selector for a custom element to use as the trigger. |

### Styling tab

| Setting | Description |
| --- | --- |
| Launcher logo | Image shown on the floating launcher button. |
| Accent color | Primary brand color used for buttons and links. |
| Primary text color | Main body text color. |
| Theme | Light or dark mode. |
| Brand logo | Logo displayed in the widget header. |
| Launcher position | Bottom/side spacing from screen edges. |
| Banner | Promotional banner shown on the home screen. |
| Custom CSS | Upload a CSS stylesheet for deep brand styling (see section 3). |

### Layout tab

| Setting | Description |
| --- | --- |
| Welcome message | Heading shown when the widget opens (max 50 characters). Configured here, not via SDK. |
| Welcome subtitle | Supporting text below the welcome heading. |
| Quick links | Predefined action buttons on the home screen. |
| Show [[features/search|search]] | Display the search bar on the home screen. |
| Show [[features/conversations-feature|conversations]] | Display the conversations list on the home screen. |
| Show [[features/tickets|tickets]] | Display the tickets list on the home screen. |

### Conversations tab

| Setting | Description |
| --- | --- |
| Auto-popup greeting | Automatically show a greeting when PLuG loads. |
| Greeting delay | Delay (in seconds) before the greeting appears. |
| Enable file attachments | Allow users to attach files in conversations. |
| Enable emoji | Allow emoji in the message input. |
| **One message at a time** | Prevent users from sending multiple messages while the CX Agent is responding. On by default. |

### Language & Region tab

| Setting | Description |
| --- | --- |
| Language | Default language for the widget UI. Supported: English, Spanish, Dutch, Portuguese. |

---

## 2. SDK initialization

Pass options to `plugSDK.init()`. These override any matching settings configured in the dashboard.

```
window.plugSDK.init({
  app_id: '<your_unique_app_id>',          // Required
  theme: 'light',                           // 'light' | 'dark'
  accent_color: '#0047FF',                  // Hex color
  primary_text_color: '#111111',            // Hex color
  enable_default_launcher: true,            // Show floating launcher button
  custom_launcher_selector: '#my-trigger',  // CSS selector for custom trigger
  widget_alignment: 'right',               // 'left' | 'right'
  spacing: {
    bottom: '20px',                         // Distance from bottom of screen
    side: '20px',                           // Distance from side of screen
  },
  disable_plug_chat_window: false,          // Set true to use search-only mode
  session_token: '<backend_generated_token>', // Identifies logged-in users
  enable_session_recording: false,          // Enable session recording
  session_recording_key: '<key>',           // Key for session recording
  send_button_disable_duration: 5000,       // ms; controls one-message-at-a-time timeout
});
```

### Parameter reference

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `app_id` | string | — | **Required.** Your unique PLuG App ID. |
| `theme` | string | `'light'` | Widget color theme: `'light'` or `'dark'`. |
| `accent_color` | string | — | Primary brand color (hex). |
| `primary_text_color` | string | — | Main text color (hex). |
| `enable_default_launcher` | boolean | `true` | Show or hide the floating launcher button. |
| `custom_launcher_selector` | string | — | CSS selector for a custom element to use as the widget trigger. |
| `widget_alignment` | string | `'right'` | Widget position relative to launcher: `'left'` or `'right'`. |
| `spacing.bottom` | string | `'10px'` | Padding distance from the bottom of the screen. |
| `spacing.side` | string | `'0px'` | Distance between the widget and launcher icon. |
| `disable_plug_chat_window` | boolean | `false` | Set to `true` to disable chat and use search only. |
| `session_token` | string | — | Backend-generated token to identify logged-in users. |
| `enable_session_recording` | boolean | `false` | Enable session recording for [[features/analytics|analytics]]. |
| `session_recording_key` | string | — | Key for session recording integration. |
| `send_button_disable_duration` | number (ms) | `5000` | How long the send button stays disabled while the CX Agent is responding. Set to `0` to disable. See [One message at a time](https://#one-message-at-a-time). |

> **Priority:** Values passed to `init()` override dashboard settings. CSS overrides both.

---

## 3. CSS customization (deep brand styling)

For full brand alignment — fonts, component shapes, spacing, animations — you can use Computer or upload a custom stylesheet manually. Both options are available from **Settings > PLuG & Portal > PLuG Chat > Styling > Advanced CSS Customisation**.

### Option A — Use Computer (recommended)

Computer has a dedicated skill for PLuG theming. Describe your brand or share a screenshot, and Computer generates a theme, gives you a live preview URL to review, and can re-upload and publish directly. No manual file handling needed.

> \*"I want to redesign PLuG to match our brand. Here's our website: https://yourcompany.com"\*

> \*"Redesign PLuG to match this screenshot."\* [attach screenshot]

Iterate conversationally until it looks right, then tell Computer to publish. Nothing goes live until you approve it.

### Option B — Download the template and edit manually

1. Go to **Settings > PLuG & Portal > PLuG Chat > Styling > Advanced CSS Customisation**.
2. Click **Download CSS template** to get all available selectors with the `snapkit__` BEM-style prefix.
3. Edit the file to match your brand. Override only the properties you need.
4. Upload it and click **Preview** to see changes live before publishing.
5. Click **Save and Publish**.

### What you can style

The `snapkit__` class system covers all PLuG surfaces:

* Launcher (floating button, icon, badge)
* Header (logo, title, close button, navigation)
* Home screen (banner, quick links, welcome message)
* Chat bubbles (user and agent messages, citations, timestamps)
* Input area (compose bar, send button, attachments, emoji picker)
* Search widget (search bar, results list, AI answer panel)
* [[entities/ticket|Ticket]] form (fields, labels, submit button)
* Footer ("Powered by DevRev" branding)
* Light and dark mode variants

### CSS limits and behavior

* Stylesheets are size-limited for performance. If your file exceeds the limit, PLuG falls back to defaults and shows an error in Settings.
* Override only the properties you need. Avoid re-declaring the full default stylesheet.
* Customizations apply per organisation. Per-instance theming is not supported.
* CSS overrides do not affect the Portal, only the PLuG widget.

Details about all supported are here - <https://app.devrev.ai/devrev/settings/knowledge-base/articles/ART-32867>

---

## Multi-language support

PLuG supports four languages for the widget UI and [[features/knowledge-base|knowledge base]].

**Supported languages:** English (`en`), Spanish (`es`), Dutch (`nl`), Portuguese (`pt`).

**What is automatically translated:**

* All stock UI components: buttons, navigation, form labels, severity options, error messages.
* Ticket creation form stock field values.
* Search, including AI-powered search, across all four languages.

**What you must translate manually:**

* Welcome message text and any custom card copy.
* Knowledge base [[entities/article|articles]] and collections. Draft and publish per language from **Settings > Knowledge Base > Articles**.

Configure the default language at **Settings > PLuG & Portal > PLuG Chat > Language & Region**.

---

## One message at a time

When enabled, PLuG prevents users from sending a second message while the CX Agent is still responding. This avoids duplicate conversations and prevents automations from firing more than once.

**How it works:**

PLuG cannot always know upfront whether the [[entities/conversation|conversation]] will go to a CX Agent or a human. So:

* On the **first message**, the send button is blocked for up to 5 seconds while PLuG waits to learn who is responding.
* If the response comes from a **CX Agent**, blocking becomes intelligent. The button stays disabled only while the agent is actively streaming, then re-enables automatically.
* If the other side is a **human agent**, blocking stops entirely.

The input field remains active throughout so users can keep composing.

**Toggle:** **Settings > PLuG & Portal > PLuG Chat > Conversations > One message at a time** — on by default.

**SDK override:** Pass `send_button_disable_duration` (in ms) to `init()` to adjust or disable the initial timeout. Set to `0` to disable blocking entirely.

---

## CX Agent response streaming

The CX Agent streams responses token-by-token so users see answers appearing in real time. Before its first tool call, the agent sends a brief personalised acknowledgement, which eliminates the silent wait.

Streaming is **on by default** for all organisations on web.

Streaming behaviour is configurable per agent via the API. The Response Settings UI in Agent Studio is not yet available.

| Value | Behaviour |
| --- | --- |
| `final_response` | Streams the final answer token-by-token. **Default.** |
| `intermediate_thoughts` | Also streams intermediate reasoning steps to the user. |
| `disabled` | Returns the full response at once with no streaming. |

```
curl -sS -X POST "https://api.devrev.ai/internal/ai-agents.update" \
  -H "Authorization: Bearer ${DEVREV_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "id": "<your_agent_don_id>",
    "response_options": {
      "streaming": "final_response"
    }
  }'
```

On **mobile SDKs (iOS / Android)**, streaming support has been added. Refer to the iOS and Android SDK reference pages for the current syntax.

---

## Related articles

* [PLuG Web SDK — Installation](https://developer.devrev.ai/sdks/web/installation)
* [PLuG Web SDK — Methods](https://developer.devrev.ai/sdks/web/methods)
* [PLuG Web SDK — User identity](https://developer.devrev.ai/sdks/web/user-identity)
* [Install PLuG search](https://developer.devrev.ai/sdks/web/install-search)
* [Customise PLuG search](https://developer.devrev.ai/sdks/web/search-customization)
* [PLuG Nudges](https://devrev.ai/docs/plug/nudges)

## Related wiki nodes
- [[features/plug-widget]]

## Source
- DevRev support article [Plug widget customization](https://support.devrev.ai/en-US/devrev/article/H86AvWQa) (ART-21877)
