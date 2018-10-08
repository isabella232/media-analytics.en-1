---
description: null
seo-description: null
seo-title: Track Errors on Chromecast
title: Track Errors on Chromecast
uuid: 2598fb8f-929b-4cc5-9d6f-7613c36f7de2
index: y
internal: n
snippet: y
translate: y
---

# Track Errors on Chromecast

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Implement**

1. Track video player errors: [trackError](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

