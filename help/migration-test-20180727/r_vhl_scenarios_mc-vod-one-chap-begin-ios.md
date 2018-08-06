---
description: In this scenario, VOD content is played back with one chapter at the beginning of the playback.
seo-description: In this scenario, VOD content is played back with one chapter at the beginning of the playback.
seo-title: Playback with one chapter at the beginning
title: Playback with one chapter at the beginning
uuid: 759a9f6e-a0cf-4564-9419-e71ef1ac9614
index: y
internal: n
snippet: y
translate: y
---

# Playback with one chapter at the beginning


><a id="fig_4EB77B19F72A4AF5A1209A773E7929E8"></a> ![](graphics/pre-chapter-regular.png) 
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
>//    i.e., there is an intent to start playback. 
>[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
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
>// 2. Call ADBMediaHeartbeatEventChapterStart when the chapter starts. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
>                 mediaObject:chapterInfo  
>                 data:chapterContextData]; 
>....... 
>....... 
> 
>// 3. Call trackPlay when the playback actually starts, i.e., when the 
>//    first frame of the main content is rendered on the screen. 
>[_mediaHeartbeat trackPlay];  
>....... 
>....... 
>  
>// 4. Call ADBMediaHeartbeatEventChapterComplete when the chapter starts. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
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
>// 6. Call trackSessionEnd when the playback session is over. This method  
>//    must be called even if the user does not watch the video to completion. 
>[_mediaHeartbeat trackSessionEnd]; 
>....... 
>....... 
>
>```

