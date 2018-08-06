---
description: In this scenario, VOD content is played back with a pre-roll ad, the content, a mid-roll ad, the content, and a post-roll ad.
seo-description: In this scenario, VOD content is played back with a pre-roll ad, the content, a mid-roll ad, the content, and a post-roll ad.
seo-title: Playback with ad breaks
title: Playback with ad breaks
uuid: c6834ccc-5bf2-4eac-b638-5507744e48a5
index: y
internal: n
snippet: y
translate: y
---

# Playback with ad breaks


><a id="fig_50DBB9988C2E42268B1ABFA2467E78FB"></a> ![](graphics/ad-content-regular-playback.png) 
>To view this scenario in iOS, set up the following code: >
>```
>//  Set up mediaObject 
>ADBMediaObject *mediaObject =  
>  [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
>                     length:VIDEO_LENGTH  
>                     streamType:ADBMediaHeartbeatStreamTypeVOD]; 
>   
>NSMutableDictionary *videoContextData =  
>  [[NSMutableDictionary alloc] init]; 
>[videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
>[videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
>  
>// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
>//    i.e., there is an intent to start playback. 
>[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
>....... 
>....... 
>  
>// Pre-roll 
>ADBMediaObject *adBreakInfo =  
>  [ADBMediaHeartbeat createAdBreakObjectWithName:AD_BREAK_NAME  
>                     position:AD_BREAK_POSITION  
>                     startTime:AD_BREAK_START_TIME]; 
>ADBMediaObject *adInfo =  
>  [ADBMediaHeartbeat createAdObjectWithName:AD_NAME  
>                     adId:AD_ID  
>                     position:AD_POSITION  
>                     length:AD_LENGTH]; 
>  
>// Context ad data 
>NSMutableDictionary *adDictionary =  
>  [[NSMutableDictionary alloc] init]; 
>[adDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
>[adDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
>  
>// 2. Track the ADBMediaHeartbeatEventAdBreakStart event when the  
>//    pre-roll pod starts to play. Note that since this is a pre-roll,  
>//    you must track the ADBMediaHeartbeatEventAdBreakStart event  
>//    before you call trackPlay. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
>                 mediaObject:adBreakObject  
>                 data:adDictionary]; 
>....... 
>....... 
>  
>// 3. Track the ADBMediaHeartbeatEventAdStart when the pre-roll  
>//    pod's ad starts to play. Note that since this is a pre-roll,  
>//    you must track the ADBMediaHeartbeatEventAdStart before you 
>//    call trackPlay. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
>                  mediaObject:adObject  
>                  data:adDictionary]; 
>....... 
>....... 
>  
>// 4. Call trackPlay when the playback actually starts, i.e., when 
>//    the first frame of the main content is rendered on the screen. 
>[_mediaHeartbeat trackPlay]; 
>....... 
>....... 
>  
>// 5. Track the ADBMediaHeartbeatEventAdComplete event when the ad  
>//    reaches the end, i.e., when it completes and finishes playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
>                  mediaObject:nil  
>                  data:nil]; 
>....... 
>....... 
>  
>// 6. Track the ADBMediaHeartbeatEventAdBreakComplete event when all  
>//    of the ads in the pod finish playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
>                  mediaObject:nil  
>                  data:nil]; 
>....... 
>....... 
>  
>// Mid-roll 
>ADBMediaObject *adBreakInfo =  
>  [ADBMediaHeartbeat createAdBreakObjectWithName:MIDROLL_BREAK_NAME  
>                     position:MIDROLL_BREAK_POSITION  
>                     startTime:MIDROLL_BREAK_START_TIME]; 
>ADBMediaObject *adInfo =  
>  [ADBMediaHeartbeat createAdObjectWithName:MIDROLL_AD_NAME  
>                     adId:MIDROLL_AD_ID position:MIDROLL_AD_POSITION  
>                     length:MIDROLL_AD_LENGTH]; 
>  
>// context ad data 
>NSMutableDictionary *midrollAdDictionary = [[NSMutableDictionary alloc] init]; 
>[midrollAdDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
>[midrollAdDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
>  
>// 7. Track the ADBMediaHeartbeatEventAdBreakStart event when the mid-roll pod  
>//    starts to play. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
>                  mediaObject:adBreakObject  
>                  data:nil]; 
>....... 
>....... 
>  
>// 8. Track the ADBMediaHeartbeatEventAdStart event when the mid-roll pod's  
>//    ad starts to play. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
>                 mediaObject:adObject  
>                 data:midrollAdDictionary]; 
>....... 
>....... 
>  
>// 9. Track the ADBMediaHeartbeatEventAdComplete event when the ad reaches  
>//    the end, i.e., when it completes and finishes playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
>                 mediaObject:nil  
>                 data:nil]; 
>....... 
>....... 
>  
>// 10. Track the ADBMediaHeartbeatEventAdBreakComplete event when all the  
>//     ads in the mid-roll pod finish playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
>                 mediaObject:nil  
>                 data:nil]; 
>....... 
>....... 
>  
>// Post-roll 
>ADBMediaObject *postrollBreakInfo =  
>  [ADBMediaHeartbeat createAdBreakObjectWithName:POSTROLL_BREAK_NAME  
>                     position:POSTROLL_BREAK_POSITION  
>                     startTime:POSTROLL_BREAK_START_TIME]; 
>ADBMediaObject *adInfo =  
>  [ADBMediaHeartbeat createAdObjectWithName:POSTROLL_AD_NAME  
>                     adId:POSTROLL_AD_ID  
>                     position:POSTROLL_AD_POSITION  
>                     length:POSTROLL_AD_LENGTH]; 
>  
>// Context ad data 
>NSMutableDictionary *postrollAdDictionary =  
>  [[NSMutableDictionary alloc] init]; 
>[postrollAdDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
>[postrollAdDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
>  
>// 11. Track the ADBMediaHeartbeatEventAdBreakStart event when the  
>//     post-roll pod starts to play. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
>                 mediaObject:adBreakObject  
>                 data:nil]; 
>....... 
>....... 
>  
>// 12. Track the ADBMediaHeartbeatEventAdStart event when the  
>//     post-roll pod's ad starts to play. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
>                 mediaObject:adObject  
>                 data:postrollAdDictionary]; 
>....... 
>....... 
>  
>// 13. Track the ADBMediaHeartbeatEventAdComplete event when the  
>//     post-roll pod's ad finishes playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
>                 mediaObject:nil  
>                 data:nil]; 
>....... 
>....... 
>  
>// 14. Track the ADBMediaHeartbeatEventAdBreakComplete event when  
>//     all the ads in the post-roll pod finish playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
>                 mediaObject:nil data:nil]; 
>....... 
>....... 
>  
>// 15. Call trackComplete when the playback reaches the end,  
>//     i.e., when the video completes and finishes playing. 
>[_mediaHeartbeat trackComplete]; 
>....... 
>....... 
>  
>// 16. Call trackSessionEnd when the playback session is over. This method  
>//     must be called even if the user does not watch the video to completion. 
>[_mediaHeartbeat trackSessionEnd]; 
>....... 
>....... 
>
>```

