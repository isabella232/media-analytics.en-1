---
seo-title: Track Core Playback on JavaScript
title: Track Core Playback on JavaScript
uuid: 64807555-0246-4b35-97e6-11dc78954c20
index: y
internal: n
snippet: y
translate: y
---

# Track Core Playback on JavaScript

>[!IMPORTANT]
>
>This documentation covers tracking in version 2.x of the SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md)

1. **Initial tracking setup -** Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance using the video information for video name, video ID, video length, and stream type.

   ** `MediaObject` reference:** 

   |  Variable Name  | Description  | Required  |
   |---|---|---|
   |  `name`  | Video name  | Yes  |
   |  `mediaid`  | Video unique identifier  | Yes  |
   |  `length`  | Video length  | Yes  |
   |  `streamType`  | Stream type (see `constants MediaHeartbeat.StreamType.VOD`)  | Yes  |

   ** `StreamType` constants:** 

   |  Constant Name  | Description  |
   |---|---|
   |  `VOD`  | Stream type for Video on Demand.  |
   |  `LIVE`  | Stream type for LIVE content.  |
   |  `LINEAR`  | Stream type for LINEAR content.  |

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<VIDEO_NAME>, <VIDEO_ID>, <VIDEO_LENGTH>, <STREAM_TYPE>.VOD);`

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<VIDEO_NAME>,  
                                      <MEDIA_ID,  
                                      <VIDEO_LENGTH>, 
                                      MediaHeartbeat.StreamType.VOD);
   ```

1. **Attach video metadata -** Optionally attach standard and/or custom video metadata objects to the video tracking session through context data variables.

    * **Standard video metadata -** 
    
      >[!NOTE]
      >
      >Attaching the standard video metadata object to the media object is optional.

      Instantiate a standard video metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example:     
    
      ```js    
      var standardVideoMetadata = {}; 
      standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] =  
        "Sample Episode"; 
      standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] =  
        "Sample Show"; 
      mediaObject.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);   
      ```

        * **Video metadata keys API Reference -** [MediaHeartbeat.VideoMetadataKeys](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/javascript/MediaHeartbeat.html#toc8)
        
        * **API Reference -** [](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/javascript/index.html).

      See the comprehensive list of video metadata here: [](../../metrics-and-metadata/audio-video-parameters.md)
    
    * **Custom metadata -** Create a variable object for the custom variables and populate with the data for this video. For example:     
    
      ```js    
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **Track the intention to start playback - **To begin tracking a video session, call `trackSessionStart` on the Media Heartbeat instance: 

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >The second value is the custom video metadata object name that you created in step 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tracks the user intention of playback, not the beginning of the playback. This API is used to load the video data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Track the actual start of playback - **Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call `trackPlay`: 

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Track the completion of playback - **Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call `trackComplete`: 

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Track the end of the session -** Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call `trackSessionEnd`: 

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marks the end of a video tracking session. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Track all possible pause scenarios - **Identify the event from the video player for video pause and call `trackPause`: 

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Pause Scenarios -** Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

    * The user explicitly hits pause in the app.
    * The player puts itself into the Pause state.
    * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
    * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. For example, the user receives a call, or a pop up from another application occurs, but you want the application to keep the session alive to give the user the opportunity to resume the video from the point of interruption.

1. Identify the event from the player for video play and/or video resume from pause and call `trackPlay`: 

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the video playback resumes.

1. Listen for playback seeking events from the media player. On seek start event notification, track seeking using the `SeekStart` event: 

   ```js
   _onSeekStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   };
   ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event: 

   ```
   _onSeekComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   };
   ```

1. Listen for the playback buffering events from the media player, and on buffer start event notification, track buffering using the `BufferStart` event: 

   ```js
   _onBufferStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
   };
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event: 

   ```js
   _onBufferComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
   };
   ```

See the sample player included with your SDK for more context, and for examples of using these core tracking calls. 
