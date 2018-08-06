---
description: Scenario  Content is 40 seconds long, played until the end, without any interruption.
seo-description: Scenario  Content is 40 seconds long, played until the end, without any interruption.
seo-title: Playback with no interruptions
title: Playback with no interruptions
uuid: 04b904eb-aff6-4772-8d7a-fa2ec81b9c52
index: y
internal: n
snippet: y
translate: y
---

# Playback with no interruptions

<a id="fig_DC8297DD576944B3A0F2E00CE8A89F02"></a> ![](graphics/main-content-regular-playback.png) 
To view this scenario in JavaScript, enter the following text: 
```
js// Set up mediaObject 
 
var mediaInfo = MediaHeartbeat.createMediaObject(Configuration.VIDEO_NAME, Configuration.VIDEO_ID,  
Configuration.VIDEO_LENGTH,MediaHeartbeat.StreamType.VOD); 
var videoMetadata = { 
    CUSTOM_KEY_1 : CUSTOM_VAL_1,  
    CUSTOM_KEY_2 : CUSTOM_VAL_2,  
    CUSTOM_KEY_3 : CUSTOM_VAL_3 
 
}; 
 
// 1. Call trackSessionStart() when the user clicks play, or when autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
 
...... 
...... 
 
// 2. Call trackPlay() when the main content starts, i.e.,  
//    the first frame of the video content is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 
 
....... 
....... 
 
// 3. Call trackComplete() when the playback reaches the end,  
      i.e., the video completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 
 
........ 
........ 
 
// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not  
//    watch the video to completion. 
this._mediaHeartbeat.trackSessionEnd(); 
 
........ 
........
```

