---
description: null
seo-description: null
seo-title: VOD playback with seeking in the main content
title: VOD playback with seeking in the main content
uuid: a498d225-c4eb-4b6a-a608-130dc21d57e6
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with seeking in the main content

## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}

This scenario comprises seeking in the main content during playback.

This is the same scenario as the [](../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md) scenario, but a part of the content is scrubbed through and a seek is completed from one point in main content to another point.

<table id="table_650DCE0B482249FFB01CCE36F2DCF259"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Trigger </th> 
   <th colname="col2" class="entry"> Heartbeat method </th> 
   <th colname="col3" class="entry"> Network calls </th> 
   <th colname="col4" class="entry"> Notes </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> User clicks <span class="uicontrol"> Play </span> </td> 
   <td colname="col2"> <span class="codeph"> trackSessionStart </span> </td> 
   <td colname="col3"> Analytics Content Start, Heartbeat Content Start </td> 
   <td colname="col4"> The measurement library is unaware that there is a pre-roll ad, so these network calls are identical to the <a href="../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> First frame of the content plays. </td> 
   <td colname="col2"> <span class="codeph"> trackPlay </span> </td> 
   <td colname="col3"> Heartbeat Content Play </td> 
   <td colname="col4"> When chapter content plays before main content, the Heartbeats start when the chapter starts. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Content plays </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> Content Heartbeats </td> 
   <td colname="col4"> This network call is exactly the same as the <a href="../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> User begins seek operation on content </td> 
   <td colname="col2"> <span class="codeph"> trackSeekStart </span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"> No heartbeats go out till seek is complete, for example, <span class="codeph"> trackSeekComplete </span> is called. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seek operation completes </td> 
   <td colname="col2"> <span class="codeph"> trackSeekComplete </span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"> Heartbeats begin to go out since seek is complete. <p>Tip:  The playhead value should represent the correct new playhead after the seek. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Content is complete </td> 
   <td colname="col2"> <span class="codeph"> trackComplete </span> </td> 
   <td colname="col3"> Heartbeat Content Complete </td> 
   <td colname="col4"> This network call is exactly the same as the <a href="../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Session Over </td> 
   <td colname="col2"> <span class="codeph"> trackSessionEnd </span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"> <span class="codeph"> SessionEnd </span> means that the end of a viewing session has been reached. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>

## Sample Code {#section_q2d_wcj_x2b}

In this scenario, the user is seeking when the main content is being played.

<a id="fig_F8759D2BD8374E99AC2A90E57961FB0C"></a>

![](assets/seek-main-to-main.png)

* **Android -** 

  To view this scenario in Android, set up the following code:

  ```java
  // Set up mediaObject 
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
   
  // 2. Call trackPlay() when the playback actually starts, i.e., whn the first frame  
  //    of the main content is rendered on the screen.  
  _mediaHeartbeat.trackPlay(); 
   
  ....... 
  ....... 
   
  // 3. Track the MediaHeartbeat.Event.SeekStart event when the user begins to seek.  
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   
  ....... 
  ....... 
   
  // 4. Track the MediaHeartbeat.Event.SeekComplete event when the user completes seeking 
  _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   
  ....... 
  ....... 
   
  // 5. Call trackComplete() when the playback reaches the end, i.e., when the video 
  //    completes and finishes playing. 
  _mediaHeartbeat.trackComplete(); 
   
  ........ 
  ........ 
   
  // 6. Call trackSessionEnd() when the playback session is over. This method must be  
  //    called even if the user does not watch the video to completion.  
  _mediaHeartbeat.trackSessionEnd(); 
   
  ........ 
  ........ 
  
  ```

* **iOS -** 

  To view this scenario in iOS, set up the following code: 

  ```
  // Set up mediaObject 
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME o 
                       length:VIDEO_LENGTH  
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 
     
  NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
  [videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
  [videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
    
  // 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
  //    i.e., there is an intent to start playback. 
  [_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
  ....... 
  ....... 
    
  // 2. Call trackPlay when the playback actually starts, i.e., when the 
  //    first frame of the main content is rendered on the screen. 
  [_mediaHeartbeat trackPlay];  
  ....... 
  ....... 
   
  // 3. Track the trackEvent:ADBMediaHeartbeatEventSeekStart event when the user  
  //    begins to seek out of the chapter with the intent to skip it. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                   mediaObject:nil  
                   data:nil]; 
  ....... 
  ....... 
    
  // 4. Track the trackEvent:ADBMediaHeartbeatEventSeekComplete event when the  
  //    user seeks out of the chapter with the intent to skip it. 
  [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                   mediaObject:nil  
                   data:nil]; 
  ....... 
  ....... 
    
  // 5. Call trackComplete when the playback reaches the end, i.e., completes  
  //    and finishes playing. 
  [_mediaHeartbeat trackComplete]; 
  ....... 
  ....... 
   
  // 6. Call trackSessionEnd when the playback session is over. This method must  
  //    be called even if the user does not watch the video to completion. 
  [_mediaHeartbeat trackSessionEnd]; 
  ....... 
  ....... 
  
  ```

* **JavaScript -** 

  To view this scenario, enter the following text: 

  ```js
  // Set up mediaObject 
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
   
  // 2. Call trackPlay() when the playback actually starts, i.e., when the  
  //    first frame of the ad video is rendered on the screen. 
  this._mediaHeartbeat.trackPlay(); 
   
  ....... 
  ....... 
   
  // 3. Track the MediaHeartbeat.Event.SeekStart event when the user  
  //    begins to seek. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   
  ....... 
  ....... 
   
  // 4. Track the MediaHeartbeat.Event.SeekComplete event when the user  
  //    completes seeking. 
  this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   
  ....... 
  ....... 
   
  // 5. Call trackComplete() when the playback reaches the end, i.e., when 
  //    playback completes and finishes playing. 
  this._mediaHeartbeat.trackComplete(); 
   
  ........ 
  ........ 
   
  // 6. Call trackSessionEnd() when the playback session is over. This method must be called  
  //    even if the user does not watch the video to completion. 
  this._mediaHeartbeat.trackSessionEnd(); 
   
  ........ 
  ........ 
  
  ```

