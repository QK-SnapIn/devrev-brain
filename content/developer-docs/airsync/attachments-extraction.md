---
title: Attachments extraction
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/extract-attachments
last_updated: 2026-05-11
summary: "During the attachments extraction phase, the snap-in retrieves attachments from the external system and uploads them to DevRev."
---

# Attachments extraction

Development Guide

# Attachments extraction

During the attachments extraction phase, the snap-in retrieves attachments from the external system and uploads them to DevRev. This phase occurs after data extraction, transformation, and loading are completed.

## [Triggering event](#triggering-event)

### [Event types](#event-types)

| Event | Direction | Description |
| --- | --- | --- |
| `START_EXTRACTING_ATTACHMENTS` | AirSync → Snap-in | Initiates the attachments extraction |
| `ATTACHMENT_EXTRACTION_PROGRESS` | Snap-in → AirSync | Indicates process is ongoing but runtime limit (13 minutes) reached |
| `ATTACHMENT_EXTRACTION_DELAYED` | Snap-in → AirSync | Requests a delay due to rate limiting from external system |
| `CONTINUE_EXTRACTING_ATTACHMENTS` | AirSync → Snap-in | Resumes the extraction process after progress update or delay |
| `ATTACHMENT_EXTRACTION_DONE` | Snap-in → AirSync | Signals successful completion of attachments extraction |
| `ATTACHMENT_EXTRACTION_ERROR` | Snap-in → AirSync | Indicates that an error occurred during extraction |

## [Implementation](#implementation)

### [Default implementation](#default-implementation)

The SDK provides a default implementation for attachments extraction. If the default behavior (iterating through attachment metadata and uploading from saved URLs) meets your needs, **no additional implementation is required**.

### [Custom implementation](#custom-implementation)

If you need to customize the attachments extraction, modify the implementation in `attachments-extraction.ts`.
Use the `streamAttachments` function from the `WorkerAdapter` class, which handles most of functionality needed for this phase:

```
const response = await adapter.streamAttachments({
  stream: getFileStream,
  batchSize: 10
});
```

Parameters:

* `stream`: (Required) Function that handles downloading attachments from the external system
* `batchSize`: (Optional) Number of attachments to process simultaneously (default: 1)

Increasing the batch size (from the default 1) can significantly improve performance. But be mindful of lambda memory constraints and external system rate limits when choosing batch size. A batch size between 10 and 50 typically provides good results.

```
async function getFileStream({
  item,
}: ExternalSystemAttachmentStreamingParams): Promise<ExternalSystemAttachmentStreamingResponse> {
  const { id, url } = item;

  try {
    const fileStreamResponse = await axiosClient.get(url, {
      responseType: 'stream',
      headers: {
        'Accept-Encoding': 'identity',
      },
    });

    return { httpStream: fileStreamResponse };
  } catch (error) {
    if (axios.isAxiosError(error)) {
      console.warn(`Error while fetching attachment ${id} from URL.`, serializeAxiosError(error));
      console.warn('Failed attachment metadata', item);
    } else {
      console.warn(`Error while fetching attachment ${id} from URL.`, error);
      console.warn('Failed attachment metadata', item);
    }

    return {
      error: {
        message: `Failed to fetch attachment ${id} from URL.`,
      },
    };
  }
}
```

## [Emitting responses](#emitting-responses)

The snap-in must send exactly one response to AirSync when extraction is complete:

```
await adapter.emit(ExtractorEventType.AttachmentExtractionDone);
```

```
await adapter.emit(ExtractorEventType.AttachmentExtractionDelayed, {
  delay: 30,  // Delay in seconds
});
```

```
await adapter.emit(ExtractorEventType.AttachmentExtractionError, {
  error: { message: "Informative error message" },
});
```

The snap-in must always emit exactly one response event.

> **Migration note (v1.16.0):** The default `streamAttachments` implementation automatically
> respects `adapter.isTimeout` and stops streaming when the soft timeout is reached.
> If implementing custom attachment processing with `processors`, check `adapter.isTimeout`
> in your iterator loop and return early when true.
> See the [full release notes](https://github.com/devrev/adaas-sdk/releases/tag/v1.16.0) for details.

## [Local and inaccessible attachment URLs](#local-and-inaccessible-attachment-urls)

When the external system stores attachments at local or internal URLs, such as, on-premise data stores like `http://localhost:8080/files/...` or `http://192.168.1.50/attachments/...`, the AirSync SDK cannot reach these URLs during the attachments extraction phase. Failed downloads are retried with exponential back-off, which can cause the `START_EXTRACTING_ATTACHMENTS` phase to stall for extended periods.

To avoid this, snap-in developers must validate and filter attachment URLs during the **data extraction phase**, before they are pushed to the attachments repository. Exclude attachments with unreachable URLs to ensure that only publicly accessible attachments are sent to the attachments extraction phase.

In your data extraction worker, filter out attachments with URLs pointing to local or otherwise inaccessible addresses before pushing them to the attachments repository.

If attachments with inaccessible URLs are not filtered out before the
attachments extraction phase, each failed download will be retried with
exponential back-off, significantly slowing down the entire sync process.

Last updated on

[Data extraction

Previous Page](/airsync/data-extraction)[Customize attachment processing

Next Page](/airsync/customize-attachment-processing)

## Source
- DevRev developer docs: [Attachments extraction](https://developer.devrev.ai/airsync/extract-attachments)
