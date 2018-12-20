---
seo-title: Track core playback on iOS
title: Track core playback on iOS
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
index: y
internal: n
snippet: y
---

# Track core playback on iOS{#track-core-playback-on-ios}

>[!IMPORTANT]
>This documentation covers tracking in version 2.x of the SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs](../../../sdk-implement/download-sdks.md)

1. **Initial tracking setup -** Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **[createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:) API** 

   |  Variable Name  | Description  | Required  |
   |---|---|---|
   |  `name`  | Video name  | Yes  |
   |  `mediaid`  | Video unique identifier  | Yes  |
   |  `length`  | Video length  | Yes  |
   |  `streamType`  | Stream type (see `constants MediaHeartbeat.StreamType.VOD`)  | Yes  |
   |  `mediaType`  | Media type ( Audio | Video )  | Yes  |

   **`StreamType` constants:** 

   |  Constant Name  | Description  |
   |---|---|
   |  `ADBMediaHeartbeatStreamTypeVOD`  | Stream type for Video on Demand  |
   |  `ADBMediaHeartbeatStreamTypeLIVE`  | Stream type for Live content  |
   |  `ADBMediaHeartbeatStreamTypeLINEAR`  | Stream type for Linear content  |
   |  `ADBMediaHeartbeatStreamTypeAOD`  | Stream type for Audio On Demand  |
   |  `ADBMediaHeartbeatStreamTypeAUDIOBOOK`  | Stream type for Audio Book  |
   |  `ADBMediaHeartbeatStreamTypePODCAST`  | Stream type for Podcast  |

   **`MediaType` constants:** 

   |  Constant Name  | Description  |
   |---|---|
   |  `ADBMediaTypeAudio`  | Media type for Audio streams.  |
   |  `ADBMediaTypeVideo`  | Media type for Video streams.  |

   The general format for creating the `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                                          mediaId:<MEDIA_ID> 
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE> 
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Attach video metadata -** Optionally attach standard and/or custom video metadata objects to the video tracking session through context data variables.

    * **Standard video metadata -** 
    
      >[!NOTE]
      >
      >Attaching the standard video metadata object to the media object is optional.

        * [Implement standard metadata on iOS](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
        * **Video metadata keys -** [iOS metadata keys](../../../sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
        
        * See the comprehensive list of video metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)

    * **Custom metadata -** Create a variable object for the custom variables and populate with the data for this video. For example:

      ```    
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```

1. **Track the intention to start playback -** To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance. 

   >[!TIP]
   >
   >The second value is the custom video metadata object name that you created in step 2.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` tracks the user intention of playback, not the beginning of the playback. This API is used to load the video data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Track the actual start of playback -** Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call `trackPlay`: 

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Track the completion of playback -** Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call `trackComplete`: 

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **Track the end of the session -** Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call `trackSessionEnd`: 

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marks the end of a video tracking session. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Track all possible pause scenarios -** Identify the event from the video player for video pause and call `trackPause`: 

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **Pause Scenarios -** Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

    * The user explicitly hits pause in the app.
    * The player puts itself into the Pause state.
    * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
    * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. For example, the user receives a call, or a pop up from another application occurs, but you want the application to keep the session alive to give the user the opportunity to resume the video from the point of interruption.

1. Identify the event from the player for video play and/or video resume from pause and call `trackPlay`: 

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the video playback resumes.

See the following for additional information on tracking core playback:

* Tracking scenarios: [VOD playback with no ads](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Sample player included with the iOS SDK for a complete tracking example.

