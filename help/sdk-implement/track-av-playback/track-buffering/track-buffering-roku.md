---
seo-title: Track buffering on Roku
title: Track buffering on Roku
uuid: 6666b270-9aa3-42ff-95a8-f12502022d47
index: y
internal: n
snippet: y
---

# Track buffering on Roku{#track-buffering-on-roku}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs](../../../sdk-implement/download-sdks.md).

**Buffer tracking constants:**

|  Constant name  | Description  |
|---|---|
| `BufferStart`  | Constant for tracking Buffer Start event  |
| `BufferComplete`  | Constant for tracking Buffer Complete event  |

**Implement**

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event. 

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_START, bufferInfo, bufferContextData)
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_COMPLETE, bufferInfo, bufferContextData)
   ```

See the tracking scenario [VOD playback with buffering](../../../sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
