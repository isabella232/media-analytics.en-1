---
description: null
seo-description: null
seo-title: Track core playback
title: Track core playback
uuid: 5ca03fff-9c00-4012-929a-985d6529cb15
index: y
internal: n
snippet: y
translate: y
---

# Track core playback

Add the library to your project by completing the tasks in [ Implement the Android library ](c_vhl_imp-lib-android.md#concept_A72BFE683F4A4A3397FD0C71E955DF07) and [](t_vhl_set-up-vid-track-feat_android.md).

>1. **Initial tracking setup -**Identify when the user triggers the intention of playback (the user clicks Play and/or autoplay is on) and create a ` MediaObject` instance using the video information.
>   Here is the ` MediaObject` (Media Object) reference: 


>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | Video name  | Yes  |
>   |  ` mediaid`  | Video unique identifier  | Yes  |
>   |  ` length`  | Video length  | Yes  |
>   |  ` streamType`  | Stream type  | Yes  |

>   Here is the ` MediaHeartbeat.StreamType` constants reference: 


>   |  Constant name  | Description  |
>   |---|---|
>   |  ` MediaHeartbeat.StreamType.VOD`  | Stream type for Video on Demand (VOD)  |
>   |  ` MediaHeartbeat.StreamType.LIVE`  | Stream type for Live content.  |
>   |  ` MediaHeartbeat.StreamType.LINEAR`  | Stream type for Linear content.  |

>
>   ```
>   java>   // Replace <VIDEO_NAME> with the video name. 
>   // Replace <VIDEO_ID> with a video unique identifier. 
>   // Replace <VIDEO_LENGTH> with the video length.  
>    
>   MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
>       <VIDEO_NAME>,  
>       <VIDEO_ID>,  
>       <VIDEO_LENGTH>,  
>       MediaHeartbeat.StreamType.VOD 
>   );
>   ```

>
>1. **Custom video metadata -**If you need to attach custom video metadata (Adobe Analytics context data) to the video tracking session, create a ` HashMap` with the key­value pairs:
>
>   ```
>   java>   HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
>   videoMetadata.put("isUserLoggedIn", "false"); 
>   videoMetadata.put("tvStation", "Sample TV Station"); 
>   videoMetadata.put("programmer", "Sample programmer"); 
>   
>   ```
>
>1. **Track the intention to start playback -**Call ` trackSessionStart()` on the ` MediaHeartbeat` instance to begin tracking a video session:
>    
>       ```
>       java>       public void onVideoLoad(Observable observable, Object data) {  
>           _heartbeat.trackSessionStart(mediaInfo, videoMetadata); 
>       }
>       ```

>       >[!NOTE]
>       >
>       >
>       >* ` trackSessionStart()` tracks the user intention of playback, not the beginning of the playback. This API is used to load the video data/metadata and to estimate the time to start QoS metric (time duration between ` trackSessionStart()` and ` trackPlay()`).
>       >* If you are not using custom video metadata, simply send an empty object for the ` data` argument in ` trackSessionStart()`.

>    
>1. **Track the actual start of playback -**Identify the event from the video player for the beginning of the video playback (the first frame of the video is rendered on the screen) and call ` trackPlay()`.
>
>   ```
>   java>   // Video is rendered on the screen) and call trackPlay.  
>   public void onVideoPlay(Observable observable, Object data) { 
>       _heartbeat.trackPlay(); 
>   }
>   ```
>
>1. **Track the completion of playback -**Identify the event from the video player for the completion of the video playback (watched the end of the content) and call ` trackComplete()`.
>
>   ```
>   java>   public void onVideoComplete(Observable observable, Object data) { 
>       _heartbeat.trackComplete(); 
>   }
>   ```
>
>1. **Track the end of the session -**Identify the event from the video player for the unloading/closing of the video playback (user closes the video and/or the video completed and unloaded) and call ` trackSessionEnd`.
>
>   ```
>   java>   // Closes the video and/or the video completed and unloaded,  
>   // and call trackSessionEnd().  
>   public void onMainVideoUnload(Observable observable, Object data) {  
>       _heartbeat.trackSessionEnd(); 
>   }
>   ```

>   >[!NOTE]
>   >
>   >` trackSessionEnd()` marks the end of a video tracking session. If the session was successfully watched to completion (user watched to the end of the content), make sure that ` trackComplete()` is called before ` trackSessionEnd()`. Any other * ` track*`* API call is ignored after ` trackSessionEnd()` (except for ` trackSessionStart()` for a new video tracking session). 
>
>1. **Track all possible pause scenarios -**Identify any event from the video player that causes the video to pause and call ` trackPause`.
>    
>       ```
>       java>       public void onVideoPause(Observable observable, Object data) {  
>           _heartbeat.trackPause(); 
>       }
>       ```
>       **Pause Scenarios -**Identify any scenario in which the Video Player will pause and make sure that ` trackPause` is properly called. The following scenarios all require that your app call ` trackPause()`: 
>    
>    * The user explicitly hits pause in the app.
>    * The player puts itself into the Pause state.
>    * The user puts the application into the background, but you want the app to keep the session open.
>    * Any type of system interrupt occurs that causes an application to be backgrounded. For example, the user receives a call, or a pop up from another application occurs, but you want the application to keep the session alive to give the user the opportunity to resume the video from the point of interruption.

>    
>1. Identify the event from the video player for video play and/or video resume from pause and call ` trackPlay()`.
>
>   ```
>   java>   // trackPlay() 
>   public void onVideoPlay(Observable observable, Object data) {  
>       _heartbeat.trackPlay(); 
>   } 
>   
>   ```

>   >[!TIP]
>   >
>   >This may be the same event source that was used in Step 4. Ensure that each ` trackPause()` API call is paired with a following ` trackPlay()` API call when the video playback resumes. 
>
