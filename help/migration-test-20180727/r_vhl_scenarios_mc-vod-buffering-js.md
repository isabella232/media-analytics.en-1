---
description: null
seo-description: null
seo-title: Playback with buffering in the main content
title: Playback with buffering in the main content
uuid: 6897fa57-a31f-41ad-9644-43f400431873
index: y
internal: n
snippet: y
translate: y
---

# Playback with buffering in the main content


><a id="fig_E4644A6B9940403BA81AC82585C4C1D7"></a> ![](graphics/buffer-regular-content.png) 
>To view this scenario, enter the following text: >
>```
>js>// Set up mediaObject 
> 
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
>// 3. Track event MediaHeartbeat.Event.BufferStart when the video player  
>//    goes into the buffering state and begins to buffer content. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
> 
>....... 
>....... 
> 
>// 4. Track the MediaHeartbeat.Event.BufferComplete event when the  
>//    video player goes into the buffering state and begins to buffer content. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
> 
>....... 
>....... 
> 
>// 5. Call trackComplete() when the playback reaches the end, i.e.,  
>//    when playback completes and finishes playing. 
>this._mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 6. Call trackSessionEnd() when the playback session is over. This method must  
>//    be called even if the user does not watch the video to completion. 
>this._mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

