---
description: null
seo-description: null
seo-title: Playback with one chapter
title: Playback with one chapter
uuid: 7a539f74-868d-413d-b386-36ef51625fe7
index: y
internal: n
snippet: y
translate: y
---

# Playback with one chapter


><a id="fig_553EA0F2821440EBB39353F627463913"></a> ![](graphics/chapter-regular-playback.png) 
>To view this scenario in Android, set up the following code: >
>```
>java>// Set up mediaObject 
>MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>    Configuration.VIDEO_NAME,  
>    Configuration.VIDEO_ID,  
>    Configuration.VIDEO_LENGTH,  
>    MediaHeartbeat.StreamType.VOD 
>); 
> 
>HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
>videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
>videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
> 
>// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
>//    i.e., there is an intent to start playback.  
>_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// 2. Call trackPlay() when the playback actually starts, i.e., first frame of the  
>//    ad video is rendered on the screen. 
>_mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// Chapter 
>HashMap<String, String> chapterMetadata = new HashMap<String, String>(); 
>chapterMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
>MediaObject chapterDataInfo =  
>  MediaHeartbeat.createChapterObject(CHAPTER_NAME,  
>                                     CHAPTER_POSITION,  
>                                     CHAPTER_LENGTH,  
>                                     CHAPTER_START_TIME); 
> 
>// 3. Track the MediaHeartbeat.Event.ChapterStart event when the chapter starts to play.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterDataInfo, chapterMetadata); 
> 
>....... 
>....... 
> 
>// 4. Track the MediaHeartbeat.Event.ChapterComplete event when the chapter finishes playing. 
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null); 
> 
>....... 
>....... 
> 
>// 5. Call trackComplete() when the playback reaches the end, i.e., completes and finishes playing. 
>_mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 6. Call trackSessionEnd() when the playback session is over. This method must be called even  
>//    if the user does not watch the video to completion.  
>_mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

