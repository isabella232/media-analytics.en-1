---
description: In this scenario, buffering occurs when the VOD content is played back.
seo-description: In this scenario, buffering occurs when the VOD content is played back.
seo-title: Playback with buffering in the main content
title: Playback with buffering in the main content
uuid: 65d875b0-5106-42bb-be4d-6a087e817369
index: y
internal: n
snippet: y
translate: y
---

# Playback with buffering in the main content


><a id="fig_E4644A6B9940403BA81AC82585C4C1D7"></a> ![](graphics/buffer-regular-content.png) 
>To view this scenario in iOS, set up the following code: >
>```
>// Set up mediaObject 
>ADBMediaObject *mediaObject =  
>  [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
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
>// 2. Call trackPlay when the playback actually starts, i.e., when the first  
>//    frame of the main content is rendered on the screen. 
>[_mediaHeartbeat trackPlay];  
>....... 
>....... 
> 
>// 3. Track the trackEvent:ADBMediaHeartbeatEventBufferStart event when the  
>//    video player goes in buffering state and begins to buffer content. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
>                 mediaObject:nil  
>                 data:nil]; 
>....... 
>....... 
>  
>// 4. Track the trackEvent:ADBMediaHeartbeatEventBufferComplete event when  
>//    the video player goes in buffering state and begins to buffer content. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
>                 mediaObject:nil  
>                 data:nil]; 
>....... 
>....... 
>  
>// 5. Call trackComplete when the playback reaches the end, i.e., when the 
>//    video completes and finishes playing. 
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

