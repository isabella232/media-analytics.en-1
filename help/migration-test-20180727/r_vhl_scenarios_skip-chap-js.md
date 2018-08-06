---
description: null
seo-description: null
seo-title: Playback with a skipped chapter
title: Playback with a skipped chapter
uuid: bc292006-3307-498d-a66a-abb588985647
index: y
internal: n
snippet: y
translate: y
---

# Playback with a skipped chapter


<a id="section_6631CA351745493DA964D198A6C37D51"></a>

<a id="fig_B5B18205EFE144B5A00B268B1A541010"></a> ![](graphics/chapter-skip.png) 
To view this scenario in JavaScript, enter the following text: 
```
js// Set up mediaObject 
var mediaInfo = MediaHeartbeat.createMediaObject( 
    Configuration.VIDEO_NAME,  
    Configuration.VIDEO_ID,  
    Configuration.VIDEO_LENGTH,  
    MediaHeartbeat.StreamType.VOD 
); 
 
var videoMetadata = { 
    CUSTOM_KEY_1 : CUSTOM_VAL_1,  
    CUSTOM_KEY_2 : CUSTOM_VAL_2,  
    CUSTOM_KEY_3 : CUSTOM_VAL_3 
 
}; 
 
// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
 
...... 
...... 
 
// Chapter 
var chapterMetadata = { 
    CUSTOM_KEY_1 : CUSTOM_VAL_1 
}; 
 
var chapterDataInfo =  
  MediaHeartbeat.createChapterObject(CHAPTER_NAME,  
                                    CHAPTER_POSITION,  
                                    CHAPTER_LENGTH,  
                                    CHAPTER_START_TIME); 
 
// 2. Track the MediaHeartbeat.Event.ChapterStart event when the chapter starts to play. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                chapterDataInfo,  
                                chapterMetadata); 
 
....... 
....... 
 
// 3. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of the main content is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 
 
....... 
....... 
 
// 4. Track the MediaHeartbeat.Event.SeekStart event when the user begins  
//    to seek out of the chapter with the intent to skip it. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
 
....... 
....... 
 
// 5. Track the MediaHeartbeat.Event.SeekComplete event when the user seeks  
//    out of the chapter with the intent to skip it. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
 
....... 
....... 
 
// 6. Track the MediaHeartbeat.Event.ChapterSkip event because the user  
//    skipped the chapter by seeking out of it in the steps above. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
 
....... 
....... 
 
// 7. Call trackComplete() when the playback reaches the end, i.e., completes  
//    and finishes playing. 
this._mediaHeartbeat.trackComplete(); 
 
........ 
........ 
 
// 8. Call trackSessionEnd() when the playback session is over. This method must be  
//    called even if the user does not watch the video to completion. 
this._mediaHeartbeat.trackSessionEnd(); 
 
........ 
........ 

```

