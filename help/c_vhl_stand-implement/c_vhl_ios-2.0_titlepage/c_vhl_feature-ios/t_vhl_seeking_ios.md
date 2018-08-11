---
description: null
seo-description: null
seo-title: Seeking
title: Seeking
uuid: 860e993e-cacb-440e-a544-8d609bec69dc
index: y
internal: n
snippet: y
translate: y
---

# Seeking

Here is the ` ADBMediaHeartbeatEvent` seek tracking constants reference: 



|  Constant name  | Description  |
|---|---|
|  ` ADBMediaHeartbeatEventBufferStart`  | Constant for tracking Buffer Start event  |
|  ` ADBMediaHeartbeatEventBufferComplete`  | Constant for tracking Buffer Complete event  |


>1. Listen for the playback seeking events from media player. On seek start event notification, track seeking using ` ADBMediaHeartbeatEventSeekStart` event.
>
>   ```
>   - (void)onSeekStart:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
>                        mediaObject:nil  
>                        data:nil]; 
>   } 
>   
>   ```
>
>1. On seek complete notification from media player, track the end of seeking using ` ADBMediaHeartbeatEventSeekComplete` event.
>
>   ```
>   - (void)onSeekComplete:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
>                        mediaObject:nil  
>                        data:nil]; 
>   } 
>   
>   ```
>
