---
description: null
seo-description: null
seo-title: Playback with a pre-roll ad break
title: Playback with a pre-roll ad break
uuid: 696347d6-d223-439b-ab64-da1c55fa4416
index: y
internal: n
snippet: y
translate: y
---

# Playback with a pre-roll ad break


><a id="fig_49C7C3412C3B413EABE67C39260F6C40"></a> ![](graphics/preroll-regular-playback.png) 
>To view this scenario in Android, set up the following code:
>
>```
>java>// Set up  mediaObject 
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
>//    i.e., there's an intent to start playback.  
>_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// Pre-roll 
>MediaObject adBreakInfo =  
>  MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
>                                     ADBREAK_POSITION,  
>                                     ADBREAK_START_TIME); 
>MediaObject adInfo =  
>  MediaHeartbeat.createAdObject(AD_NAME,  
>                                AD_ID,  
>                                AD_POSITION,  
>                                AD_LENGTH); 
> 
>// Context ad data 
>HashMap<String, String> adMetadata = new HashMap<String, String>(); 
>adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
>adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
> 
>// 2. Track the MediaHeartbeat.Event.AdBreakStart event when the pre-roll pod starts  
>//    to play. Note that since this is a pre-roll, call must track the 
>//    "MediaHeartbeat.Event.AdBreakStart" event before you call trackPlay().  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
> 
>....... 
>....... 
> 
>// 3. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's ad starts  
>//    to play. Note that since this is a pre-roll, you must track the  
>//    "MediaHeartbeat.Event.AdStart" event before you call trackPlay(). 
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 4. Call trackPlay() when the playback actually starts, i.e., when the first frame  
>//    of the ad video is rendered on the screen. 
>_mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
>//    i.e., when the ad completes and finishes playing.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
> 
>....... 
>....... 
> 
>// 6. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's second ad  
>//    starts to play. 
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 7. Track the MediaHeartbeat.Event.AdComplete event when the second ad reaches the  
>//    end, i.e., the second ad completes and finishes playing. 
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
> 
>....... 
>....... 
> 
>// 8. Track the MediaHeartbeat.Event.AdBreakComplete event when all of the ads in the  
>//    pod finish playing.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
> 
>....... 
>....... 
> 
>// 9. Call trackComplete() when the playback reaches the end, i.e., when the video 
>//    completes and finishes playing. 
>_mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 10. Call trackSessionEnd() when the playback session is over. This method must be  
>//     called even if the user does not watch the video to completion.  
>_mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

