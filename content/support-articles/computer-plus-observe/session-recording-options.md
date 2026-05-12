---
title: Session recording options
devrev_id: ART-21918
parent_directory: Computer+ Observe
translation_group: 8teIro6K
modified_date: "2026-03-26T05:19:45.94Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/8teIro6K"
tags: []
top_category: Computer+ Observe
wiki_match: features/email-integration
match_score: 0.476
last_updated: 2026-05-11
summary: "During Plug SDK initialization, you can provide custom attributes for session recording options."
---

# Session recording options

During [[glossary/plug|Plug]] SDK initialization, you can provide custom attributes for session recording options. If no custom attributes are specified, the default options are used.

Plug SDK offers the ability to hide sensitive user information by masking it in session recordings. During session replays, masking replaces user-visible or typed content in specific elements with asterisks ("\*"). This ensures that sensitive information is not displayed in the recordings, protecting user privacy.

During Plug initialization, you have several options to manually configure which elements should be masked. Masking is applied based on the element's ID, allowing you to control which specific fields are protected in the session replay.

```
window.plugSDK.init({
// Please ensure you replace the app_id with your unique app ID
    app_id: "<your_unique_app_id>",
    session_recording_options: PlugStartRecordingOptions,
    sessionDetails: {
        sessionId?: string;
        tabId?: string;
    },

})

PlugStartRecordingOptions = {
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
        recordCrossOriginIframes?: boolean;
        maskTextFn?: (text: string, element: HTMLElement | null) => string;
    }
}
```

|  |  |  |
| --- | --- | --- |
| Option | Description | Default |
| `maskAllInputs` | Whether all input elements (irrespective of their types) should be masked during session recording. | False |
| `maskInputOptions` | Whether specific input element types should be masked during session recording. | The masking preference applies as follows: input elements with types `email`, `tel`, or `password` are masked during session recording, while other input types are not masked. For example, `<input type="email"/>` is masked, but `<input type="text" name="email"/>` is not masked. |
| `captureMouseMove` | Whether to capture the full mouse movement throughout the session or only track mouse clicks. | False |
| `captureNetworkLogs` | Whether network logs should be captured during the session. | True |
| `captureConsoleLogs` | Whether the session captures console logs or not. | True |
| `recordCrossOriginIframes` | Whether interactions occurring within the chat widget and [[features/search|search]] agent should be captured or not. | True |
| `sessionDetails.sessionId` | Field to pass session ID of the previous session to link. | null |
| `sessionDetails.tabId` | Field to pass the tab ID of the previous session to link. | null |
| `maskTextFn` | An option to customize the logic for masking sensitive text during session recording. This function accepts a callback that receives the text content and allows you to define how the text should be masked | null Example: `maskTextFn: (text: string, element: HTMLElement) => {`  `return text.replace(/[\S]/g, "@");` `};`. |

# Mask text function example

The function replaces all non-whitespace characters in the given text with the "@" symbol.

```
maskTextFn: (text: string, element: HTMLElement) => {
  return text.replace(/[\S]/g, "@");
};
```

In addition, you can use the following CSS classes to mask or unmask specific elements on your webpage:

|  |  |
| --- | --- |
| Purpose | CSS classes |
| To mask all page elements, add the CSS class `ue-mask` to your app's body tag. | `<body class="ue-mask"> ... </body>` |
| To mask a specific element during capture, apply the CSS class `ue-mask` to it. | `<div class="ue-mask"> Hello World </div>` |
| Apply the `ue-mask` CSS class to images to mask them with a black overlay during capture. | `<img class="ue-mask" src="…" >` |
| Use the CSS class `ue-input-mask` to mask input elements, displaying their data as \*\*\* in session replays. **NOTE**: Password fields are masked by default, but applying the ue-input-mask class adds extra security. | `<input class="ue-input-mask"/>` |
| Use the CSS class `ue-unmask` to unmask text and input elements. This also unmasks texts found in child elements as well. For input fields, it is only applied on the direct input element consisting the class. | `<div class="ue-unmask"> Hello World </div>` |
| To block input data from being captured in the session replay, apply the `ue-block` class. This prevents the SDK from recording the input. | `<input class="ue-block"/>` |

You can set a custom label for an element using the `data-plug-label` attribute, and this label appears in the web player timeline.

|  |  |  |
| --- | --- | --- |
| Attribute | Description | Example |
| `data-plug-label` | Custom attribute to set an element's label in the web player timeline. | `<h1 data-plug-label="Custom label"> ... </h1>` |

## Source
- DevRev support [[entities/article|article]] [Session recording options](https://support.devrev.ai/en-US/devrev/article/8teIro6K) (ART-21918)
