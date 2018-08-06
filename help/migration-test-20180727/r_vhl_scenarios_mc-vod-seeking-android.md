---
description: null
seo-description: null
seo-title: Playback with seeking in the main content
title: Playback with seeking in the main content
uuid: 84bced99-1000-4e8d-be38-e5b41a00669d
index: y
internal: n
snippet: y
translate: y
---

# Playback with seeking in the main content


><a id="fig_F8759D2BD8374E99AC2A90E57961FB0C"></a> ![](graphics/seek-main-to-main.png) 
><a id="fig_A88CC6C6AACF4DBBACA2AE524276D02B"></a>To view this scenario in Android, set up the following code:
>
>```
>java>// Set up mediaObject 
>MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>    Configuration.VIDEO_NAME,  
>    Configuration.VIDEO_ID,  
>    Configuration.VIDEO_LENGTH,  
>    MediaHeartbeat.StreamType.VOD 
>); 
> 
>HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
>videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
>videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
> 
>// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
>//    i.e., there is an intent to start playback.  
>_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// 2. Call trackPlay() when the playback actually starts, i.e., whn the first frame  
>//    of the main content is rendered on the screen.  
>_mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 3. Track the MediaHeartbeat.Event.SeekStart event when the user begins to seek.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
> 
>....... 
>....... 
> 
>// 4. Track the MediaHeartbeat.Event.SeekComplete event when the user completes seeking 
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
> 
>....... 
>....... 
> 
>// 5. Call trackComplete() when the playback reaches the end, i.e., when the video 
>//    completes and finishes playing. 
>_mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 6. Call trackSessionEnd() when the playback session is over. This method must be  
>//    called even if the user does not watch the video to completion.  
>_mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

