---
title: Install the Web SDK
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/web/installation
last_updated: 2026-05-11
summary: "To install the Plug SDK on your website or web application, insert the code snippet provided below on every page where you want the SDK to be active."
---

# Install the Web SDK

PLuG Web SDK

# Install the Web SDK

To install the Plug SDK on your website or web application, insert the code snippet provided below on every page where you want the SDK to be active. Once the SDK is installed, the chat widget appears by default.

## [Getting your unique app ID](#getting-your-unique-app-id)

You can access your app ID from your DevRev account by following these steps:

1. In DevRev, go to **Settings > Support > Plug Settings** via the settings icon in the top-left corner.
2. If the Plug feature is not already enabled, click **Enable Plug**.
3. Under the **Configuration** tab, copy the **Unique App ID**.

Place the following code in the `<head>` section of your HTML page:

```
<script
  type="text/javascript"
  src="https://plug-platform.devrev.ai/static/plug.js"
></script>
```

Place the following code in the `<body>` section of your HTML page:

```
<script>
  window.plugSDK.init({
    // Please ensure you replace the app_id with your unique app id
    app_id: "<your_unique_app_id>",
  });
</script>
```

Add the following code to the public/index.html file, inside the `<body>` tag of your HTML page:

```
<script
  type="text/javascript"
  src="https://plug-platform.devrev.ai/static/plug.js"
></script>
```

Place the following code inside the React component where you want to render the Plug widget. Typically, this should be done in a top-level component like `App.js`.

```
useEffect(() => {
  window.plugSDK.init({
    // Please ensure you replace the app_id with your unique app id
    app_id: "<your_unique_app_id>",
  });
}, []);
```

The Plug widget should now be installed on your website. If you experience any issues, you can reach out to us using our Plug chat widget in the bottom right corner of your screen.

After the widget is installed on your website, every visitor is considered an anonymous user. Anonymous users are those who have not yet logged in or shared any personal information.

After integrating the Plug widget, you can personalize and contextualize customer engagement. Learn how to [identify your customers](https://developer.devrev.ai/sdks/web/user-identity) and update their information.

Once the SDK is installed, the chat widget appears by default. If you are not
using the Plug SDK for support or chat-related flows, you can disable the chat
widget by setting the `disable_plug_chat_window` input to `true`.

```
<script>
    window.plugSDK.init({
        app_id: '<your_unique_app_id>',
        disable_plug_chat_window: true,
    });
</script>
```

To ensure seamless communication between the Web SDK and external services, you must configure your Content Security Policy (CSP) to allow access to specific domains.

* <https://api.devrev.ai>
* <https://plug-platform.devrev.ai>
* <https://ingestion-useast1.devrev.ai> - For organizations in the US East region.
* <https://ingestion-eucentral1.devrev.ai> - For organizations in the EU Central region.
* <https://ingestion-apsouth1.devrev.ai> - For organizations in the AP South region.
* <https://ingestion-apsoutheast1.devrev.ai> - For organizations in the AP South East 1 region.
* <https://ingestion-apsoutheast2.devrev.ai> - For organizations in the AP South East 2 region.

Last updated on

[Overview

Previous Page](/sdks)[Install Plug search

Next Page](/sdks/web/install-search)

## Source
- DevRev developer docs: [Install the Web SDK](https://developer.devrev.ai/sdks/web/installation)
