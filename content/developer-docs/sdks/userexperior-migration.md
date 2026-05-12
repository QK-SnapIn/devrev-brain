---
title: UserExperior migration
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/web/migration
last_updated: 2026-05-11
summary: "The DevRev Plug SDK serves as a direct replacement for the legacy UserExperior Web SDK."
---

# UserExperior migration

PLuG Web SDK

# UserExperior migration

The DevRev Plug SDK serves as a direct replacement for the legacy UserExperior Web SDK. This section outlines the steps to facilitate a seamless migration from UserExperior to DevRev Plug.

NPM package support is discontinued.

## [Installation](#installation)

Update your script tags as shown to migrate successfully to the DevRev Plug SDK.

```
<script src="https://unpkg.com/user-experior-web@latest/bundle/ue-web-bundle.js"></script>
```

```
<script type="text/javascript" src="https://plug-platform.devrev.ai/static/plug.js"></script>
```

## [Initialization](#initialization)

Update your initialization code to work with the DevRev Plug SDK, ensuring session recording is enabled and handling events appropriately.

```
const ue = new UserExperior.init();
ue.startRecording("<your_unique_app_id>")
.then(() => {
  // code you want to execute after recording starts
  // you can call the setUserIdentifer method here
})
.catch((error) => {
  // code you want to execute if recording fails
});
```

To enable session recordings, go to **Settings** > **Support** > **Session Replays** and enable recordings for your desired platforms.

```
window.plugSDK.init({
   app_id: "<your_unique_app_id>",
   disable_plug_chat_window: true,
});
window.plugSDK.onEvent((payload) => {
	if (payload.type === 'ON_OBSERVABILITY_READY') {
    // code you want to execute after recording starts
	}
});
```

If you have configured Content Security Policy (CSP) in your application, you need to allow access to the following domains.

* <https://api.devrev.ai>
* <https://plug-platform.devrev.ai>
* <https://ingestion-useast1.devrev.ai> - For organizations in the US East region.
* <https://ingestion-eucentral1.devrev.ai> - For organizations in the EU Central region.
* <https://ingestion-apsouth1.devrev.ai> - For organizations in the AP South region.
* <https://ingestion-apsoutheast1.devrev.ai> - For organizations in the AP South East 1 region.
* <https://ingestion-apsoutheast2.devrev.ai> - For organizations in the AP South East 2 region.

## [Recording options](#recording-options)

```
ue.startRecording("243b0f40-db67-4f3e-b51d-c52001dd858a", {
	sessionReplay: {
		// To mask all the input fields pass the following.
		maskAllInputs: true,
		
		// Available Mask Input Options:
		maskInputOptions: {
		    color: boolean,
		    date: boolean,
		    'datetime-local': boolean,
		    month: boolean,
		    number: boolean,
		    range: boolean,
		    search: boolean,
		    text: boolean,
		    time: boolean,
		    url: boolean,
		    week: boolean,
		    textarea: boolean
		},
		
		// Mouse moves are also ignored by default by the SDK to avoid unnecessary events increasing the payload size. To enable mouse move capture  
		// you need to specify the following option to capture the mouse movements:
		captureMouseMove: true 
		
		// By default we track network log in session. To disable network log tracking you can specify the following option:
		captureNetworkLogs: false 
		
		// By default we track console errors in session. To disable console tracking you can specify the following option:
		captureConsoleLogs: false 
	}
});
```

```
window.plugSDK.init({
  app_id: "<your_unique_app_id>",
  disable_plug_chat_window: true,
  session_recording_options: {
  		sessionReplay: {
  			maskAllInputs?: boolean;
  			maskInputOptions?: {
  				color: boolean;
  				date: boolean;
  				'datetime-local': boolean;
  				email: boolean;
  				month: boolean;
  				number: boolean;
  				range: boolean;
  				search: boolean;
  				tel: boolean;
  				text: boolean;
  				time: boolean;
  				url: boolean;
  				week: boolean;
  				textarea: boolean;
  				select: boolean;
  			};
  			captureMouseMove?: boolean;
  			captureNetworkLogs?: boolean;
  			captureConsoleLogs?: boolean;
  		}
  },
})
```

## [Masking](#masking)

The same CSS classes from UserExperior are compatible with the DevRev Plug SDK without modifications.

**Specific HTML elements**

To mask a div:

```
<div class="ue-mask">Hello World</div>
```

**Input elements**

To mask input text:

```
<input class="ue-input-mask"/>
```

To completely block the input element:

```
<input class="ue-block"/>
```

These classes ensure elements are masked or blocked as required.

## [User identification](#user-identification)

```
// Setting a user identifier
ue.setUserIdentifier('unique-user-identifier');

// Passing user properties
ue.setUserIdentifier('unique-user-identifier', {
 key1: value1,
 key2: value2,
 // ...
});
```

DevRev introduces the concept of a `RevUser` object for enhanced user identity management. Use this to associate sessions with users and attach properties. For more details, refer to the [DevRev user identity](https://developer.devrev.ai/sdks/web/user-identity).

## [Logging custom events](#logging-custom-events)

This approach facilitates custom event tracking, similar to the process in UserExperior, with additional capabilities.

```
ue.logEvent("YOUR_EVENT", {
    key1: value1,
    key2: value2,
    ...
})
```

```
window.plugSDK.trackEvent("YOUR_EVENT", {
    key1: value1,
    key2: value2,
    ...
})
```

For more details, see the [Track events](https://developer.devrev.ai/sdks/web/track-events).

## [Session attributes (User properties)](#session-attributes-user-properties)

UserExperior allowed setting session-level properties but didn’t have a global user object. DevRev utilizes the `RevUser` object and `addSessionProperties()` for enhanced functionality.

For setting user properties, refer to the [User Identification](https://developer.devrev.ai/sdks/web/user-identity).

```
ue.setUserProperties({
    key1: value1,
    key2: value2,
    ...
})
```

```
window.plugSDK.addSessionProperties({
    key1: value1,
    key2: value2,
    ...
})
```

## [Restart a session](#restart-a-session)

Terminate the current session recording and start a new one.

```
 ue.restartSession();
```

```
await window.plugSDK.shutdown();
window.plugSDK.init({
   app_id: "<your_unique_app_id>",
   disable_plug_chat_window: true,
});
```

Last updated on

[Custom implementation

Previous Page](/sdks/web/customize)[Quickstart guide

Next Page](/sdks/android/quickstart)

## Source
- DevRev developer docs: [UserExperior migration](https://developer.devrev.ai/sdks/web/migration)
