---
description: null
seo-description: null
seo-title: Inactive video sessions and resuming
title: Inactive video sessions and resuming
uuid: 92885925-ca34-4c66-8735-92b5e25521a6
index: y
internal: n
snippet: y
translate: y
---

# Inactive video sessions and resuming


>[!NOTE] {type="other" othertype="Prerequisite"}
>
>Before you configure the resuming of inactive video sessions, see*Core playback tracking* and *Adding pause and other interruptions* in [ Implement the Android library ](c_vhl_imp-lib-android.md#concept_A72BFE683F4A4A3397FD0C71E955DF07). 

**Long Pauses - **

Media Heartbeat (VHL) automatically tracks how long the video playback is in one of the following inactive states: 


* Paused
* Seeking
* Stalled
* Buffering
If a video tracking session remains in an inactive state for longer than 30 minutes, the session will automatically be closed. If the user resumes after a previously inactive video tracking session ( ` trackPlay()`), Media Heartbeat automatically creates a new video session using the previously used video information and metadata, and sends a resume heartbeat event. For more information, see [ Video Measurement Parameters ](../../../c_vhl_stand-implement/c_vhl_titlepage-android/c_vhl_android_video_params.md#concept_F0673625FDD148C6AF455E8947378609). 

**Manually Resume Previously Closed Session - **

VHL will only automatically resume sessions if the application was not closed. If the application stores user data and has the capability to resume a previously closed video, it is possible to manually trigger a resume event. When starting the video tracking session, set the optional property ` MediaHeartbeat.MediaObjectKey.VideoResumed` to ` true`. 
```
java// Set MediaHeartbeat.MediaObjectKey.VideoResumed to true 
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

