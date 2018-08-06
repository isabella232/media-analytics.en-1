---
description: null
seo-description: null
seo-title: Playback with a skipped chapter
title: Playback with a skipped chapter
uuid: a8b42c40-1c42-43bc-b47c-3fecb211d5a0
index: y
internal: n
snippet: y
translate: y
---

# Playback with a skipped chapter


<a id="section_2AE8066EB1F945E2B863EC0F2123E07D"></a>

<a id="fig_6DDC303ED9D14FE396EB093DF6E35882"></a> ![](graphics/chapter-skip.png) 
To view this scenario in Android, set up the following code:

```
java// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
    Configuration.VIDEO_NAME,  
    Configuration.VIDEO_ID,  
    Configuration.VIDEO_LENGTH,  
    MediaHeartbeat.StreamType.VOD 
 
); 
 
HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
 
// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
 
...... 
...... 
 
// Chapter 
HashMap<String, String> chapterMetadata = new HashMap<String, String>(); 
chapterMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
MediaObject chapterDataInfo =  
  MediaHeartbeat.createChapterObject(CHAPTER_NAME,  
                                     CHAPTER_POSITION,  
                                     CHAPTER_LENGTH,  
                                     CHAPTER_START_TIME); 
 
// 2. Track the MediaHeartbeat.Event.ChapterStart event when the chapter starts to play.  
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                           chapterDataInfo,  
                           chapterMetadata); 
 
....... 
....... 
 
// 3. Call trackPlay() when the playback actually starts, i.e., when the first frame  
//    of the main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 
 
....... 
....... 
 
// 4. Track the MediaHeartbeat.Event.SeekStart event when the user begins to seek out  
//    of the chapter with the intent to skip it.  
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
 
....... 
....... 
 
// 5. Track the MediaHeartbeat.Event.SeekComplete event when the user seeks out of the  
//    chapter with the intent to skip it.  
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
 
....... 
....... 
 
// 6. Track the MediaHeartbeat.Event.ChapterSkip event because the user skipped the  
//    chapter by seeking out of it in the steps above.  
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null); 
 
....... 
....... 
 
// 7. Call trackComplete() when the playback reaches the end, i.e., when the video 
//    completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 
 
........ 
 
........ 
 
// 8. Call trackSessionEnd() when the playback session is over. This method must be  
//    called even if the user does not watch the video to completion.  
_mediaHeartbeat.trackSessionEnd(); 
 
........ 
........ 

```

