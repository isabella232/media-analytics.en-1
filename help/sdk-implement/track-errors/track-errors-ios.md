---
seo-title: Track errors on iOS
title: Track errors on iOS
uuid: 18ea93d3-5948-4375-bcdb-72309268e38d
index: y
internal: n
snippet: y
---

# Track errors on iOS{#track-errors-on-ios}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs](../../sdk-implement/download-sdks.md).

**Implement**

1. Track video player errors: 

   ```
   - (void)onPlayerError:(NSNotification *)notification { 
       [_mediaHeartbeat trackError:@"videoErrorId"]; 
   }
   ```

>[!NOTE]
>
>Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

