---
seo-title: Track Core Video Playback
title: Track Core Video Playback
uuid: 48763ff0-9833-427d-bb46-8c11d44af7e6
index: y
internal: n
snippet: y
translate: y
---

# Track Core Video Playback


>[!IMPORTANT]
>
>This documentation covers tracking in version 2.x of the SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here:[](../implement/download-sdks.md) 



## Overview {#section_904E0524877241939A0E0557E7395C4A}

Core video playback includes tracking video starts, video completes, pausing, and scrubbing. Utilize the video player API to identify key player events and to populate the required and optional video variables. The following are the key elements of tracking video playback; details for each element follow below: 

**On video load:** 


* Create the media object
* Populate the metadata
* Call ` trackSessionStart(mediaObject, contextData)`


**On video start**: 

* Call ` trackPlay`
**On video complete:** 


* Call ` trackComplete`
* Call ` trackSessionEnd`


**On video pause:** 


* Call ` trackPause`
* Call ` trackPlay` when the video resumes


**On video scrub: ** 


* Call ` trackEvent(SeekStart)`
* Call ` trackEvent(SeekComplete)`


**On video buffer: ** 


* Call ` trackEvent(BufferStart);`
* Call ` trackEvent(BufferComplete);`


>[!TIP]
>
>The playhead position is set as part of the set-up and configuration code. For more information about ` getCurrentPlayheadTime`, see [](../implement/sdk-setup/sdk-setup-overview.md). 


## Implement {#section_BB217BE6585D4EDEB34C198559575004}


1. **Initial tracking setup - **Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a ` MediaObject` instance using the video information for video name, video ID, video length, and stream type. ** ` MediaObject` reference:** 

   |  Variable Name  | Description  | Required  |
   |---|---|---|
   |  ` name`  | Video name  | Yes  |
   |  ` mediaid`  | Video unique identifier  | Yes  |
   |  ` length`  | Video length  | Yes  |
   |  ` streamType`  | Stream type (see ` constants MediaHeartbeat.StreamType.VOD`)  | Yes  |

   ** ` MediaHeartbeat.StreamType.VOD` constants:** 

   |  Constant Name  | Description  |
   |---|---|
   |  ` VOD`  | Stream type for Video on Demand.  |
   |  ` LIVE`  | Stream type for LIVE content.  |
   |  ` LINEAR`  | Stream type for LINEAR content.  |

   The general format for creating the ` MediaObject` is ` MediaHeartbeat.createMediaObject(<VIDEO_NAME>, <VIDEO_ID>, <VIDEO_LENGTH>, <STREAM_TYPE>.VOD);` 
   ```
   // Replace <VIDEO_NAME> with the video name. 
   // Replace <MEDIA_ID> with a unique identifier. 
   // Replace <VIDEO_LENGTH> with the video length.
   ```


    * **Android:** 
      ```
      MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
          <VIDEO_NAME>,  
          <MEDIA_ID>,  
          <VIDEO_LENGTH>,  
          MediaHeartbeat.StreamType.VOD 
      );
      ```


    * **iOS:** 
      ```
      ADBMediaObject *mediaObject =  
        [ADBMediaHeartbeat createMediaObjectWithName:<VIDEO_NAME> 
                           mediaId:<MEDIA_ID>  
                           length:<VIDEO_LENGTH>  
                           streamType:ADBMediaHeartbeatStreamTypeVOD]; 
      
      ```


    * **Javascript:** 
      ```
      var mediaObject =  
        MediaHeartbeat.createMediaObject(<VIDEO_NAME>,  
                                         <MEDIA_ID,  
                                         <VIDEO_LENGTH>, 
                                         MediaHeartbeat.StreamType.VOD);
      ```


    * **Chromecast:** 
      ```
      
      ```

    *
    * **Roku:&amp;nbsp;**Media&nbsp;playback&nbsp;tracking&nbsp;method&nbsp;to&nbsp;track&nbsp;the&nbsp;media&nbsp;load&nbsp;and&nbsp;set&nbsp;the &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;current&nbsp;session&nbsp;to&nbsp;active. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    
      ```
      ‘ Create a media info object 
      mediaInfo = adb_media_init_mediainfo() 
      mediaInfo.id = <MEDIA_ID> 
      mediaInfo.playhead = "0" 
      mediaInfo.length = "600" 
       
      ‘ Create context data if any 
      mediaContextData = {} 
      mediaContextData["cmk1"] = "cmv1" 
      mediaContextData[""cmk2""] = "cmv2" 
       
      ADBMobile().mediaTrackLoad(mediaInfo,mediaContextData)
      ```


1. **Attach video metadata - **Optionally attach standard and/or custom video metadata objects to the video tracking session through context data variables. 
    * **Standard video metadata - ** 
      >[!NOTE] {type="note"}
      >
      >Attaching the standard video metadata object to the media object is optional.


      Instantiate a standard video metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example: 
    
        * **Android:** 
          ```
          java          // Sample code to set standard Video Metadata 
          Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
          standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
          standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
          standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
          mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata); 
          
          ```
        
            * **Video metadata keys API Reference** - [ Standard metadata keys - Android ](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
            * **API Reference -** [](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/android/index.html)

        * **iOS:** 
          ```
          // Sample implementation for using standard video metadata keys 
           
          NSMutableDictionary *standardVideoMetadata =  
            [[NSMutableDictionary alloc] init]; 
           
          [standardVideoMetadata setObject:@"Sample Show"  
            forKey:ADBVideoMetadataKeySHOW]; 
           
          [standardVideoMetadata setObject:@"Sample Season"  
            forKey:ADBVideoMetadataKeySEASON]; 
           
          [standardVideoMetadata setObject:@"Sample Episode"  
            forKey:ADBVideoMetadataKeyEPISODE]; 
           
          [mediaObject setValue:standardVideoMetadata  
            forKey:ADBMediaObjectKeyStandardVideoMetadata];
          ```
        
            * **Video metadata keys - ** [](../metrics-and-metadata/ios-metadata-keys.md)
            * **API Reference - ** [](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/ios/index.html)

        * **JavaScript:** 
          ```
          js          var standardVideoMetadata = {}; 
          standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] =  
            "Sample Episode"; 
          standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] =  
            "Sample Show"; 
          mediaObject.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                               standardVideoMetadata);   
          ```

        
            * **Video metadata keys API Reference - ** [ MediaHeartbeat.VideoMetadataKeys ](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/javascript/MediaHeartbeat.html#toc8)
            * **API Reference -** [](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/javascript/index.html).

        * **Roku:**
      See the comprehensive list of video metadata here: [](../metrics-and-metadata/r_vhl_video-params.md)

    * **Custom metadata -** Create a variable object for the custom variables and populate with the data for this video. For example: 
    
        * **Android:** 
          ```
          java          HashMap<String, String> videoMetadata =  
            new HashMap<String, String>(); 
          videoMetadata.put("isUserLoggedIn", "false"); 
          videoMetadata.put("tvStation", "Sample TV Station"); 
          videoMetadata.put("programmer", "Sample programmer");
          ```


        * **iOS:** 
          ```
          NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
          [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
          [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
          ```

        * **JavaScript:** 
          ```
          js          /* Set custom context data */ 
          var customVideoMetadata = { 
              isUserLoggedIn: "false", 
              tvStation: "Sample TV station", 
              programmer: "Sample programmer" 
          };
          ```




1. **Track the intention to start playback - **To begin tracking a video session, call ` trackSessionStart` on the Media Heartbeat instance. 
   >[!TIP]
   >
   >The second value is the custom video metadata object name that you created in step 2.

    * **Android:** 
      ```
      java      public void onVideoLoad(Observable observable, Object data) {  
          _heartbeat.trackSessionStart(mediaInfo, videoMetadata); 
      }
      ```


    * **iOS:** 
      ```
      -(void)onMainVideoLoaded:(NSNotification *)notification { 
      //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
          [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
      }
      ```


    * **JavaScript:** 
      ```
      js      mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
      ```


    * **Roku:** 
      ```
      trackSessionStart: Function(mediaInfo as Object, contextData = invalid as Object) As Void 
      m._logger.debug("#::trackSessionStart()") 
      reContext = m._ruleEngine.createContext() 
      reContext.setData(m._KEY_MEDIA_OBJECT, mediaInfo) 
      reContext.setData(m._KEY_CUSTOM_METADATA, m._cleanContextData(contextData)) 
      m._processRule(m._Rule.SessionStart, reContext) 
      End Function 
      
      ```


   >[!IMPORTANT]
   >
   >` trackSessionStart` tracks the user intention of playback, not the beginning of the playback. This API is used to load the video data/metadata and to estimate the time-to-start QoS metric (the time duration between ` trackSessionStart` and ` trackPlay`). 

   >[!NOTE] {type="note"}
   >
   >If you are not using custom video metadata, simply send an empty object for the ` data` argument in ` trackSessionStart`, as shown in the commented out line in the iOS example above. 

1. **Track the actual start of playback - **Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call ` trackPlay`: 
    * **Android:** 
      ```
      java      // Video is rendered on the screen) and call trackPlay.  
      public void onVideoPlay(Observable observable, Object data) { 
          _heartbeat.trackPlay(); 
      }
      ```


    * **iOS:** 
      ```
      -(void)onVideoPlay:(NSNotification *)notification { 
          [_mediaHeartbeat trackPlay]; 
      }
      ```


    * **JavaScript:** 
      ```
      js      mediaHeartbeat.trackPlay();
      ```




1. **Track the completion of playback - **Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call ` trackComplete`: 
    * **Android:** 
      ```
      java      public void onVideoComplete(Observable observable, Object data) { 
          _heartbeat.trackComplete(); 
      }
      ```


    * **iOS:** 
      ```
      -(void)onVideoComplete:(NSNotification *)notification { 
          [_mediaHeartbeat trackComplete]; 
      }
      ```


    * **JavaScript:** 
      ```
      js      mediaHeartbeat.trackComplete();
      ```




1. **Track the end of the session - **Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call ` trackSessionEnd`: 
    * **Android:** 
      ```
      java      // Closes the video and/or the video completed and unloaded,  
      // and call trackSessionEnd().  
      public void onMainVideoUnload(Observable observable, Object data) {  
          _heartbeat.trackSessionEnd(); 
      }
      ```


    * **iOS:** 
      ```
      - void)onMainVideoUnloaded:(NSNotification *)notification { 
          [_mediaHeartbeat trackSessionEnd]; 
      }
      ```


    * **JavaScript:** 
      ```
      js      mediaHeartbeat.trackSessionEnd();
      ```




   >[!IMPORTANT]
   >
   >` trackSessionEnd` marks the end of a video tracking session. If the session was successfully watched to completion, where the user watched the content until the end, ensure that ` trackComplete` is called before ` trackSessionEnd`. Any other ` track*` API call is ignored after ` trackSessionEnd`, except for ` trackSessionStart` for a new video tracking session. 

1. **Track all possible pause scenarios - **Identify the event from the video player for video pause and call ` trackPause`. 
    * **Android:** 
      ```
      java      public void onVideoPause(Observable observable, Object data) {  
          _heartbeat.trackPause(); 
      }
      ```


    * **iOS:** 
      ```
      -(void)onVideoPause:(NSNotification *)notification { 
          [_mediaHeartbeat trackPause]; 
      }
      ```


    * **JavaScript:** 
      ```
      js      mediaHeartbeat.trackPause();
      ```




   **Pause Scenarios - **Identify any scenario in which the Video Player will pause and make sure that ` trackPause` is properly called. The following scenarios all require that your app call ` trackPause()`: 


    * The user explicitly hits pause in the app.
    * The player puts itself into the Pause state.
    * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
    * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. For example, the user receives a call, or a pop up from another application occurs, but you want the application to keep the session alive to give the user the opportunity to resume the video from the point of interruption.


1. Identify the event from the player for video play and/or video resume from pause and call ` trackPlay`. 
    * **Android:** 
      ```
      java      // trackPlay() 
      public void onVideoPlay(Observable observable, Object data) {  
          _heartbeat.trackPlay(); 
      }
      ```


    * **iOS:** 
      ```
      -(void)onVideoPlay:(NSNotification *)notification { 
          [_mediaHeartbeat trackPlay]; 
      }
      ```


    * **JavaScript:** 
      ```
      js      mediaHeartbeat.trackPlay();
      ```




   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. Ensure that each ` trackPause()` API call is paired with a following ` trackPlay()` API call when the video playback resumes. 

1. Listen for playback seeking events from the media player. On seek start event notification, track seeking using the ` SeekStart` event. 
    * **Android:** 
      ```
      public void onSeekStart(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onSeekStart:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onSeekStart = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
      };
      ```



1. On seek complete notification from the media player, track the end of seeking using the ` SeekComplete` event. 
    * **Android:** 
      ```
      java      public void onSeekComplete(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
      }
      ```


    * **iOS:** 
      ```
      - (void)onSeekComplete:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      _onSeekComplete = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
      };
      ```


1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the ` BufferStart` event. 
    * **Android:** 
      ```
      public void onBufferStart(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onBufferStart:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onBufferStart = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
      };
      ```



1. On buffer complete notification from media player, track the end of buffering using the ` BufferComplete` event. 
    * **Android:** 
      ```
      public void onBufferComplete(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onBufferComplete:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onBufferComplete = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
      };
      ```





The following sample code uses the JavaScript 2.x SDK for an HTML5 video player: 
```
js/* Call on video start */ 
if (e.type == "play") { 
 
    // Check for start of video 
    if (mediaOffset == 0) { 
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<VIDEO_NAME>,  
                                            <VIDEO_ID>,  
                                            <VIDEO_LENGTH>, 
                                            MediaHeartbeat.StreamType.VOD);*/ 
        var mediaInfo = MediaHeartbeat.createMediaObject( 
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration, 
          MediaHeartbeat.StreamType.VOD); 
 
        /* Set custom context data */ 
        var customVideoMetadata = { 
            isUserLoggedIn: "false", 
            tvStation: "Sample TV station", 
            programmer: "Sample programmer" 
        }; 
 
        /* Set standard video metadata */     
        var standardVideoMetadata = {}; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     
 
        // Start Session 
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    
 
        // Track play 
        this.mediaHeartbeat.trackPlay();      
 
    } else { 
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    } 
}; 
 
/* Call on video complete */ 
if (e.type == "ended") { 
    console.log("video ended"); 
    this.mediaHeartbeat.trackComplete(); 
    this.mediaHeartbeat.trackSessionEnd(); 
    mediaOffset = 0;     
}; 
 
/* Call on pause */ 
if (e.type == "pause") { 
    this.mediaHeartbeat.trackPause(); 
}; 
 
/* Call on scrub start */ 
if (e.type == "seeking") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
}; 
     
/* Call on scrub stop */ 
if (e.type == "seeked") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
}; 
 
/* Call on buffer start */ 
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffering end”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
}; 

```


## Validate {#section_ABCFB92C587B4CAABDACF93452EFA78F}

**Video Start** 

On start of a video player, these key calls are sent in the following order: 


1. Video analytics start*****
1. Heartbeat start*****
1. Heartbeat analytics start


*****These calls contain additional metadata variables for both custom and standard. 

**Content Play** 

During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds. 

**Video Complete** 

At the 100% point, on a video or at a show boundary on a linear stream, a Heartbeat complete call will be sent. 

**Content Pause** 

When the video player pauses, video player pause event calls will be sent every 10 seconds. After pause ends, the play events should resume. 

**Content Scrub/Seek** 

On scrubbing of the video playhead, no special tracking calls are sent. However, when video playback resumes after scrubbing, the playhead value should reflect the new position in the main content. 

**Content Buffer** 

When the video player buffers, video player buffer event calls will be sent every 10 seconds. After buffer ends, the play events should resume. 
