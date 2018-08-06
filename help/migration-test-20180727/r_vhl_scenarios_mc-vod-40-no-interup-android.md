---
description: Scenario  Content is 40 seconds long, played until the end, without any interruption.
seo-description: Scenario  Content is 40 seconds long, played until the end, without any interruption.
seo-title: Playback with no interruptions
title: Playback with no interruptions
uuid: af017d02-42c1-47c2-96cf-37c608f43a55
index: y
internal: n
snippet: y
translate: y
---

# Playback with no interruptions

<a id="fig_DC8297DD576944B3A0F2E00CE8A89F02"></a> ![](graphics/main-content-regular-playback.png) 
To view this scenario in Android, set up the following code:

```
java// Set up  mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
    Configuration.VIDEO_NAME,  
    Configuration.VIDEO_ID,  
    Configuration.VIDEO_LENGTH,  
    MediaHeartbeat.StreamType.VOD 
); 
 
HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
videoMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
videoMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 
 
// 1. Call trackSessionStart() when the user clicks Play or if autoplay  
//    is used, i.e., there's an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
 
...... 
...... 
 
// 2. Call trackPlay() when the playback actually starts,  
//    i.e., the first frame of video is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 
 
....... 
....... 
 
// 3. Call trackComplete() when the playback reaches the end,  
//    i.e., when the video completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 
 
........ 
........ 
 
// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not watch  
//    the video to completion.  
_mediaHeartbeat.trackSessionEnd(); 
 
........ 
........ 

```

