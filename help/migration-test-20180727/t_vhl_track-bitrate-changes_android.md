---
description: null
seo-description: null
seo-title: QoS updates
title: QoS updates
uuid: 6ea71370-dd20-41c7-a9e0-3b9a909afd01
index: y
internal: n
snippet: y
translate: y
---

# QoS updates

Here is the ` MediaHeartbeat.Event` QoS tracking constants reference: 


|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.Event.BitrateChange`  | Constant for tracking bitrate change.  |


>1. Listen for the QoS updates from the media player, and on a bitrate change event notification, create a the ` MediaObject` with QoS information.
>   ` MediaObject` (QoS Object) reference: 

>   |  Variable  | Description  | Required  |
>   |---|---|---|
>   |  ` bitrate`  | Current bitrate  | Yes  |
>   |  ` startupTime`  | Startup time  | Yes  |
>   |  ` fps`  | FPS value  | Yes  |
>   |  ` droppedFrames`  | Number of dropped frames  | Yes  |

>
>   ```
>   java>   // Replace <BITRATE> with the updated bitrate value 
>   // Replace <STARTUP_TIME> with a startup time value 
>   // Replace <FPS> with the fps value 
>   // Replace <DROPPED_FRAMES> with dropped frames 
>   MediaObject qosObject =  
>     MediaHeartbeat.createQoSObject(<BITRATE>,  
>                                    <STARTUP_TIME>,  
>                                    <FPS>,  
>                                    <DROPPED_FRAMES>); 
>   
>   ```

>
>1. Track bitrate change using ` MediaHeartbeat.Event.BitrateChange` event.
>
>   ```
>   java>   public void onBitrateChange(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject, null); 
>   } 
>   
>   ```
>
