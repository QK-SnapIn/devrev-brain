---
title: Custom implementation
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/web/customize
last_updated: 2026-05-11
summary: "Plug has a completely no-code way of changing the look and interaction of your widget."
---

# Custom implementation

PLuG Web SDK

# Custom implementation

Plug has a completely [no-code way](https://support.devrev.ai/devrev/article/ART-21877) of changing the look and interaction of your widget. In case you wish to make your Plug widget more interactive and customized to how your app is structured, you can use these customization properties to set up your widget.

If you have customized these properties of the widget through the Plug settings page of DevRev, the values set in the initalization code take priority over those which you have updated in your Plug settings.

All of these properties have to be passed as parameters while initializing the Plug widget using `plugSDK.init()`. For details, refer to the Plug SDK for Web [methods documentation](/sdks/web/methods).

| Customization | Description |
| --- | --- |
| `custom_launcher_selector` | Customize the widget launcher to best fit your website or app. |
| `widget_alignment` | Align the widget to be placed either on the left or right side, relative to the launcher. |
| `enable_default_launcher` | Show/hide the default Plug Widget launcher. |
| `theme` | Set the theme of the Plug Widget. |

## [Code sandbox](#code-sandbox)

## [Properties](#properties)

### [Plug launcher](#plug-launcher)

Customize the widget launcher to best fit your website or app; or show or hide the default Plug widget launcher.

To customize your Plug launcher styles, specify the CSS selector in the `custom_launcher_selector` property. This CSS selector is the reference based on which your Plug widget opens. This property accepts a string value. The selector can also be configured through the plug settings on app.devrev.ai.

```
custom_launcher_selector?: '#my-plug-widget'
```

Use the `enable_default_launcher` property only if you are not using the custom launcher selector.

```
enable_default_launcher?: boolean;
```

The default value is `true`.

### [Widget alignment](#widget-alignment)

Align the widget to be placed on the left or right of the launcher.

The widget can be set to open to the left or to the right of the custom launcher.

```
widget_alignment?: 'left' | 'right';
```

The default value is `right`.

### [Spacing](#spacing)

Adjust spacing of the Plug widget.

Two properties are available to apply spacing.

* The `bottom` property determines the padding from the bottom of the launcher.

  The default value is `10px`.
* The `side` property determines the spacing of the widget from the launcher icon.

  The default value is `0px`.

```
spacing?:{
    bottom?: '10px',
    side?:'10px',
}
```

### [Light/dark theme](#lightdark-theme)

Set the theme of the Plug widget.

```
theme?: 'dark' | 'light';
```

The default value is `light`.

Last updated on

[Methods

Previous Page](/sdks/web/methods)[UserExperior migration

Next Page](/sdks/web/migration)

## Source
- DevRev developer docs: [Custom implementation](https://developer.devrev.ai/sdks/web/customize)
