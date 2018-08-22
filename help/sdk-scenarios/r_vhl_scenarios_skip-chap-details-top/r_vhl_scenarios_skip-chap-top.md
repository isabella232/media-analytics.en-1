---
description: null
seo-description: null
seo-title: Playback with a skipped chapter
title: Playback with a skipped chapter
uuid: 96bc4aef-1871-43a9-9389-27f7d3090503
index: y
internal: n
snippet: y
translate: y
---

# Playback with a skipped chapter


<a id="section_6631CA351745493DA964D198A6C37D51"></a>

<a id="fig_B5B18205EFE144B5A00B268B1A541010"></a> ![](assets/chapter-skip.png) 


* **Android - **To view this scenario in Android, set up the following code: 


  ```
  java  // Set up mediaObject 
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


* **iOS - **To view this scenario in iOS, set up the following code: 
  ```
  // Set up mediaObject 
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
                       length:VIDEO_LENGTH  
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 
     
  NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
  [videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
  [videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
    
  // 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
  //    i.e., there's an intent to start playback. 
  [_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
  ....... 
  ....... 
     
  // Chapter 
  NSMutableDictionary *chapterContextData = [[NSMutableDictionary alloc] init]; 
  [chapterContextData setObject:CONTEXT_DATA_VALUE forKey:CONTEXT_DATA_KEY]; 
     
  id chapterInfo =  
    [ADBMediaHeartbeat createChapterObjectWithName:CHAPTER_NAME  
                       position:CHAPTER_POSITION  
                       length:CHAPTER_LENGTH  
                       startTime:CHAPTER_START_TIME]; 
        
  // 2. Track the ADBMediaHeartbeatEventChapterStart event when the chapter starts. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                   mediaObject:chapterInfo  
                   data:chapterContextData]; 
  ....... 
  ....... 
   
  // 3. Call trackPlay when the playback actually starts, i.e., when the first  
  //    frame of the main content is rendered on the screen. 
  [_mediaHeartbeat trackPlay]; 
  ....... 
  ....... 
   
  // 4. Track the trackEvent:ADBMediaHeartbeatEventSeekStart event when the user  
  //    begins to seek out of the chapter with the intent to skip it. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart mediaObject:nil data:nil]; 
  ....... 
  ....... 
    
  // 5. Track the trackEvent:ADBMediaHeartbeatEventSeekComplete event when the  
  //    user seeks out of the chapter with the intent to skip it. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete mediaObject:nil data:nil]; 
  ....... 
  ....... 
    
  // 6. Track the trackEvent:ADBMediaHeartbeatEventChapterSkip event because the  
  //    user skipped the chapter by seeking out of it in the steps above. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                   mediaObject:chapterInfo  
                   data:chapterContextData]; 
  ....... 
  ....... 
     
  // 7. Call trackComplete when the playback reaches the end, i.e., when the video 
  //    completes and finishes playing. 
  [_mediaHeartbeat trackComplete]; 
  ....... 
  ....... 
   
  // 8. Call trackSessionEnd when the playback session is over. This method must  
  //    be called even if the user does not watch the video to completion. 
  [_mediaHeartbeat trackSessionEnd]; 
  ....... 
  ....... 
  
  ```


* **JavaScript - **To view this scenario in JavaScript, enter the following text: 
  ```
  js  // Set up mediaObject 
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



