---
seo-title: Track seeking on iOS
title: Track seeking on iOS
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
index: y
internal: n
snippet: y
---

# Track seeking on iOS{#track-seeking-on-ios}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../../sdk-implement/download-sdks.md).

**Seek tracking constants:**

|  Constant name  | Description  |
|---|---|
|  `ADBMediaHeartbeatEventSeekStart`  | Constant for tracking Seek Start event.  |
|  `ADBMediaHeartbeatEventSeekComplete`  | Constant for tracking Seek Complete event.  |

**Implement**

1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the `SeekStart` event: 

   ```
   - (void)onSeekStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event: 

   ```
   - (void)onSeekComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

See the tracking scenario [](../../../sdk-implement/tracking-scenarios/vod-seeking.md) for more information.
