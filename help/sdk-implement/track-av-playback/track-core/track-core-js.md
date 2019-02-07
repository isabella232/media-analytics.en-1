---
seo-title: Track core playback on JavaScript
title: Track core playback on JavaScript
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab

---

# Track core playback on JavaScript{#track-core-playback-on-javascript}

>[!IMPORTANT]
>This documentation covers tracking in version 2.x of the SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs](../../../sdk-implement/download-sdks.md)

1. **Initial tracking setup -** Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **[createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)**

    |  Variable Name  | Description  | Required  |
    | --- | --- | :---: |
    |  `name`  | Media name  | Yes  |
    |  `mediaid`  | Media unique identifier  | Yes  |
    |  `length`  | Media length  | Yes  |
    |  `streamType`  | Stream type (see _StreamType constants_ below)  | Yes  |
    |  `mediaType`  | Media type (see _MediaType constants_ below)  | Yes  |

   **`StreamType` constants:** 

    |  Constant Name  | Description&nbsp;&nbsp;  |
    |---|---|
    |  `VOD`  | Stream type for Video on Demand.  |
    |  `LIVE`  | Stream type for LIVE content.  |
    |  `LINEAR`  | Stream type for LINEAR content.  |

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>.VOD);`

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                      <MEDIA_ID,  
                                      <MEDIA_LENGTH>, 
                                      MediaHeartbeat.StreamType.VOD);
   ```

1. **Attach metadata -** Optionally attach standard and/or custom metadata objects to the tracking session through context data variables.

    * **Standard metadata -** [Implement standard metadata on JavaScript](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)     
    
      >[!NOTE]
      >
      >Attaching the standard metadata object to the media object is optional.

        * Media metadata keys API Reference - [Standard metadata keys - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript) 

          See the comprehensive set of available metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)

    * **Custom metadata -** Create a variable object for the custom variables and populate with the data for this media. For example:     
    
      ```js    
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **Track the intention to start playback -** To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance: 

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >The second value is the custom media metadata object name that you created in step 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tracks the user intention of playback, not the beginning of the playback. This API is used to load the data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Track the actual start of playback -** Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`: 

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Track the completion of playback -** Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`: 

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Track the end of the session -** Identify the event from the media player for the unloading/closing of the playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`: 

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marks the end of a tracking session. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Track all possible pause scenarios -** Identify the event from the media player for pause and call `trackPause`: 

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Pause Scenarios -** Identify any scenario in which the media player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

    * The user explicitly hits pause in the app.
    * The player puts itself into the Pause state.
    * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
    * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. For example, the user receives a call, or a pop up from another application occurs, but you want the application to keep the session alive to give the user the opportunity to resume the media from the point of interruption.

1. Identify the event from the player for play and/or resume from pause and call `trackPlay`: 

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

* Tracking scenarios: [VOD playback with no ads](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Sample player included with the JavaScript SDK for a complete tracking example.

