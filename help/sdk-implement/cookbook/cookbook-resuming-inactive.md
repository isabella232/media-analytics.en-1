---
seo-title: Resuming inactive sessions
title: Resuming inactive sessions
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
index: y
internal: n
snippet: y
---

# Resuming inactive sessions{#resuming-inactive-sessions}

**Long Pauses -**

The Media SDK automatically tracks how long the video playback is in one of the following inactive states:

* Paused
* Seeking
* Stalled
* Buffering

If a video tracking session remains in an inactive state for longer than 30 minutes, the session will automatically be closed. If the user resumes after a previously inactive video tracking session ( `trackPlay`), Media Heartbeat automatically creates a new video session using the previously used video information and metadata, and sends a resume heartbeat event. For more information, see [Audio and video parameters](../../metrics-and-metadata/audio-video-parameters.md).

**Manually resume previously closed session -**

The Media SDK will only automatically resume sessions if the application was not closed. If the application stores user data and has the capability to resume a previously closed video, it is possible to manually trigger a resume event. When starting the video tracking session, set the optional Video Resumed property.

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
       
      // Set to true if this is a resume playback scenario 
      mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, true);
       
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
   
      //Set to YES if this user is resuming a previously closed media session 
      [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeyVideoResumed];
   
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

      // Set to true if this user is resuming a previously closed media session 
      mediaObject.setValue(MediaObjectKey.VideoResumed, true); 
      this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
  };
  ```

