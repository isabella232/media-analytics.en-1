---
description: null
seo-description: null
seo-title: QoS updates on iOS
title: QoS updates on iOS
uuid: cf749aa0-b9eb-437b-8fe8-448861464a6f
index: y
internal: n
snippet: y
translate: y
---

# QoS updates on iOS

Here is the ` ADBMediaHeartbeatEvent` QoS tracking constants reference: 



|  Constant name  | Description  |
|---|---|
|  ` ADBMediaHeartbeatEventBitrateChange`  | Constant for tracking Bitrate change  |


>1. Listen for the QoS updates from media player.
>1. On bitrate change event notification, create ` ADBMediaObject` with QoS information.
>   ` ADBMediaObject` (QoS Object) Reference: 



>   |  Variable  | Description  | Required  |
>   |---|---|---|
>   |  ` bitrate`  | Current bitrate  | Yes  |
>   |  ` startupTime`  | Startup time  | Yes  |
>   |  ` fps`  | FPS value  | Yes  |
>   |  ` droppedFrames`  | Number of dropped frames  | Yes  |

>
>   ```
>   //Replace <BITRATE> with the updated bitrate value 
>   //Replace <STARTUP_TIME> with a startup time value 
>   //Replace <FPS> with the fps value 
>   //Replace <DROPPED_FRAMES> with dropped frames 
>    
>   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
>                                     startupTime:[STARTUP_TIME]  
>                                     fps:[FPS]  
>                                     droppedFrames:[DROPPED_FRAMES]]; 
>   
>   ```

>
>1. Track bitrate change using the ` ADBMediaHeartbeatEventBitrateChange` event.
>
>   ```
>   - (void)onBitrateChange:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
>                        mediaObject:qosObject  
>                        data:nil]; 
>   } 
>   
>   ```
>
