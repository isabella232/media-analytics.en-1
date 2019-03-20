---
seo-title: Track buffering on iOS
title: Track buffering on iOS
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2

---

# Track buffering on iOS{#track-buffering-on-ios}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../../sdk-implement/download-sdks.md)

## Buffer tracking constants


|  Constant name  | Description&nbsp;&nbsp;&nbsp;&nbsp;  |
|---|---|
|  `ADBMediaHeartbeatEventBufferStart`  | Constant for tracking Buffer Start event  |
|  `ADBMediaHeartbeatEventBufferComplete`  | Constant for tracking Buffer Complete event  |

## Implement buffering

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event: 

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event: 

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

See the tracking scenario [VOD playback with buffering](../../../sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
