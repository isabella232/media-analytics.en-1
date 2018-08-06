---
description: null
seo-description: null
seo-title: Playback with seeking in the main content
title: Playback with seeking in the main content
uuid: 43746321-4fe4-455e-bf70-2aa733454776
index: y
internal: n
snippet: y
translate: y
---

# Playback with seeking in the main content


><a id="fig_F8759D2BD8374E99AC2A90E57961FB0C"></a> ![](graphics/seek-main-to-main.png) 
><a id="fig_A88CC6C6AACF4DBBACA2AE524276D02B"></a>To view this scenario, enter the following text: >
>```
>js>// Set up mediaObject 
>var mediaInfo = MediaHeartbeat.createMediaObject( 
>    Configuration.VIDEO_NAME,  
>    Configuration.VIDEO_ID,  
>    Configuration.VIDEO_LENGTH,  
>    MediaHeartbeat.StreamType.VOD 
> 
>); 
> 
>var videoMetadata = { 
>    CUSTOM_KEY_1 : CUSTOM_VAL_1,  
>    CUSTOM_KEY_2 : CUSTOM_VAL_2,  
>    CUSTOM_KEY_3 : CUSTOM_VAL_3 
> 
>}; 
> 
>// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
>//    i.e., there's an intent to start playback. 
>this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// 2. Call trackPlay() when the playback actually starts, i.e., when the  
>//    first frame of the ad video is rendered on the screen. 
>this._mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 3. Track the MediaHeartbeat.Event.SeekStart event when the user  
>//    begins to seek. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
> 
>....... 
>....... 
> 
>// 4. Track the MediaHeartbeat.Event.SeekComplete event when the user  
>//    completes seeking. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
> 
>....... 
>....... 
> 
>// 5. Call trackComplete() when the playback reaches the end, i.e., when 
>//    playback completes and finishes playing. 
>this._mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 6. Call trackSessionEnd() when the playback session is over. This method must be called  
>//    even if the user does not watch the video to completion. 
>this._mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

