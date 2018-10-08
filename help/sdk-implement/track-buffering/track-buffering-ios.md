---
description: null
seo-description: null
seo-title: Track Buffering on iOS
title: Track Buffering on iOS
uuid: 231000df-6359-4b0e-9cce-44129f7fe939
index: y
internal: n
snippet: y
translate: y
---

# Track Buffering on iOS

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Buffer tracking constants:**

|  Constant name  | Description  |
|---|---|
|  `BufferStart`  | Constant for tracking Buffer Start event  |
|  `BufferComplete`  | Constant for tracking Buffer Complete event  |

**Implement**

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

