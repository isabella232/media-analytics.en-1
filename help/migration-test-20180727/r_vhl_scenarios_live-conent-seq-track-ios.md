---
description: null
seo-description: null
seo-title: Live main content with sequential tracking
title: Live main content with sequential tracking
uuid: fac50fc3-409c-4d8b-afc4-83366aa34dc2
index: y
internal: n
snippet: y
translate: y
---

# Live main content with sequential tracking


><a id="fig_65D741D8180845E3BD58C248DD5083C6"></a> ![](graphics/ios-live-noads-multiplesessions.png) 
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
>//    frame of main content is rendered on the screen. 
>[_mediaHeartbeat trackPlay]; 
>....... 
>....... 
>  
>// 3. Call trackComplete when the playback reaches the end of session,  
>//    i.e., when the video completes and finishes playing the first 
>//    episode/session. 
>[_mediaHeartbeat trackComplete]; 
>....... 
>....... 
>  
>// 4. Call trackSessionEnd to end session 1 
>[_mediaHeartbeat trackSessionEnd]; 
>........ 
>........ 
>  
>// Start tracking session 2 / episode 2 of the same live stream, No need to  
>// reinstantiate mediaHeartbeat instance for tracking sesison 2. 
> 
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
>// 5. Call trackSessionStart when the playhead reaches a point that denotes  
>//    start of session 2 
>[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
>...... 
>...... 
>   
>// 6. Call trackPlay to start tracking session 2 playback 
>[_mediaHeartbeat trackPlay]; 
>....... 
>....... 
>   
>// 7. Call trackComplete when the playback reaches the end of session 2,  
>//    i.e., when the video completes and finishes playing. 
>[_mediaHeartbeat trackComplete]; 
>........ 
>........ 
>   
>// 8. Call trackSessionEnd to end the session 2 
>[_mediaHeartbeat trackSessionEnd]; 
>........ 
>........ 
>  
>// Continue tracking further sessions in live stream similarly if required 
>
>```

