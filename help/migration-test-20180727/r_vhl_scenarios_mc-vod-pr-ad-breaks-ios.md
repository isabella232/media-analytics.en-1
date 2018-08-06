---
description: In this scenario, the VOD content consists of a pre-roll ad, a second pre-roll ad, and then the content is played.
seo-description: In this scenario, the VOD content consists of a pre-roll ad, a second pre-roll ad, and then the content is played.
seo-title: Playback with a pre-roll ad break
title: Playback with a pre-roll ad break
uuid: ef313f6a-528e-47ff-a6b3-3978fe8b55be
index: y
internal: n
snippet: y
translate: y
---

# Playback with a pre-roll ad break


><a id="fig_49C7C3412C3B413EABE67C39260F6C40"></a> ![](graphics/preroll-regular-playback.png) 
>To view this scenario in iOS, set up the following code: >
>```
>//  Set up mediaObject 
>ADBMediaObject *mediaObject =  
>  [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
>                     length:VIDEO_LENGTH  
>                     streamType:ADBMediaHeartbeatStreamTypeVOD]; 
>    
>NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
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
>// context ad data 
>NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
>[adDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
>[adDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
>  
>// 2. Track the ADBMediaHeartbeatEventAdBreakStart event when the pre-roll pod  
>//    starts to play. Note that since this is a pre-roll, you must track the  
>//    "ADBMediaHeartbeatEventAdBreakStart" event before you call trackPlay. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
>                 mediaObject:adBreakObject  
>                 data:nil]; 
>....... 
>....... 
>  
>// 3. Track the ADBMediaHeartbeatEventAdStart event when the pre-roll pod's  
>//    ad starts to play. Note that since this is a pre-roll, you must track  
>//    the "ADBMediaHeartbeatEventAdStart" event before you call trackPlay. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
>                 mediaObject:adObject  
>                 data:adDictionary]; 
>....... 
>....... 
>  
>// 4. Call trackPlay when the playback actually starts, i.e., when the   
>//    first frame of the main content is rendered on the screen. 
>[_mediaHeartbeat trackPlay]; 
>....... 
>....... 
>  
>// 5. Track the ADBMediaHeartbeatEventAdComplete event when the ad reaches  
>//    the end, i.e., when the video completes and finishes playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
>                 mediaObject:nil  
>                 data:nil]; 
>....... 
>....... 
>  
>// 6. Track the ADBMediaHeartbeatEventAdStart event when the pre-roll pod's  
>//    second ad starts to play. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
>                 mediaObject:adBreakObject  
>                 data:nil]; 
>....... 
>....... 
>  
>// 7. Track the ADBMediaHeartbeatEventAdComplete event when the second ad  
>//    reaches the end, i.e., it completes and finishes playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
>                 mediaObject:nil  
>                 data:nil]; 
>....... 
>....... 
>  
>// 8. Track the ADBMediaHeartbeatEventAdBreakComplete event when all the  
>//    ads in the pod finish playing. 
>[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
>                 mediaObject:adBreakObject  
>                 data:nil]; 
>....... 
>....... 
>  
>// 9. Call trackComplete when the playback reaches the end, i.e., when the  
>//    video completes and finishes playing. 
>[_mediaHeartbeat trackComplete]; 
>....... 
>....... 
>  
>// 10. Call trackSessionEnd when the playback session is over. This method  
>//     must be called even if the user does not watch the video to completion. 
>[_mediaHeartbeat trackSessionEnd]; 
>....... 
>....... 
>
>```

