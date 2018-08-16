---
description: null
seo-description: null
seo-title: Track buffering
title: Track buffering
uuid: c72298e3-c003-4769-a96a-5279879cfcef
index: y
internal: n
snippet: y
translate: y
---

# Track buffering

Here is the ` ADBMediaHeartbeatEvent` buffer tracking constants reference: 



|  Constant name  | Description  |
|---|---|
|  ` ADBMediaHeartbeatEventBufferStart`  | Constant for tracking Buffer Start event  |
|  ` ADBMediaHeartbeatEventBufferComplete`  | Constant for tracking Buffer Complete event  |


>1. Listen for the playback buffering events from media player. On buffer start event notification, track buffering using ` ADBMediaHeartbeatEventBufferStart` event.
>
>   ```
>   - (void)onBufferStart:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
>                        mediaObject:nil  
>                        data:nil]; 
>   } 
>   
>   ```
>
>1. On buffer complete notification from media player, track the end of buffering using ` ADBMediaHeartbeatEventBufferComplete` event.
>
>   ```
>   - (void)onBufferComplete:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
>                        mediaObject:nil  
>                        data:nil]; 
>   } 
>   
>   ```
>
