---
description: null
seo-description: null
seo-title: Live content playback
title: Live content playback
uuid: a32ec900-c9e0-4c32-9486-acc7ebaee0e6
index: y
internal: n
snippet: y
translate: y
---

# Live content playback


><a id="fig_65D741D8180845E3BD58C248DD5083C6"></a> ![](graphics/live-content-playback.png) 
>Here is the expected API call order: >
>```
>// Set up mediaObject 
>ADBMediaObject *mediaObject =  
>  [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
>                     length:VIDEO_LENGTH  
>                     streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
>   
>NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
>[videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
>[videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
>   
>// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
>//    i.e., there is an intent to start playback. 
>[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
>...... 
>...... 
>   
>// 2. Call trackPlay when the playback actually starts, i.e., when the first  
>//    frame of the main content is rendered on the screen. 
>[_mediaHeartbeat trackPlay]; 
>....... 
>....... 
>   
>// 3. Call trackSessionEnd when user ends the playback session. Since the user  
>//    does not watch live video to completion, there is no need to call  
>//    trackComplete. 
>[_mediaHeartbeat trackSessionEnd]; 
>........ 
>........ 
>
>```

