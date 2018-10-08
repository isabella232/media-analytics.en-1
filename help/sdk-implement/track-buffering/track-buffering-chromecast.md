---
description: null
seo-description: null
seo-title: Track Buffering on Chromecast
title: Track Buffering on Chromecast
uuid: 00e3b085-53c9-4d17-8a63-be42ac91ba1d
index: y
internal: n
snippet: y
translate: y
---

# Track Buffering on Chromecast

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Buffer tracking constants:**

|  Constant name  | Description  |
|---|---|
|  `BufferStart`  | Constant for tracking Buffer Start event  |
|  `BufferComplete`  | Constant for tracking Buffer Complete event  |

**Implement**

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event: [trackEvent](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/chromecast/ADBMobile.media.html#.trackEvent) 

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event: [trackEvent](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/chromecast/ADBMobile.media.html#.trackEvent) 

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

