---
seo-title: Track Core Playback on Android
title: Track Core Playback on Android
uuid: ff240c99-b1a6-4c09-8371-132f8d1ff4b1
index: y
internal: n
snippet: y
translate: y
---

# Track Core Playback on Android

>[!IMPORTANT]
>
>This documentation covers tracking in version 2.x of the SDK. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guide for Android here: [](../../sdk-implement/download-sdks.md)

1. **Initial tracking setup -** Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance using the video information for video name, video ID, video length, and stream type. 

   ** `MediaObject` reference:** 

   |  Variable Name  | Description  | Required  |
   |---|---|---|
   |  `name`  | Video name  | Yes  |
   |  `mediaid`  | Video unique identifier  | Yes  |
   |  `length`  | Video length  | Yes  |
   |  `streamType`  | Stream type (e.g., `MediaHeartbeat.StreamType.VOD`)  | Yes  |

   ** `StreamType` constants:** 

   |  Constant Name  | Description  |
   |---|---|
   |  `VOD`  | Stream type for Video on Demand.  |
   |  `LIVE`  | Stream type for LIVE content.  |
   |  `LINEAR`  | Stream type for LINEAR content.  |

   The general format for creating the `MediaObject` is `createMediaObject(<VIDEO_NAME>, <VIDEO_ID>, <VIDEO_LENGTH>, <STREAM_TYPE>);` 

   ```
   MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
       <VIDEO_NAME>,  
       <MEDIA_ID>,  
       <VIDEO_LENGTH>,  
       MediaHeartbeat.StreamType.VOD 
   );
   ```

1. **Attach video metadata -** Optionally attach standard and/or custom video metadata objects to the video tracking session through context data variables.

    * 
    
      **Standard video metadata -** 
    
      >[!NOTE]
      >
      >Attaching the standard video metadata object to the media object is optional.

      Instantiate a standard video metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example:     
    
      ```java    
      // Sample code to set standard Video Metadata 
      Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
      standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
      standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
      standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
      mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata); 
      
      ```

        * **Video metadata keys API Reference -** [Standard metadata keys - Android](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
        
        * **API Reference -** [](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/android/index.html)

      See the comprehensive list of video metadata here: [](../../metrics-and-metadata/audio-video-parameters.md)

    * 
    
      **Custom metadata -** Create a variable object for the custom variables and populate with the data for this video. For example:     
    
      ```java    
      HashMap<String, String> videoMetadata =  
        new HashMap<String, String>(); 
      videoMetadata.put("isUserLoggedIn", "false"); 
      videoMetadata.put("tvStation", "Sample TV Station"); 
      videoMetadata.put("programmer", "Sample programmer");
      ```

1. **Track the intention to start playback - **To begin tracking a video session, call `trackSessionStart` on the Media Heartbeat instance. For example: 

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, videoMetadata); 
   }
   ```

   >[!TIP]
   >
   >The second value is the custom video metadata object name that you created in step 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tracks the user intention of playback, not the beginning of the playback. This API is used to load the video data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom video metadata, simply send an empty object for the second argument in `trackSessionStart`.

1. **Track the actual start of playback - **Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call `trackPlay`: 

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **Track the completion of playback - **Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call `trackComplete`: 

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **Track the end of the session -** Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call `trackSessionEnd`: 

   ```java
   // Closes the video and/or the video completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marks the end of a video tracking session. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Track all possible pause scenarios - **Identify the event from the video player for video pause and call `trackPause`: 

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **Pause Scenarios -** Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

    * The user explicitly hits pause in the app.
    * The player puts itself into the Pause state.
    * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
    * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. For example, the user receives a call, or a pop up from another application occurs, but you want the application to keep the session alive to give the user the opportunity to resume the video from the point of interruption.

1. Identify the event from the player for video play and/or video resume from pause and call `trackPlay`. 

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the video playback resumes.

1. Listen for playback seeking events from the media player. On seek start event notification, track seeking using the `SeekStart` event. 

   ```
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event. 

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event. 

   ```
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. On buffer complete notification from media player, track the end of buffering using the `BufferComplete` event. 

   ```
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

See the sample player included with the Android SDK for a complete tracking example. 
