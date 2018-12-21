---
seo-title: Track errors on Chromecast
title: Track errors on Chromecast
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a

---

# Track errors on Chromecast{#track-errors-on-chromecast}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs](../../sdk-implement/download-sdks.md).

**Implement**

1. Track video player errors: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

