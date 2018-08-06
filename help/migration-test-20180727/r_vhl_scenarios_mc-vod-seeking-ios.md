---
description: In this scenario, the user is seeking when the main content is being played.
seo-description: In this scenario, the user is seeking when the main content is being played.
seo-title: Playback with seeking in the main content
title: Playback with seeking in the main content
uuid: ed7d5827-6558-491f-ac9a-c36ffa0edecf
index: y
internal: n
snippet: y
translate: y
---

# Playback with seeking in the main content


><a id="fig_F8759D2BD8374E99AC2A90E57961FB0C"></a> ![](graphics/seek-main-to-main.png) 
>To view this scenario in iOS, set up the following code: >
>```
>// Set up mediaObject 
>ADBMediaObject *mediaObject =  
>  [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME o 
>                     length:VIDEO_LENGTH  
>                     streamType:ADBMediaHeartbeatStreamTypeVOD]; 
>   
>NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
>[videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
>[videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
>  
>// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
>//    i.e., there is an intent to start playback. 
>[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
>....... 
>....... 
>  
>// 2. Call trackPlay when the playback actually starts, i.e., when the 
>//    first frame of the main content is rendered on the screen. 
>[_mediaHeartbeat trackPlay];  
>....... 
>....... 
> 
>// 3. Track the trackEvent:ADBMediaHeartbeatEventSeekStart event when the user  
>//    begins to seek out of the chapter with the intent to skip it. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
>                 mediaObject:nil  
>                 data:nil]; 
>....... 
>....... 
>  
>// 4. Track the trackEvent:ADBMediaHeartbeatEventSeekComplete event when the  
>//    user seeks out of the chapter with the intent to skip it. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
>                 mediaObject:nil  
>                 data:nil]; 
>....... 
>....... 
>  
>// 5. Call trackComplete when the playback reaches the end, i.e., completes  
>//    and finishes playing. 
>[_mediaHeartbeat trackComplete]; 
>....... 
>....... 
> 
>// 6. Call trackSessionEnd when the playback session is over. This method must  
>//    be called even if the user does not watch the video to completion. 
>[_mediaHeartbeat trackSessionEnd]; 
>....... 
>....... 
>
>```

