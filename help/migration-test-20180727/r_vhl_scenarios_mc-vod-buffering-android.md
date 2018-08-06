---
description: null
seo-description: null
seo-title: Playback with buffering in the main content
title: Playback with buffering in the main content
uuid: dc34a477-553c-41b6-9aa4-d4c1fdb19bcd
index: y
internal: n
snippet: y
translate: y
---

# Playback with buffering in the main content


><a id="fig_E4644A6B9940403BA81AC82585C4C1D7"></a> ![](graphics/buffer-regular-content.png) 
>To view this scenario in Android, set up the following code:
>
>```
>java>// Set up mediaObject 
> 
>MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>    Configuration.VIDEO_NAME,  
>    Configuration.VIDEO_ID,  
>    Configuration.VIDEO_LENGTH,  
>    MediaHeartbeat.StreamType.VOD 
> 
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
>// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
>//    frame of the main content is rendered on the screen. 
>_mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 3. Track the MediaHeartbeat.Event.BufferStart event when the video player  
>//    goes into the buffering state and begins to buffer content. 
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
> 
>....... 
>....... 
> 
>// 4. Track the MediaHeartbeat.Event.BufferComplete event when the video player  
>//    goes into the buffering state and begins to buffer content. 
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete, null, null); 
> 
>....... 
>....... 
> 
>// 5. Call trackComplete() when the playback reaches the end, i.e., when the 
>//    video completes and finishes playing. 
>_mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 6. Call trackSessionEnd() when the playback session is over. This method must  
>//    be called even if the user does not watch the video to completion. 
>_mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>
>```

