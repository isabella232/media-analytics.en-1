---
description: null
seo-description: null
seo-title: Manually resume a previously closed session
title: Manually resume a previously closed session
uuid: 8884fcb4-a425-4541-ba99-296aff98a522
index: y
internal: n
snippet: y
translate: y
---

# Manually resume a previously closed session


>[!NOTE] {type="other" othertype="Prerequisite"}
>
>Before you manually resume a previously closed session, see[ Getting started in JavaScript ](../../../../c_vhl_stand-implement/c_vhl_titlepage-js/r_vhl_getting-started-js.md#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD). 

MediaHeartbeat (VHL) will only automatically resume sessions if the application was not closed. If the application stores user data and has the capability to resume a previously closed video, it is possible to manually trigger a resume event. When starting the video tracking session. Set the optional property ` MediaObjectKey.VideoResumed` to ` Yes`. 


```
js_onVideoLoad = function () { 
    // Replace <VIDEO_NAME> with the video name. 
    // Replace <VIDEO_ID> with a video unique identifier. 
    // Replace <VIDEO_LENGTH> with the video length.  
    var mediaObject =  
      MediaHeartbeat.createMediaObject(<VIDEO_NAME>,  
                                       <VIDEO_ID,  
                                       <VIDEO_LENGTH>,  
                                       MediaHeartbeat.StreamType.VOD); 
      
    // Set to true if this user is resuming a previously closed video session 
    mediaObject.setValue(MediaObjectKey.VideoResumed, true); 
    this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
};
```

