---
description: null
seo-description: null
seo-title: QoS updates on JavaScript
title: QoS updates on JavaScript
uuid: 948f72de-ca32-4d1e-afe3-347241cfbf49
index: y
internal: n
snippet: y
translate: y
---

# QoS updates on JavaScript

Here is the ` MediaHeartbeat.Event` QoS tracking constants reference: 



|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.Event.BitrateChange`  | Constant for tracking Bitrate change  |

Implement QoS tracking:

>1. Listen for the QoS updates from media player, and on bitrate change event notification, create ` MediaObject` with QoS information.
>   ADBMediaObject (QoS Object) Reference: 

>   |  Variable  | Description  | Required  |
>   |---|---|---|
>   |  ` bitrate`  | Current bitrate  | Yes  |
>   |  ` startupTime`  | Startup time  | Yes  |
>   |  ` fps`  | FPS value  | Yes  |
>   |  ` droppedFrames`  | Number of dropped frames  | Yes  |

>
>   ```
>   js>   // Replace <bitrate>, <startuptime>, <fps> and  
>   // <droppeFrames> with the current playback QoS values.  
>   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
>                                                  <startuptime>,  
>                                                  <fps>,  
>                                                  <droppedFrames>); 
>   
>   ```

>
>1. Track bitrate change using the ` MediaHeartbeat.Event.BitrateChange` event.
>
>   ```
>   js>   _onBitrateChange = function() { 
>       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
>   }; 
>   
>   ```
>
