---
description: null
seo-description: null
seo-title: Live content playback
title: Live content playback
uuid: c6cdec4c-7b77-43ee-b4a3-81e522b5e86f
index: y
internal: n
snippet: y
translate: y
---

# Live content playback


><a id="fig_65D741D8180845E3BD58C248DD5083C6"></a> ![](graphics/android-live-noads-noepisodes.png) 
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
>//    i.e., there is an intent to start playback.  
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
>// 3. Call trackSessionEnd() when user ends the playback session.  
>//    Since the user does not watch live video to completion, there  
>//    is no need to call trackComplete().  
>_mediaHeartbeat.trackSessionEnd(); 
>....... 
>....... 
>
>```

