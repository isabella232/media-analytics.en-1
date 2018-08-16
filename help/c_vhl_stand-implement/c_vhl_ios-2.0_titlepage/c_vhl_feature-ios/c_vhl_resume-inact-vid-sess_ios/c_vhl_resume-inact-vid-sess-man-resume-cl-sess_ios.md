---
description: null
seo-description: null
seo-title: Manually resume a previously closed session
title: Manually resume a previously closed session
uuid: 618870fb-3907-4af2-bc81-c3505e9a934a
index: y
internal: n
snippet: y
translate: y
---

# Manually resume a previously closed session

` MediaHeartbeat` (VHL) will only automatically resume sessions if the application was not closed. If the application stores user data and has the capability to resume a previously closed video, it is possible to manually trigger a resume event. When starting the video tracking session, set the optional property ` ADBMediaObjectKeyVideoResumed` to ` Yes`. 
```
- (void)onMainVideoLoaded:(NSNotification *)notification { 
    //Replace <VIDEO_NAME> with the video name. 
    //Replace <VIDEO_ID> with a video unique identifier. 
    //Replace <VIDEO_LENGTH> with the video length.     
    ADBMediaObject *mediaObject =  
      [ADBMediaHeartbeat createMediaObjectWithName:<VIDEO_NAME> 
                         mediaId:<VIDEO_ID> 
                         length:<VIDEO_LENGTH> 
                         streamType:ADBMediaHeartbeatStreamTypeVOD]; 
 
    //Set to YES if this user is resuming a previously closed video session 
    [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeyVideoResumed]; 
 
    [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
} 

```

