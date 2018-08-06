---
description: null
seo-description: null
seo-title: Playback with a pre-roll ad break
title: Playback with a pre-roll ad break
uuid: c6406ace-d46e-4237-817f-ac762e74e1d7
index: y
internal: n
snippet: y
translate: y
---

# Playback with a pre-roll ad break


><a id="fig_49C7C3412C3B413EABE67C39260F6C40"></a> ![](graphics/preroll-regular-playback.png) 
>To view this scenario in JavaScript, enter the following text: >
>```
>js>// Set up mediaObject 
>var mediaInfo =  
>  MediaHeartbeat.createMediaObject(Configuration.VIDEO_NAME,  
>                                   Configuration.VIDEO_ID,  
>                                   Configuration.VIDEO_LENGTH,MediaHeartbeat.StreamType.VOD); 
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
>// Preroll 
>var adBreakInfo =  
>  MediaHeartbeat.createAdBreakObject(ADBREAK_NAME, ADBREAK_POSITION, ADBREAK_START_TIME); 
>var adInfo =  
>  MediaHeartbeat.createAdObject(AD_NAME, AD_ID, AD_POSITION, AD_LENGTH); 
> 
>// Custom ad metadata 
>var adMetadata = { 
>    CUSTOM_AD_KEY_1 : CUSTOM_AD_VAL_1,  
>    CUSTOM_AD_KEY_2 : CUSTOM_AD_VAL_2 
>}; 
> 
>// 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod starts to play.  
>//    Note that since this is a preroll, track the MediaHeartbeat.Event.AdBreakStart  
>//    event before you call trackPlay(). 
>this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
> 
>....... 
>....... 
> 
>// 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's ad starts to play.  
>//    Note that since this is a preroll, track the MediaHeartbeat.Event.AdStart event before  
>//    you call trackPlay(). 
>this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 4. Call trackPlay() when the playback actually starts, i.e., the first frame of the  
>      main content is rendered on the screen.  
>this._mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 5. Track event MediaHeartbeat.Event.AdComplete when the ad reaches the end,  
>//    i.e., when it completes and finishes playing. 
>this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
> 
>....... 
>....... 
> 
>// 6. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's second  
>//    ad starts to play. 
>this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 7. Track the MediaHeartbeat.Event.AdComplete event when the second ad reaches  
>//    the end, i.e., when it completes and finishes playing. 
>this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
> 
>....... 
>....... 
> 
>// 8. Track the MediaHeartbeat.Event.AdBreakComplete event when all the ads  
>//    in the pod finish playing. 
>this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
> 
>....... 
>....... 
> 
>// 9. Call trackComplete() when the playback reaches the end, i.e., when it 
>//    completes and finishes playing.  
>this._mediaHeartbeat.trackComplete(); 
> 
>// 10. Call trackSessionEnd() when the playback session is over. This method must  
>//     be called even if the user does not watch the video to completion. 
>this._mediaHeartbeat.trackSessionEnd(); 
> 
>....... 
>.......
>```

