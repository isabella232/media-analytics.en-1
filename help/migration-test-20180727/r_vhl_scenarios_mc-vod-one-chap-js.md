---
description: null
seo-description: null
seo-title: Playback with one chapter
title: Playback with one chapter
uuid: 4f8caa40-e3af-4009-af04-542d41a2a888
index: y
internal: n
snippet: y
translate: y
---

# Playback with one chapter


><a id="fig_553EA0F2821440EBB39353F627463913"></a> ![](graphics/chapter-regular-playback.png) 
>To view this scenario in JavaScript, enter the following text: >
>```
>js>// Set up mediaObject 
>var mediaInfo = MediaHeartbeat.createMediaObject( 
>   Configuration.VIDEO_NAME,  
>   Configuration.VIDEO_ID,  
>   Configuration.VIDEO_LENGTH,  
>   MediaHeartbeat.StreamType.VOD 
> 
>); 
> 
>var videoMetadata = { 
>    CUSTOM_KEY_1 : CUSTOM_VAL_1,  
>    CUSTOM_KEY_2 : CUSTOM_VAL_2,  
>    CUSTOM_KEY_3 : CUSTOM_VAL_3 
>}; 
> 
>// 1. Call trackSessionStart when Play is clicked or if autoplay is used,  
>//    i.e., when there's an intent to start playback. 
>this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// Chapter 
>var chapterMetadata = { 
>    CUSTOM_KEY_1 : CUSTOM_VAL_1 
>}; 
> 
>var chapterDataInfo =  
>  MediaHeartbeat.createChapterObject(CHAPTER_NAME,  
>                                     CHAPTER_POSITION,  
>                                     CHAPTER_LENGTH,  
>                                     CHAPTER_START_TIME); 
> 
>// 2. Track the MediaHeartbeat.Event.ChapterStart event when the chapter  
>//    starts to play. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
>                                chapterDataInfo,  
>                                chapterMetadata); 
> 
>....... 
>....... 
> 
>// 3. Call trackPlay() when the playback actually starts, i.e., when the first  
>//    frame of the main content is rendered on the screen. 
>this._mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 4. Track the MediaHeartbeat.Event.ChapterComplete event when the chapter  
>//    finishes playing. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
> 
>....... 
>....... 
> 
>// 5. Call trackComplete() when the playback reaches the end, i.e., when playback   
>//    completes and finishes playing. 
>this._mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 6. Call trackSessionEnd() when the playback session is over. This method must be  
>//    called even if the user does not watch the video to completion. 
>this._mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

