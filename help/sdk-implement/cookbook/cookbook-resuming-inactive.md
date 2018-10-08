---
description: null
seo-description: null
seo-title: Resuming Inactive Sessions
title: Resuming Inactive Sessions
uuid: 645e53a2-29d8-448e-b04a-884960b37fe3
index: y
internal: n
snippet: y
translate: y
---

# Resuming Inactive Sessions

**Long Pauses -**

The VA library automatically tracks how long the video playback is in one of the following inactive states:

* Paused
* Seeking
* Stalled
* Buffering

If a video tracking session remains in an inactive state for longer than 30 minutes, the session will automatically be closed. If the user resumes after a previously inactive video tracking session ( `trackPlay`), Media Heartbeat automatically creates a new video session using the previously used video information and metadata, and sends a resume heartbeat event. For more information, see [](../../metrics-and-metadata/audio-video-parameters.md).

**Manually Resume Previously Closed Session -**

The VA library will only automatically resume sessions if the application was not closed. If the application stores user data and has the capability to resume a previously closed video, it is possible to manually trigger a resume event. When starting the video tracking session, set the optional Video Resumed property.

* **Android:** 

  ```java
  // Set MediaHeartbeat.MediaObjectKey.VideoResumed to true 
  public void onVideoLoad(Observable observable, Object data) { 
   
  // Replace <VIDEO_NAME> with the video name. 
  // Replace <VIDEO_ID> with a video unique identifier. 
  // Replace <VIDEO_LENGTH> with the video length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <VIDEO_NAME>,  
      <VIDEO_ID>,  
      <VIDEO_LENGTH>,  
      MediaHeartbeat.StreamType.VOD 
  ); 
   
<b> 
       // Set to true if this is a resume playback scenario 
       mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, true); </b> 
   
      _heartbeat.trackSessionStart(mediaInfo, videoMetadata); 
  }
  ```

* **iOS:** 

  ```
  - (void)onMainVideoLoaded:(NSNotification *)notification { 
      //Replace <VIDEO_NAME> with the video name. 
      //Replace <VIDEO_ID> with a video unique identifier. 
      //Replace <VIDEO_LENGTH> with the video length.     
      ADBMediaObject *mediaObject =  
        [ADBMediaHeartbeat createMediaObjectWithName:<VIDEO_NAME> 
                           mediaId:<VIDEO_ID> 
                           length:<VIDEO_LENGTH> 
                           streamType:ADBMediaHeartbeatStreamTypeVOD]; 
   
<b> 
       //Set to YES if this user is resuming a previously closed video session 
       [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeyVideoResumed];</b> 
   
      [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
  } 
  
  ```

* **JavaScript:** 

  ```js
  _onVideoLoad = function () { 
      // Replace <VIDEO_NAME> with the video name. 
      // Replace <VIDEO_ID> with a video unique identifier. 
      // Replace <VIDEO_LENGTH> with the video length.  
      var mediaObject =  
        MediaHeartbeat.createMediaObject(<VIDEO_NAME>,  
                                         <VIDEO_ID,  
                                         <VIDEO_LENGTH>,  
                                         MediaHeartbeat.StreamType.VOD);

<b>    // Set to true if this user is resuming a previously closed video session 
       mediaObject.setValue(MediaObjectKey.VideoResumed, true); 
   </b> 
      this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
  };
  ```

