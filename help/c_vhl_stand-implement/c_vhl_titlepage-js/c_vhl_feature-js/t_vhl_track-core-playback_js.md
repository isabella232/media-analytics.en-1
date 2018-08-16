---
description: null
seo-description: null
seo-title: Track core playback
title: Track core playback
uuid: 14a229ba-85e0-4bb0-8cdb-e0867371afc0
index: y
internal: n
snippet: y
translate: y
---

# Track core playback

Add the library to your project by completing the tasks in[ Implement the JavaScript library ](c_vhl_imp-lib-js.md#concept_A72BFE683F4A4A3397FD0C71E955DF07) and [ Configure and setup ](../../../c_vhl_stand-implement/c_vhl_titlepage-js/c_vhl_feature-js/t_vhl_set-up-vid-track-feat_js.md#task_7DDA96A6DDB841569025678102973E60). 
>1. Identify when the user triggers the intention of playback (user clicks play and/or autoplay is on) and create a ` MediaObject` instance using the video information.
>   Here is the ` MediaObject` (Media Object) reference: 



>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | Video name.  | Yes  |
>   |  ` mediaId`  | Video unique identifier.  | Yes  |
>   |  ` length`  | Video length  | Yes  |
>   |  ` streamType`  | Stream type (see constants ` MediaHeartbeatStreamType`)  | Yes  |

>   Here is the ` MediaHeartbeat.StreamType` constants reference: 



>   |  Constant name  | Description  |
>   |---|---|
>   |  ` VOD`  | Stream type for Video on Demand.  |
>   |  ` LIVE`  | Stream type for LIVE content.  |
>   |  ` LINEAR`  | Stream type for LINEAR content.  |

>
>   ```
>   js>   //Replace <VIDEO_NAME> with the video name. 
>   //Replace <VIDEO_ID> with a video unique identifier. 
>   //Replace <VIDEO_LENGTH> with the video length.  
>   var mediaObject =  
>     MediaHeartbeat.createMediaObject(<VIDEO_NAME>,  
>                                      <VIDEO_ID,  
>                                      <VIDEO_LENGTH>, 
>                                      MediaHeartbeat.StreamType.VOD);
>   ```

>
>1. To attach custom video metadata (Adobe Analytics context data) to the video tracking session, create an object with key­value pairs:
>
>   ```
>   js>   var videoCustomMetadata = { 
>      subchannel: "Sample sub­channel",  
>      campaign: "Sample campaign",  
>      videometadata3: "Sample video metadata 3" 
>   };
>   ```
>
>1. Call ` trackSessionStart()` in the ` MediaHeartbeat` instance to begin tracking a video session:
>
>   ```
>   js>   _onVideoLoad = function () { 
>       this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
>   }; 
>   
>   ```

>   >[!IMPORTANT]
>   >
>   >` trackSessionStart()` tracks the user intention of playback, not the beginning of the playback. This API is used to load the video data/metadata and to estimate the time to start QoS metric (time duration between ` trackSessionStart()` and ` trackPlay()`). 

>   >[!NOTE]
>   >
>   >If you are not using custom video metadata, simply send an empty object for the ` data` argument in ` trackSessionStart()`. 
>
>1. Identify the event from the video player for the beginning of the video playback (the 1st frame of the main content is rendered on the screen) and call ` trackPlay()`.
>
>   ```
>   js>   _onVideoPlay = function() { 
>       this._mediaHeartbeat.trackPlay(); 
>   };
>   ```
>
>1. Identify the event from the video player for the completion of the video playback (user watched the end of the content) and call ` trackComplete()`.
>
>   ```
>   js>   _onVideoComplete = function() { 
>       this._mediaHeartbeat.trackComplete(); 
>   };
>   ```
>
>1. Identify the event from the video player for the unloading/closing of the video playback (user closes the video and/or the video completed and unloaded) and call ` trackSessionEnd()`.
>
>   ```
>   js>   _onVideoUnload = function() { 
>       this._mediaHeartbeat.trackSessionEnd(); 
>   };
>   ```

>   >[!IMPORTANT]
>   >
>   >` trackSessionEnd()` marks the end of a video tracking session. If the session was successfully watched to completion (user watched the end of the content), make sure that ` trackComplete()` is called before ` trackSessionEnd()`. Any other ` track*` API call is ignored after ` trackSessionEnd()` (except for ` trackSessionStart()` for a new video tracking session). 
>
>1. Identify the event from the video player for video play and/or video resume from pause and call ` trackPause()`.
>
>   ```
>   js>   _onPause = function() { 
>       this._mediaHeartbeat.trackPause(); 
>   }; 
>   
>   ```

>   >[!TIP]
>   >
>   >Identify any scenario in which the Video Player will pause and make sure that ` trackPause()` is properly called. Sample scenarios include when an application goes to background, the video pause, and so on. 
>
>1. Identify the event from the video player for video play and/or video resume from pause and call ` trackPlay()`.
>
>   ```
>   js>   _onVideoPlay = function() { 
>       this._mediaHeartbeat.trackPlay(); 
>   };
>   ```

>   >[!IMPORTANT]
>   >
>   >This might be the same event source that was used for "How to track video playback". Make sure that each ` trackPause()` API call is paired with a following ` trackPlay()` API call when the video playback resumes. 
>
