---
description: null
seo-description: null
seo-title: Track Errors on Roku
title: Track Errors on Roku
uuid: 36d81230-f527-4cf7-bf1e-17c1e8f7062a
index: y
internal: n
snippet: y
translate: y
---

# Track Errors on Roku

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Implement**

1. Track video player errors: 

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                                        ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

