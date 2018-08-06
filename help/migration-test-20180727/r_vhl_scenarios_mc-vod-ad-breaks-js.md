---
description: In this scenario, VOD content is played back with a 30-second pre-roll ad, 20 seconds of conent, a 20-second mid-roll ad, 40 seconds of content, and a 20-second post-roll ad.
seo-description: In this scenario, VOD content is played back with a 30-second pre-roll ad, 20 seconds of conent, a 20-second mid-roll ad, 40 seconds of content, and a 20-second post-roll ad.
seo-title: Playback with ad breaks
title: Playback with ad breaks
uuid: 038a6982-f13a-4df5-98ad-fe5f33df9711
index: y
internal: n
snippet: y
translate: y
---

# Playback with ad breaks


>![](graphics/ad-content-regular-playback.png) 
>To view this scenario in JavaScript, enter the following text: >
>```
>js>// Set up mediaObject 
>MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
>    Configuration.VIDEO_NAME,  
>    Configuration.VIDEO_ID,  
>    Configuration.VIDEO_LENGTH,  
>    MediaHeartbeat.StreamType.VOD 
>); 
> 
>var videoMetadata = { 
>    CUSTOM_KEY_1 : CUSTOM_VAL_1,  
>    CUSTOM_KEY_2 : CUSTOM_VAL_2,  
>    CUSTOM_KEY_3 : CUSTOM_VAL_ 
>}; 
> 
>// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
>//    i.e., when there's an intent to start playback.  
>this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// Preroll 
>var adBreakInfo =  
>  MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
>                                     ADBREAK_POSITION,  
>                                     ADBREAK_START_TIME); 
>var adInfo =  
>  MediaHeartbeat.createAdObject(AD_NAME,  
>                                AD_ID,  
>                                AD_POSITION,  
>                                AD_LENGTH); 
> 
>// Custom ad metadata 
>var adMetadata = { 
>    CUSTOM_KEY_1 : CUSTOM_VAL_1,  
>    CUSTOM_KEY_2 : CUSTOM_VAL_2 
> 
>}; 
> 
>// 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod  
>//    starts to play. Note that since this is a preroll, you must track the  
>//    MediaHeartbeat.Event.AdBreakStart event before you call trackPlay().  
>this._trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
> 
>....... 
>....... 
> 
>// 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's ad  
>//    starts to play. Note that since this is a preroll, you must track the 
>//    MediaHeartbeat.Event.AdStart event before you call trackPlay().  
>this._heartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 4. Call trackPlay() when the main content actually starts, i.e., when the  
>//    first frame of the video content is rendered on the screen.  
>this._mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
>//    i.e., when the ad completes and finishes playing. 
>this._heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
> 
>....... 
>....... 
> 
>// 6. Track the MediaHeartbeat.Event.AdBreakComplete event when all of the ads in  
>//    the pod finish playing. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
> 
>....... 
>....... 
> 
>// Midroll 
>var adBreakInfo =  
>  MediaHeartbeat.createAdBreakObject(MIDROLL_BREAK_NAME,  
>                                     MIDROLL_BREAK_POSITION,  
>                                     MIDROLL_BREAK_START_TIME); 
>var adInfo =  
>  MediaHeartbeat.createAdObject(MIDROLL_AD_NAME,  
>                                MIDROLL_AD_ID, 
>                                MIDROLL_AD_POSITION,  
>                                MIDROLL_AD_LENGTH); 
> 
>// Custom ad metadata 
>var adMetadata = { 
>    CUSTOM_KEY_1 : CUSTOM_VAL_1,  
>    CUSTOM_KEY_2 : CUSTOM_VAL_2 
> 
>}; 
> 
>// 7. Track the MediaHeartbeat.Event.AdBreakStart event when the  
>//    midroll pod starts to play. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
> 
>....... 
>....... 
> 
>// 8. Track the MediaHeartbeat.Event.AdStart event when the midroll  
>//    pod's ad starts to play. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
>                                adInfo,  
>                                adMetadata); 
> 
>....... 
>....... 
> 
>// 9. Track the MediaHeartbeat.Event.AdComplete event when the ad  
>//    reaches the end, i.e., when the ad completes and finishes playing.  
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
> 
>....... 
>....... 
> 
>// 10. Track the MediaHeartbeat.Event.AdBreakComplete event when all of  
>//     the ads in the midroll pod finish playing. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
> 
>....... 
>....... 
> 
>// Set up mediaObject 
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
>// 1. Call trackSessionStart() when Play is clicked or if autoplay  
>//    is used, i.e., when there's an intent to start playback. 
>this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
> 
>...... 
>...... 
> 
>// Preroll 
>var adBreakInfo =  
>  MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
>                                     ADBREAK_POSITION,  
>                                     ADBREAK_START_TIME); 
>var adInfo =  
>  MediaHeartbeat.createAdObject(AD_NAME,  
>                                AD_ID,  
>                                AD_POSITION,  
>                                AD_LENGTH); 
> 
>// Custom ad metadata 
>var adMetadata = { 
>   CUSTOM_KEY_1 : CUSTOM_VAL_1,  
>   CUSTOM_KEY_2 : CUSTOM_VAL_2 
> 
>}; 
> 
>// 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod  
>//    starts to play. Note that since this is a preroll, you must track the   
>//    MediaHeartbeat.Event.AdBreakStart event before you call trackPlay(). 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
> 
>....... 
>....... 
> 
>// 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's  
>//    ad starts to play. Note that since this is a preroll, you must track   
>//    the MediaHeartbeat.Event.AdStart event before you call trackPlay(). 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 4. Call trackPlay() when the playback actually starts, i.e., when the first  
>//    frame of the main content is rendered on the screen.  
>_mediaHeartbeat.trackPlay(); 
> 
>....... 
>....... 
> 
>// 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches  
>//    the end, i.e., when the ad completes and finishes playing. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
> 
>....... 
>....... 
> 
>// 6. Track the MediaHeartbeat.Event.AdBreakComplete event when all  
>//    of the ads in the pod finish playing. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
> 
>....... 
>....... 
> 
>// Mid-roll 
>var adBreakInfo =  
>  MediaHeartbeat.createAdBreakObject(MIDROLL_BREAK_NAME, 
>                                     MIDROLL_BREAK_POSITION,  
>                                     MIDROLL_BREAK_START_TIME); 
>var adInfo =  
>  MediaHeartbeat.createAdObject(MIDROLL_AD_NAME,  
>                                MIDROLL_AD_ID,  
>                                MIDROLL_AD_POSITION,  
>                                MIDROLL_AD_LENGTH); 
> 
>// Custom ad metadata 
>var adMetadata = { 
>   CUSTOM_KEY_1 : CUSTOM_VAL_1,  
>   CUSTOM_KEY_2 : CUSTOM_VAL_2 
> 
>}; 
> 
>// 7. Track the MediaHeartbeat.Event.AdBreakStart event when the midroll  
>//    pod starts to play. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
> 
>....... 
>....... 
> 
>// 8. Track the MediaHeartbeat.Event.AdStart event when the midroll pod's  
>//    ad starts to play. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 9. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches  
>//    the end, i.e., when the ad completes and finishes playing. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
> 
>....... 
>....... 
> 
>// 10. Track the MediaHeartbeat.Event.AdBreakComplete event when all  
>//     of the ads in the midroll pod finish playing. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
> 
>....... 
>....... 
> 
>// Postroll 
>var adBreakInfo = MediaHeartbeat.createAdBreakObject(POSTROLL_BREAK_NAME,  
>POSTROLL_BREAK_POSITION, POSTROLL_BREAK_START_TIME); 
>var adInfo = MediaHeartbeat.createAdObject(POSTROLL_AD_NAME, POSTROLL_AD_ID,  
>POSTROLL_AD_POSITION, POSTROLL_AD_LENGTH); 
> 
>// Custom ad metadata 
>var adMetadata = { 
>   CUSTOM_KEY_1 : CUSTOM_VAL_1,  
>   CUSTOM_KEY_2 : CUSTOM_VAL_2 
> 
>}; 
> 
>// 11. Track the MediaHeartbeat.Event.AdBreakStart event when the postroll  
>//     pod starts to play. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
> 
>....... 
>....... 
> 
>// 12. Track the MediaHeartbeat.Event.AdStart event when the postroll pod's ad  
>//     starts to play. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 13. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches   
>//     the end, i.e., when the ad completes and finishes playing. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
> 
>....... 
>....... 
> 
>// 14. Track the MediaHeartbeat.Event.AdBreakComplete event when all of  
>//     the ads in the postroll pod finish playing. 
>this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
> 
>....... 
>....... 
> 
>// 15. Call trackComplete() when the playback reaches the end, i.e., when playback 
>//     completes and finishes playing. 
>this._mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 16. Call trackSessionEnd() when the playback session is over. This method must be called  
>//     even if the user does 
>not watch the video to completion. 
>this._mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

