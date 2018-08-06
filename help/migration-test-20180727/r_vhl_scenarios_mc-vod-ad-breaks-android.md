---
description: Scenario  Pre-roll ads, the main content, mid-roll ads, the main content, and post-roll ads.
seo-description: Scenario  Pre-roll ads, the main content, mid-roll ads, the main content, and post-roll ads.
seo-title: Playback with ad breaks
title: Playback with ad breaks
uuid: a2d2696b-f636-4ecf-a5df-52620aa99122
index: y
internal: n
snippet: y
translate: y
---

# Playback with ad breaks


><a id="fig_50DBB9988C2E42268B1ABFA2467E78FB"></a> ![](graphics/ad-content-regular-playback.png) 
>To view this scenario in Android, set up the following code:
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
>//   i.e., there's an intent to start playback. 
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
>MediaObject adInfo = MediaHeartbeat.createAdObject(AD_NAME,  
>                                                   AD_ID,  
>                                                   AD_POSITION,  
>                                                   AD_LENGTH); 
> 
>// Context ad data 
>HashMap<String, String> adMetadata = new HashMap<String, String>(); 
>adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
>adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
> 
>// 2. Track the MediaHeartbeat.Event.AdBreakStart event when the pre-roll pod  
>//    starts to play. Note that since this is a pre-roll, you must track the  
>//    "MediaHeartbeat.Event.AdBreakStart" event before you call trackPlay().  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
> 
>....... 
>....... 
> 
>// 3. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's ad  
>//    starts to play. Note that since this is a pre-roll, you must track the  
>//    "MediaHeartbeat.Event.AdStart" event before you call trackPlay().  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
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
>// 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
>//    i.e., when the ad completes and finishes playing.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
> 
>....... 
>....... 
> 
>// 6. Track the MediaHeartbeat.Event.AdBreakComplete event when all of the ads in  
>//;    the pod finish playing. 
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
> 
>....... 
>....... 
> 
>// Mid-roll 
>MediaObject adBreakInfo =  
>  MediaHeartbeat.createAdBreakObject(mid-roll_BREAK_NAME,  
>                                     mid-roll_BREAK_POSITION,  
>                                     mid-roll_BREAK_START_TIME); 
>MediaObject adInfo =  
>  MediaHeartbeat.createAdObject(mid-roll_AD_NAME,  
>                                mid-roll_AD_ID,  
>                                mid-roll_AD_POSITION,  
>                                mid-roll_AD_LENGTH); 
> 
>// Context ad data 
>HashMap<String, String> adMetadata = new HashMap<String, String>(); 
>adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
>adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
> 
>// 7. Track the MediaHeartbeat.Event.AdBreakStart event when the mid-roll pod  
>//    starts to play.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
> 
>....... 
>....... 
> 
>// 8. Track the MediaHeartbeat.Event.AdStart event when the mid-roll pod's ad  
>//    starts to play.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 9. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
>//    i.e., when the adcompletes and finishes playing.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
> 
>....... 
>....... 
> 
>// 10. Track the MediaHeartbeat.Event.AdBreakComplete event when all the ads in the  
>//      mid-roll pod finish playing.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
> 
>....... 
>....... 
> 
>// Post-roll 
>MediaObject adBreakInfo =  
>  MediaHeartbeat.createAdBreakObject(POSTROLL_BREAK_NAME,  
>                                     POSTROLL_BREAK_POSITION,  
>                                     POSTROLL_BREAK_START_TIME); 
>MediaObject adInfo =  
>  MediaHeartbeat.createAdObject(POSTROLL_AD_NAME,  
>                                POSTROLL_AD_ID,  
>                                POSTROLL_AD_POSITION,  
>                                POSTROLL_AD_LENGTH); 
> 
>// Context ad data 
>HashMap<String, String> adMetadata = new HashMap<String, String>(); 
>adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
>adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
> 
>// 11. Track the MediaHeartbeat.Event.AdBreakStart event when the post-roll pod  
>//     starts to play.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
> 
>....... 
>....... 
> 
>// 12. Track the MediaHeartbeat.Event.AdStart event when the post-roll pod's  
>//     ad starts to play.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
> 
>....... 
>....... 
> 
>// 13. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the  
>//     end, i.e., when the ad completes and finishes playing. 
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
> 
>....... 
>....... 
> 
>// 14. Track the MediaHeartbeat.Event.AdBreakComplete event when all the ads in  
>//     the post-roll pod finish playing.  
>_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
> 
>....... 
>....... 
> 
>// 15. Call trackComplete() when the playback reaches the end, i.e., when the 
>//     video completes and finishes playing. 
>_mediaHeartbeat.trackComplete(); 
> 
>........ 
>........ 
> 
>// 16. Call trackSessionEnd() when the playback session is over. This method  
>//     must be called even if the user does not watch the video to completion.  
>_mediaHeartbeat.trackSessionEnd(); 
> 
>........ 
>........ 
>
>```

