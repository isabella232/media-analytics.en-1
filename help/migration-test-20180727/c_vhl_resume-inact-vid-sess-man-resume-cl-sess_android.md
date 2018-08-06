---
description: null
seo-description: null
seo-title: Manually resume a previously closed session
title: Manually resume a previously closed session
uuid: efb78e51-d44e-4939-94aa-97e7ad563453
index: y
internal: n
snippet: y
translate: y
---

# Manually resume a previously closed session

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

