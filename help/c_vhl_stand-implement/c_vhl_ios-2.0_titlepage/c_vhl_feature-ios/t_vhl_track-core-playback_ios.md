---
description: null
seo-description: null
seo-title: Track core playback
title: Track core playback
uuid: f230bd32-98a9-465a-be68-fd92bc98ae7a
index: y
internal: n
snippet: y
translate: y
---

# Track core playback

Add the library to your project by completing the tasks in [ Implement the iOS library ](c_vhl_imp-lib-ios.md#concept_A72BFE683F4A4A3397FD0C71E955DF07) and [](../../../c_vhl_stand-implement/c_vhl_ios-2.0_titlepage/c_vhl_feature-ios/t_vhl_set-up-vid-track-feat_ios.md). 

>1. **Initial tracking setup - **Identify when the user triggers the intention of playback (the user clicks Play and/or autoplay is on) and create an ` ADBMediaObject` instance using the video information.
>   Here is the ` ADBMediaObject` (Media Object) Reference: 

>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | Video name.  | Yes  |
>   |  ` mediaid`  | Video unique identifier.  | Yes  |
>   |  ` length`  | Video length  | Yes  |
>   |  ` streamType`  | Stream type (see constants ` ADBMediaHeartbeatStreamType`)  | Yes  |

>   Here is the ` ADBMediaHeartbeatStreamType` constants reference: 

>   |  Constant name  | Description  |
>   |---|---|
>   |  ` ADBMediaHeartbeatStreamTypeVOD`  | Stream type for Video on Demand.  |
>   |  ` ADBMediaHeartbeatStreamTypeLIVE`  | Stream type for LIVE content.  |
>   |  ` ADBMediaHeartbeatStreamTypeLINEAR`  | Stream type for LINEAR content.  |

>
>   ```
>   // Replace <VIDEO_NAME> with the video name. 
>   // Replace <VIDEO_ID> with a unique video identifier. 
>   // Replace <VIDEO_LENGTH> with the video length. 
>   ADBMediaObject *mediaObject = [ADBMediaHeartbeat createMediaObjectWithName:<VIDEO_NAME> 
>                                                    mediaId:<VIDEO_ID>  
>                                                    length:<VIDEO_LENGTH>  
>                                                    streamType:ADBMediaHeartbeatStreamTypeVOD]; 
>   
>   ```

>
>1. **Track the intention to start playback - **Call ` trackSessionStart` in the ` ADBMediaHeartbeat` instance to begin tracking a video session:
>
>   ```
>   - void)onMainVideoLoaded:(NSNotification *)notification { 
>       [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
>   } 
>   
>   ```

>   >[!NOTE]
>   >
>   >The ` trackSessionStart` call tracks the user intention of playback, not the beginning of the playback. This API is used to load the video data/metadata and to estimate the time to start QoS metric (time duration between ` trackSessionStart` and ` trackPlay`). 
>
>1. **Track the actual start of playback - **Identify the event from the video player for the beginning of the video playback (the first frame of the main content is rendered on the screen) and call ` trackPlay`.
>
>   ```
>   -(void)onVideoPlay:(NSNotification *)notification { 
>       [_mediaHeartbeat trackPlay]; 
>   }
>   ```
>
>1. **Track the completion of playback - **Identify the event from the video player for the completion of the video playback (user watched to the end of the content) and call ` trackComplete`.
>
>   ```
>   -(void)onVideoComplete:(NSNotification *)notification { 
>       [_mediaHeartbeat trackComplete]; 
>   }
>   ```
>
>1. **Track the end of the session - **Identify the event from the video player for the unloading/closing of the video playback (user closes the video and/or the video completed and unloaded) and call ` trackSessionEnd`.
>
>   ```
>   - void)onMainVideoUnloaded:(NSNotification *)notification { 
>       [_mediaHeartbeat trackSessionEnd]; 
>   }
>   ```

>   >[!NOTE]
>   >
>   >` trackSessionEnd` marks the end of a video tracking session. If the session was successfully watched to completion (the user watched to the end of the content), make sure that ` trackComplete` is called before ` trackSessionEnd`. Any other ` track*` API call is ignored after ` trackSessionEnd` (except for ` trackSessionStart` for a new video tracking session). 
>
>1. **Track all possible pause scenarios - **Identify any event from the video player that causes the video to pause and call ` trackPause`.
>    
>       ```
>       -(void)onVideoPause:(NSNotification *)notification { 
>           [_mediaHeartbeat trackPause]; 
>       }
>       ```
>       **Pause Scenarios - **Identify any scenario in which the Video Player will pause and make sure that ` trackPause` is properly called. The following scenarios all require that your app call ` trackPause`: 

>    
>    * The user explicitly hits pause in the app.
>    * The player puts itself into the Pause state.
>    * The user puts the application into the background, but you want the app to keep the session open.
>    * Any type of system interrupt occurs that causes an application to be backgrounded. For example, the user receives a call, or a pop up from another application occurs, but you want the application to keep the session alive to give the user the opportunity to resume the video from the point of interruption.

>    
>1. Identify the event from the video player for video play and/or video resume from pause and call ` trackPlay`.
>
>   ```
>   -(void)onVideoPlay:(NSNotification *)notification { 
>       [_mediaHeartbeat trackPlay]; 
>   } 
>   
>   ```

>   >[!NOTE]
>   >
>   >This might be the same event source that was used for "How to track video playback". Make sure that each ` trackPause` API call is paired with a following ` trackPlay` API call when the video playback resumes 
>
