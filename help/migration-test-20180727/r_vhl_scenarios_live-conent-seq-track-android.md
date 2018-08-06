---
description: null
seo-description: null
seo-title: Live main content with sequential tracking
title: Live main content with sequential tracking
uuid: 5378461e-ef81-4ed0-9434-d1764994305b
index: y
internal: n
snippet: y
translate: y
---

# Live main content with sequential tracking


><a id="fig_65D741D8180845E3BD58C248DD5083C6"></a> ![](graphics/android-live-noads-multiplesessions.png) 
>Here is the expected API call order: >
>```
>java>// Set up mediaObject 
>MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>    Configuration.VIDEO_NAME,  
>    Configuration.VIDEO_ID,  
>    Configuration.VIDEO_LENGTH,  
>    MediaHeartbeat.StreamType.LIVE 
>); 
> 
>HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
>videoMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
>videoMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 
> 
>// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
>//    i.e., when there is an intent to start playback.  
>_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
>//    frame of main content is rendered on the screen.  
>_mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 3. Call trackComplete() when the playback reaches the end of session,  
>//    i.e., when the video completes and finishes playing 1st episode/session.  
>_mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 4. Call trackSessionEnd() to end session 1 
>_mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
> 
>// Start tracking session 2 /episode 2 of the same live stream.  
>// There is no need to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 
>// Set up mediaObject 
>MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>    Configuration.VIDEO_NAME,  
>    Configuration.VIDEO_ID,  
>    Configuration.VIDEO_LENGTH,  
>    MediaHeartbeat.StreamType.LIVE 
>); 
> 
>HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
>videoMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
>videoMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 
> 
>// 5. Call trackSessionStart() when the playhead reaches a point that denotes the 
>//    start of session 2 
>_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// 6. Call trackPlay() to start tracking session 2 playback  
>_mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 7. Call trackComplete() when the playback reaches the end of session 2,  
>//    i.e., the video completes and finishes playing.  
>_mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 8. Call trackSessionEnd() to end session 2 
>_mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
> 
>// Continue similarly tracking further sessions in the live stream if required 
>
>```

