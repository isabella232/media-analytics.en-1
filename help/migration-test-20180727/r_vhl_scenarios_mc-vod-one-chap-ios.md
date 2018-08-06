---
description: In this scenario, the VOD content is played back as a chapter.
seo-description: In this scenario, the VOD content is played back as a chapter.
seo-title: Playback with one chapter
title: Playback with one chapter
uuid: 1fc11220-bb84-4147-9e01-15158c7d1828
index: y
internal: n
snippet: y
translate: y
---

# Playback with one chapter


><a id="fig_553EA0F2821440EBB39353F627463913"></a> ![](graphics/chapter-regular-playback.png) 
>To view this scenario in iOS, set up the following code: >
>```
>when the user clicks Play 
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
>//    i.e., when there is an intent to start playback. 
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
>// Chapter 
>NSMutableDictionary *chapterContextData = [[NSMutableDictionary alloc] init]; 
>[chapterContextData setObject:CONTEXT_DATA_VALUE forKey:CONTEXT_DATA_KEY]; 
>  
>id chapterInfo =  
>  [ADBMediaHeartbeat createChapterObjectWithName:CHAPTER_NAME  
>                     position:CHAPTER_POSITION  
>                     length:CHAPTER_LENGTH  
>                     startTime:CHAPTER_START_TIME]; 
>      
>// 3. Track the ADBMediaHeartbeatEventChapterStart event when the chapter  
>//    starts to play. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
>                 mediaObject:chapterInfo  
>                 data:chapterContextData]; 
>....... 
>....... 
>  
>// 4. Track the ADBMediaHeartbeatEventChapterComplete event when the chapter  
>//    finishes playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
>                 mediaObject:nil  
>                 data:nil];  
>....... 
>....... 
>// 5. Call trackComplete when the playback reaches the end, i.e., when the  
>//    video completes and finishes playing. 
>[_mediaHeartbeat trackComplete]; 
>....... 
>....... 
>// 6. Call trackSessionEnd when the playback session is over. This method must  
>//    be called even if the user does not watch the video to completion. 
>[_mediaHeartbeat trackSessionEnd]; 
>....... 
>....... 
>
>```

